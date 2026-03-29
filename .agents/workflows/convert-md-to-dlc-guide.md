---
description: Convert a raw Markdown file into a styled Astro DLC walkthrough guide.
---

# AI INSTRUCTIONS: DLC Content Processing Guidelines

**CRITICAL:** When converting or processing large source documents (e.g., massive markdown files), you MUST follow these instructions to ensure 100% fidelity. Do not summarize, omit, or hallucinate content. Maintain a true 1:1 parity with the source text.

## 1. Handle Output Limitations Safely

- **Acknowledge Constraints:** You have a hard limit on how many tokens you can generate in a single response.
- **Do Not Summarize:** If a source document or requested output is too large to fit in one response, DO NOT summarize, compress, or skip content to force it to fit.
- **Stop and Chunk:** If you cannot write the entire file, stop and process it in parts.

## 2. Standard Processing Protocol for Large Files

- **Use Placeholders:** When creating a new file from a large source, create the layout scaffolding first with placeholders (e.g., `<!-- INSERT_PART_1 -->`, `<!-- INSERT_PART_2 -->`).
- **Sequential Insertion:** Process and fill in each placeholder in separate, sequential tool calls. This resets your output token count for each section.

## 3. Editing Existing Files

- **Avoid Bulk Rewrites:** Do not rewrite an entire large file just to change a small amount of formatting.
- **Use Surgical Edits:** Target only the specific lines or elements that need changing. Leave the raw text blocks completely untouched by your generative engine.

---

Follow these steps to convert a markdown file into an Astro DLC walkthrough guide:

1. **Acknowledge Output Limitations**: Determine the size of the source file. If it's too large to convert in a single response, use the chunking protocol described in the guidelines above. Maintain 1:1 parity with the source text.

2. **Page Wrapper**: Create the `.astro` file wrapper:
   - Import `DlcLayout` (not `WalkthroughLayout`) and needed components (`QuestStep`, `Image`, `Video`, `Tip`, `BossFight`, `MediaGrid`, `EndLogo`, `StoryBlurb`).
   - Optionally declare `const baseUrl = import.meta.env.BASE_URL;` in the frontmatter.
   - Map `<h2>` headers into the `sections` array and use `<DlcLayout>`.
   - Always include a relevant `subtitle` prop in `<DlcLayout>` (e.g., 'DLC WALKTHROUGH' or 'DLC SIDE QUEST WALKTHROUGH').
   - Include `guideId` prop matching the page slug (e.g., `guideId="dlc-beyond-the-rift"`).

3. **Text Formatting**:
   - Regular walkthrough instructions should be plain text inside `<p>` tags without any italic formatting.

4. **Sections Mapping**:
   - Add HTML comments to mark section boundaries (e.g., `<!-- SECTION 1: Step into the Mushroom Forest -->`).
   - Wrap top-level regions in `<section id="ID" class="content-section">` (NOT `walkthrough-section`).
   - Each section should have an `<h2>` heading matching the section label.
   - Wrap specific objectives in `<QuestStep id="ID" title="Title">`.
   - **ID Naming Convention**: QuestStep IDs should append `-quest` to the section ID (e.g., section `step-into-the-mushroom-forest` → QuestStep `step-into-the-mushroom-forest-quest`).

5. **Media Mapping**:
   - Use `<Image src="..." alt="..." />` for single images (wrap in component, not raw `<div class="media-container">`).
   - **Image URLs**: For images sourced from Neoseeker, use the external CDN URLs directly (e.g., `https://cdn.staticneo.com/ew/1/16/Ec_805.jpg`). Do NOT use local paths like `${baseUrl}images/dlc/ec-805.jpg` unless the images have been downloaded to the project.
   - Use `<Video id="YOUTUBE_ID" title="..." />` for videos (not raw `<iframe>` tags).
   - Use `<MediaGrid columns={2}>` to wrap multiple `<Image>` components (not raw `<div class="media-grid">`).

6. **Callouts**:
   - Use `<Tip type="tip|warning|note">` for NOTE/blockquote sections.
   - **Nested Tips**: `<Tip>` components can be nested inside each other.
   - **Vin Comments**: For author commentary/inner dialogue, use the `<vin>` tag inside a `<Tip>`:
     ```astro
     <Tip type="note">
       <vin>Personal commentary or inner dialogue here.</vin>
     </Tip>
     ```

7. **Boss Fights**: Use `<BossFight title="...">` for boss sections, including a `<Video>` and list of stats inside.

8. **QuestStep Component**:
   - **Always use `<QuestStep id="ID" title="Title">`** for quest objectives (not manual `<article>` with `<h3>` and `<img>` tags).
   - The `id` should be a kebab-case version of the objective title (e.g., "Head for the top of Raminas Tower" → `head-for-the-top-of-raminas-tower`).
   - The `title` should be the exact objective text as it appears in the source.
   - **Common Mistake**: Do NOT use raw HTML like `<article id="..." class="quest-step"><h3><img src="..." class="obj-icon" /></h3>...</article>`. Always use the `<QuestStep>` component.

9. **Controller Button Images**: For controller button references, use inline `<img>` tags with specific styling:

```astro
Press <img
  src="https://cdn.staticneo.com/ew/thumb/6/6f/PSSQUARE.png/21px-PSSQUARE.png"
  alt="PS Square button"
  style="vertical-align: middle"
/>
```

Common button URLs:

- Cross: `https://cdn.staticneo.com/ew/thumb/1/11/PSCROSS.png/21px-PSCROSS.png`
- Square: `https://cdn.staticneo.com/ew/thumb/6/6f/PSSQUARE.png/21px-PSSQUARE.png`
- R1: `https://cdn.staticneo.com/ew/thumb/8/86/PSR1.png/21px-PSR1.png`

10. **Lists**: Use standard HTML `<ul>` and `<li>` tags for unordered lists:

```astro
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

11. **Next Steps**: Use `<EndLogo />` at the very bottom.

12. **Closing Style Block**: After `<EndLogo />` and before closing `</DlcLayout>`, add a `<style>` block:

    ```astro
    </DlcLayout>

    <style>
      .content-section {
        padding: 2rem 0;
      }

      .content-section h2 {
        color: var(--accent-gold);
        border-bottom: 1px solid var(--border-color);
        padding-bottom: 0.75rem;
        margin-bottom: 1.5rem;
        font-size: clamp(1.5rem, 4vw, 2rem);
        text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
      }
    </style>
    ```

13. **Astro Syntax**:
    - Escape bare ampersands `&`.
    - Ensure imports are at the top.
