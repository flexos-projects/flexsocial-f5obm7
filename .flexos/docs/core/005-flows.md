---
id: flows
title: User & Data Flows
description: A description of the key user journeys and data processing pipelines.
type: doc
subtype: core
status: draft
sequence: 5
tags:
  - flows
  - ux
  - architecture
createdAt: "2023-10-27T10:00:00.000Z"
updatedAt: "2023-10-27T10:00:00.000Z"
---

This document describes the critical user and data flows within the flexSocial application. It connects the user actions described in the **Pages** document with the data models in the **Database** schema and the features in the **Features** list.

### Flow 1: New User Onboarding & Persona Creation

This flow is the most critical for user activation and long-term success. The goal is to gather enough information to make the AI useful from day one.

1.  **User Action:** User signs up and is redirected to `/onboarding/persona`.
2.  **UI/UX:** The user is guided through a multi-step wizard as outlined in the **Pages** document.
3.  **Data Flow:**
    *   A new document is created in the `users` collection.
    *   As the user progresses, a new document is created in the `personas` collection, linked by `userId`.
    *   When the user submits knowledge sources (URLs, files), they are added to the `knowledgeSources` array in their `personas` document.
    *   A background job is triggered for each new source:
        *   **If URL:** A web scraper fetches and cleans the text content.
        *   **If File:** A parser extracts text from the document.
        *   The extracted text is chunked into smaller, manageable pieces.
        *   Each chunk is passed to an embedding model (e.g., OpenAI's Ada) to create a vector embedding.
        *   The chunk text, source metadata, and the resulting vector are stored in the `vectors` collection, linked to the `userId` and `personaId`.
    *   Goal and style settings are saved directly to the `personas` document.
    *   Connecting a social account creates a new document in the `social_connections` collection, storing the encrypted OAuth tokens.

### Flow 2: The Core Content Creation Loop

This is the primary day-to-day user flow for creating content.

1.  **User Action:** User adds a new item to "The Stream" via the Quick Add form on the `/dashboard` or the `/stream` page.
2.  **UI/UX:** User provides a URL, text, or media. They select an `Intent` (`Agree`, `Disagree`, `Promote`), set the `Intensity`, and add optional context.
3.  **Data Flow:**
    *   A new document is created in the `raw_content` collection with a status of `pending`.
    *   A serverless function or background worker is triggered by this new document.
4.  **AI Processing (Backend):**
    *   The background job changes the `raw_content` status to `processing`.
    *   **Context Retrieval:** The AI queries the `vectors` collection using the user's `raw_content` input (and context) as the query. The top N most relevant chunks of the user's persona are retrieved (Retrieval-Augmented Generation - RAG).
    *   **Prompt Engineering:** A detailed prompt is constructed for a Large Language Model (LLM). This prompt includes:
        *   The retrieved persona context.
        *   The user's style and goal settings from their `personas` document.
        *   The content of the `raw_content` item.
        *   The user's specified `Intent`, `Intensity`, and `Context`.
        *   Instructions to generate multiple post stubs (Flexes) and optimize them for different platforms.
    *   **LLM Invocation:** The prompt is sent to the LLM (e.g., GPT-4).
    *   **Output Parsing:** The LLM's response is parsed.
    *   For each generated post idea, a new document is created in the `flexes` collection with a status of `for_review`. This document links back to the original `raw_content` item.
    *   The `raw_content` document status is updated to `processed`.

### Flow 3: Review, Approval, and Scheduling

This flow covers the user's interaction with the AI's output.

1.  **User Action:** User navigates to the `/studio` page.
2.  **UI/UX:** The user sees the newly generated Flexes in the "For Review" column of the Kanban board.
3.  **User Action:** User clicks on a Flex card to open the detail view.
4.  **UI/UX:** The user reviews the platform-optimized content in the tabbed interface. They can make manual edits to the text, swap media, or approve the suggestions.
5.  **User Action:** User clicks "Schedule" for one or more platform versions of the Flex.
6.  **Data Flow:**
    *   For each approved platform post, a new document is created in the `scheduled_posts` collection. This document contains the final content, media URLs, target platform, and the `scheduledAt` timestamp.
    *   The status of the parent `flexes` document is updated (e.g., parts of it are now `scheduled`). If all optimizations are actioned, the Flex might move to the `Scheduled` column.
7.  **Backend Cron Job:**
    *   A time-based scheduler (e.g., a cron job) runs every minute.
    *   It queries the `scheduled_posts` collection for posts where `scheduledAt` is in the past and `status` is `scheduled`.
    *   For each found post, it retrieves the appropriate credentials from the `social_connections` collection.
    *   It calls the relevant social media API to publish the post.
    *   On success, it updates the `scheduled_posts` document status to `posted` and saves the resulting post URL. On failure, it updates the status to `failed` and logs the error.