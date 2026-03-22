---
description: Convert a raw Markdown file into a styled Astro walkthrough guide.
---

# AI INSTRUCTIONS: Content Processing Guidelines

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

Follow these steps to convert a markdown file into an Astro walkthrough guide:

1. **Acknowledge Output Limitations**: Determine the size of the source file. If it's too large to convert in a single response, use the chunking protocol described in the guidelines above. Maintain 1:1 parity with the source text.
2. **Page Wrapper**: Create the `.astro` file wrapper:
   - Import `WalkthroughLayout` and needed components (`QuestStep`, `Image`, `Video`, `Tip`, `BossFight`, `MediaGrid`, `NextSteps`, `StoryBlurb`).
   - Map `<h2>` headers into the `sections` array and use `<WalkthroughLayout>`.
3. **Global Content Introduction**: Wrap story text in `<StoryBlurb>`.
4. **Sections Mapping**: 
   - Wrap top-level regions in `<section id="ID" class="walkthrough-section">`.
   - Wrap specific objectives in `<QuestStep id="ID" title="Title">`.
5. **Media Mapping**: 
   - Use `<Image src="..." alt="..." />` for single images.
   - Use `<Video id="YOUTUBE_ID" title="..." />` for videos.
   - Use `<MediaGrid columns={2}>` to wrap multiple `<Image>` components.
6. **Callouts**: Use `<Tip type="tip|warning|note">` for NOTE/blockquote sections.
7. **Boss Fights**: Use `<BossFight title="...">` for boss sections, including a `<Video>` and list of stats inside.
8. **Next Steps**: Use `<NextSteps links={[{ href: "...", label: "..." }]} />` at the very bottom.
9. **Astro Syntax**:
    - Escape bare ampersands `&amp;`.
    - Ensure imports are at the top.
10. **Link to TOC / Sidebar**: Add the new guide to `Layout.astro` and `table-of-contents.astro`.
