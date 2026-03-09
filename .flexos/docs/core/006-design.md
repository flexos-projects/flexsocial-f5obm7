---
id: design
title: Design System & Branding
description: Guidelines for the visual identity, branding, and UI components of flexSocial.
type: doc
subtype: core
status: draft
sequence: 6
tags:
  - design
  - branding
  - ui
createdAt: "2023-10-27T10:00:00.000Z"
updatedAt: "2023-10-27T10:00:00.000Z"
---

## 1. Brand Identity & Philosophy

The flexSocial brand should feel empowering, intelligent, and minimalist. It's a professional tool for creative people, so the design must be clean and functional, allowing the user's content to take center stage. The aesthetic is inspired by modern productivity apps and creative software—think Notion meets Figma. We avoid the loud, attention-grabbing design language of social media platforms themselves.

*   **Keywords:** Authentic, Smart, Effortless, Clean, Focused, Creative.
*   **Logo:** A simple, abstract mark that combines the letter 'f' with a subtle 'S' curve or a visual representation of a 'flex' or 'flow'. It should be modern and geometric.

## 2. Color Palette

Our color palette is built around a single, vibrant primary color to create a strong brand association, balanced by a sophisticated and muted set of neutrals for the UI.

*   **Primary:** `#10b981` (Emerald Green)
    *   **Usage:** Call-to-action buttons, active states, links, key highlights, and branding elements. It signifies growth, intelligence, and 'go'.
*   **Neutral Palette (Dark Mode First):**
    *   **Background:** `#0f172a` (Slate-900) - A very dark, slightly blue-tinted gray.
    *   **UI Panels/Cards:** `#1e293b` (Slate-800) - The primary surface color for cards and sidebars.
    *   **Borders/Dividers:** `#334155` (Slate-700) - For subtle separation between elements.
    *   **Text (Primary):** `#f1f5f9` (Slate-100) - For headings and important text.
    *   **Text (Secondary):** `#94a3b8` (Slate-400) - For body copy, labels, and less important text.
*   **Accent Colors:**
    *   **Warning/Alert:** `#f59e0b` (Amber-500)
    *   **Error/Destructive:** `#ef4444` (Red-500)
    *   **Success:** `#22c55e` (Green-500)

## 3. Typography

We will use a clean, modern, and highly legible sans-serif typeface available via a service like Google Fonts to ensure consistency.

*   **Primary Typeface:** Inter
*   **Headings (`h1`, `h2`, `h3`):** Inter Bold (or SemiBold). Sizing will follow a modular scale (e.g., 36px, 24px, 20px).
*   **Body & UI Text:** Inter Regular. Base font size will be 16px for readability.
*   **Code/Monospace:** A monospaced font like `Fira Code` or `JetBrains Mono` can be used for any code-like text or to display hashtags for clarity.

## 4. UI Components

We will build a library of reusable UI components to ensure a consistent user experience across the application, as described in the **Pages** document.

*   **Buttons:**
    *   **Primary:** Solid `primary` color background with light text.
    *   **Secondary:** Outlined with `primary` color, transparent background.
    *   **Tertiary/Ghost:** No border or background, just colored text.
*   **Cards:** The primary container for content like Flexes and Stream items. They will have a subtle border (`#334155`), a slightly lighter background (`#1e293b`), and a `border-radius` of 8-12px for a modern, soft look.
*   **Forms & Inputs:** Clean and simple. Inputs will have a dark background, a subtle border, and a clear focus state using the `primary` color. Labels will be placed above the input field.
*   **Modals:** Used for focused tasks like the Flex Detail View. They will appear over a semi-transparent dark overlay to focus the user's attention.
*   **Kanban Board (Flex Studio):** This is a key UI pattern. Columns will be clearly labeled, and cards will be draggable. We will use subtle visual cues (like a colored left border on the card) to indicate status or platform.
*   **The Intent Engine UI:** This is a signature component. It will be a custom-designed control featuring three distinct buttons for `Agree`, `Disagree`, `Promote`. When one is selected, a horizontal slider appears below it to set the `Intensity`, providing clear visual feedback.

## 5. Iconography

We will use a single, consistent icon set (e.g., Heroicons or Feather Icons) for all UI iconography. Icons should be minimalist and line-based to match the overall aesthetic. Social media platform icons will use their official brand logos.