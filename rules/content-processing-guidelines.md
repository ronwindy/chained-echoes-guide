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

## 4. Separation of Content and Layout (Astro Specific)
- **Prefer Raw Content:** Keep source content as raw Markdown (`.md` or `.mdx`) whenever possible.
- **Use Slots:** Use Astro Content Collections or Layouts that inject the markdown into a `<slot />`. Avoid converting raw markdown text directly into complex Astro/HTML components unless explicitly requested.
