---
id: pages
title: Pages & User Interface
description: A sitemap and description of the primary pages and UI components in flexSocial.
type: doc
subtype: core
status: draft
sequence: 3
tags:
  - ui
  - ux
  - sitemap
createdAt: "2023-10-27T10:00:00.000Z"
updatedAt: "2023-10-27T10:00:00.000Z"
---

This document outlines the key pages and user interface structure of the flexSocial application. It provides a blueprint for the user's journey through the platform, referencing features described in the **Core Features** document.

## 1. Public Pages

*   **`/` (Landing Page):** The main marketing page. It will clearly articulate the value proposition from the **Vision** document, showcase key features, display pricing tiers, and have prominent call-to-action buttons for signing up.
*   **`/login`:** User login page with email/password and social sign-on options (Google, etc.).
*   **`/signup`:** User registration page.

## 2. Onboarding

*   **`/onboarding/persona`:** A multi-step wizard that guides new users through the initial setup of their **Persona Engine**. This is a critical flow for user success.
    *   **Step 1: Basics:** Set display name, and upload a profile picture.
    *   **Step 2: Knowledge Ingestion:** A component with tabs for URL input, document upload, and direct text input. We will encourage users to provide at least one significant source (e.g., their personal website) to start.
    *   **Step 3: Goals & Style:** The interface for the **Goal & Style Configuration**, including the goal selector and tone sliders.
    *   **Step 4: Connect Accounts:** The UI for the **Account Connector** to link their social media profiles via OAuth.

## 3. Core Application Pages (Authenticated)

All core app pages will share a persistent navigation sidebar for easy access to key areas.

*   **`/dashboard` (Home):** The main landing page after login. It serves as a central hub.
    *   **Component: Quick Add to Stream:** A prominent form at the top of the page for quickly adding new `raw_content` (URL, text, or media upload) and setting the `Intent`.
    *   **Component: "For Review" Queue:** A compact list or carousel showing the top 3-5 Flexes currently in the `For Review` status, prompting the user to take action.
    *   **Component: Scheduled Posts:** A calendar or timeline view of upcoming posts.
    *   **Component: Recent Performance:** A small module with high-level analytics from the last 7 days.

*   **`/stream`:** A dedicated page for managing the `raw_content` feed. 
    *   It will display a reverse-chronological list of all submitted items.
    *   Each item will be a card showing the content, the user's selected `Intent` and `Intensity`, and a status indicator (e.g., "Processing," "Flexes Generated").
    *   A persistent "Add to Stream" button will be present.

*   **`/studio` (The Flex Studio):** The workspace for managing generated content.
    *   **Default View: Kanban Board:** The primary interface will be a multi-column board representing the content pipeline: `Drafts`, `For Review`, `Scheduled`, `Published`.
    *   **Flex Cards:** Each card on the board represents a single Flex and will display a snippet of the generated text, a media preview, and icons for the target social platforms.
    *   **Flex Detail View:** Clicking a card will open a modal or a dedicated page (`/studio/:flexId`). This view contains the **Multi-Platform Optimizer** interface, with tabs for each social network. Each tab shows the tailored content and provides options to edit, approve, or discard the suggestion.

*   **`/analytics`:** The **Performance Dashboard** page.
    *   Will feature filterable charts and data visualizations for engagement metrics over time.
    *   Users can filter by social account, content type, or the original `Intent` to understand what resonates with their audience.

*   **`/settings`:** A multi-tabbed page for account management.
    *   **`/settings/profile`:** Manage basic account information (name, email, password).
    *   **`/settings/persona`:** A page to edit and add to the **Persona Engine**. Users can add new knowledge sources or re-run the AI analysis.
    *   **`/settings/style`:** A page to adjust the **Goal & Style Configuration** settings.
    *   **`/settings/accounts`:** Manage connected social media accounts (add new ones, re-authenticate, or remove).
    *   **`/settings/billing`:** Manage subscription plan and payment information.