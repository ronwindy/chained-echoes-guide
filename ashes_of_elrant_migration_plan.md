# Migrate Ashes of Elrant DLC to a Standalone Guide

We will extract the "Ashes of Elrant DLC" section out of the main guide's structure and give it its own dedicated layout, navigation, and background. This architectural change ensures both guides remain focused and scalable for future pages.

## Proposed Changes

---

### Layouts & Navigation Architecture

We will create a specific layout for the DLC guide so it can maintain its own sidebar structure and styling without bloating the main `Layout.astro`.

#### [NEW] DlcLayout.astro
- An exact structural copy of `Layout.astro`.
- **Sidebar Changes**: The sidebar will *only* contain DLC sections (Introduction, Walkthrough, Sidequest, Reward Board, Guides) with URLs mapped to `/ashes-of-elrant-dlc/...`. 
- **Backlink**: It will include a "Return to Main Guide" link in the "Getting Started" section.
- **Background**: We will add a `<body class="dlc-theme">` tag to allow custom background styling.
- **Completion Tracking**: It will use a completely separate tracking system reading from a `chained-echoes-dlc-completed` localStorage key so that the DLC guide tracks separately from the main game.

#### [MODIFY] Layout.astro
- Remove the entire "Ashes of Elrant DLC" details section from the sidebar.
- Add a new callout or simple navigation link pointing to the new DLC Table of Contents (`/ashes-of-elrant-dlc/table-of-contents`).

---

### Table of Contents (TOC)

We will separate the TOC pages so the DLC feels like an independent guide.

#### [NEW] table-of-contents.astro (DLC)
- Create a new TOC page specifically for the DLC at `/ashes-of-elrant-dlc/table-of-contents`.
- It will use `<DlcLayout>` instead of `<Layout>`.
- It will contain the sections previously housed in the main TOC (Walkthrough, Sidequests, Reward Board, Guides for the DLC).
- Update the completion script on this page to use `chained-echoes-dlc-completed`.

#### [MODIFY] table-of-contents.astro (Main)
- Remove the full "Ashes of Elrant DLC" breakdown.
- Replace it with a single, prominent card: "Play the Ashes of Elrant DLC Guide" that links to the new DLC TOC.

---

### Styling

#### [MODIFY] global.css
- Add styling for `body.dlc-theme` to override the main background image (`chained-echoes-1.avif`) with a placeholder background color or image specifically for the DLC guide, creating an immediate visual distinction between the base game guide and the DLC guide.

## Verification Plan

### Automated Tests
- Run `npm run build` to ensure there are no build issues or broken routes.

### Manual Verification (User Instructions)
*The user will verify the following manually without using the browser agent:*
- Navigate to the main TOC and confirm the DLC is removed and correctly linked out.
- Navigate to `/ashes-of-elrant-dlc/table-of-contents` to verify the new sidebar, new TOC features, and the new visual default placeholder background.
- Verify the mobile hamburger menu works on the new layout.
- Test that marking an item as completed in the DLC updates the green checks separately from the main guide.
