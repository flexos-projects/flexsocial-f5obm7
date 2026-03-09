---
id: features
title: Core Features
description: A detailed breakdown of flexSocial's primary functionalities and modules.
type: doc
subtype: core
status: draft
sequence: 2
tags:
  - features
  - product
createdAt: "2023-10-27T10:00:00.000Z"
updatedAt: "2023-10-27T10:00:00.000Z"
---

## 1. Persona Engine

The Persona Engine is the foundation of flexSocial, responsible for creating a deep, evolving understanding of the user's identity. This is not a static profile but a living knowledge base used by the AI to ensure all generated content is authentic. The data for this is managed in the `personas` collection, as detailed in the **Database** documentation.

*   **Knowledge Base Ingestion:** Users can populate their persona by providing various sources:
    *   **URL Scraping:** Provide links to personal websites, blogs, portfolios, or specific articles. The system will crawl and index the text content.
    *   **Document Upload:** Upload PDFs (e.g., brand guidelines, CVs), and text documents.
    *   **Direct Text Input:** A large text area for a "brain dump" of core beliefs, mission statements, or key biographical information.
    *   **Image Analysis:** Upload logos and key brand imagery. The AI will analyze these for color palettes and stylistic elements to inform visual asset generation.
*   **AI Analysis & Vectorization:** All ingested content is processed, chunked, and stored as vector embeddings in our `vectors` collection. This allows for semantic search and retrieval (RAG) during content generation, ensuring the AI can pull relevant, personal context.

## 2. Goal & Style Configuration

This module allows users to provide explicit instructions to the AI, guiding the tone, style, and strategic direction of the generated content.

*   **Goal Selector:** Users choose a primary objective from a predefined list (e.g., "Build Audience," "Generate Leads," "Establish Thought Leadership," "Be Provocative"). This choice influences the call-to-actions and overall framing of the generated posts.
*   **Tone & Voice Matrix:** A set of sliders and multi-select options to define the communication style:
    *   `Formality`: Casual <--> Professional
    *   `Humor`: Witty/Sarcastic <--> None
    *   `Complexity`: Simple/Accessible <--> Technical/Nuanced
    *   `Emoji Usage`: High <--> Low/None
*   **Core Hashtag Bank:** A dedicated area to store and manage evergreen hashtags related to the user's industry and core topics.

## 3. The Stream (Content Ingestion)

The Stream is the primary user interaction point for day-to-day use. It's designed for low-friction input of raw content and ideas. Each submission creates a document in the `raw_content` collection.

*   **Multi-Modal Input:** Users can add content via:
    *   **URL:** Paste a link to an article, video, or another social media post.
    *   **Text:** Write or paste any amount of text, from a single thought to a full article.
    *   **Media Upload:** Upload images or short videos.
*   **The Intent Engine:** This is the critical feature that adds user perspective. For every item added to The Stream, the user must specify:
    *   **Intent:** A choice of `Agree`, `Disagree`, or `Promote`.
    *   **Intensity:** A slider from 1 (mild) to 5 (strong).
    *   **Context:** An optional text field to add specific thoughts, a key quote to highlight, or instructions for the AI.

## 4. The Flex Studio (Content Generation & Management)

The Flex Studio is where the AI's output is reviewed, refined, and scheduled. It's a comprehensive workspace for managing the content lifecycle.

*   **Flex Draft Dashboard:** A Kanban-style view (`Drafts`, `For Review`, `Scheduled`, `Published`) displaying all generated "Flexes" (post stubs). Each Flex is a card that shows the source `raw_content` item and a summary of the generated post.
*   **Multi-Platform Optimizer:** Clicking on a Flex card opens a detailed view with tabs for each connected social media account (e.g., Twitter, LinkedIn, Instagram). 
    *   The AI automatically generates optimized versions of the content for each platform, respecting character limits, formatting conventions, and audience expectations.
    *   For Instagram, it might suggest a carousel post. For Twitter, a concise thread. For LinkedIn, a more professional, long-form post.
*   **AI Asset Generation:** The system will automatically propose or generate visual assets based on the content and the user's **Persona Engine** visual guidelines. This can include:
    *   Creating a quote graphic from a key sentence.
    *   Finding a relevant stock image and applying a brand color overlay.
    *   Formatting a user-uploaded video into a 9:16 Reel/Short with animated captions.
*   **Scheduler & Publisher:** Once approved, users can schedule the optimized posts for each platform individually or simultaneously.

## 5. Account Connector & Analytics

*   **Secure OAuth 2.0 Integration:** A settings page to securely connect and manage social media profiles for Twitter, LinkedIn, Facebook Pages, Instagram Professional, and TikTok.
*   **Performance Dashboard:** A simple analytics view that tracks key metrics (likes, comments, shares, reach) for all content published via flexSocial, allowing users to see which types of `raw_content` and `intents` perform best.