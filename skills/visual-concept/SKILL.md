---
name: visual-concept
description: >-
  Use when generating image-based visual concepts, UI explorations, product mockups, moodboards, or design
  directions for brainstorming. Helps create tasteful image-generation prompts, avoid AI-sloppy outputs,
  inspect results, and copy selected images into the project.
---

# Visual Concept

Create tasteful image-generated visual concepts for early product and UI exploration.

Use this skill as the taste layer before calling image generation. Do not use it for deterministic diagrams, coded UI mockups, or production UI implementation.

## Core Rules

- Treat these as three separate paths:
  - Built-in `image_gen`: preferred for image-generated concepts. Does not require `OPENAI_API_KEY`.
  - OpenAI Images API or CLI fallback: only after explicit user approval and credential setup.
  - Coded/local rendering: not image generation. Use only for narrowed layout or interaction validation, or when the user explicitly chooses it.
- If built-in `image_gen` is unavailable in the current Codex surface, say so plainly and stop. Do not substitute API calls or coded mockups without asking.
- In a project repo, every generated visual used for brainstorming or product direction must be copied into the repo before it is presented as the usable artifact. The built-in tool may leave the original under `~/.codex/generated_images/`; that is only the source copy.
- Generate visuals only when seeing the product direction would help more than text.
- Keep each image tied to one product/design question.
- Avoid exact small UI text. Use broad visual structure and large readable labels only when necessary.
- Treat generated images as exploratory artifacts, not source-of-truth UI.
- For UI mockups, describe the product as if it already exists. Ask for practical, usable interface structure rather than concept art.

## Prompt Process

1. Identify the decision the image should clarify.
2. Choose the artifact plan:
   - image type: product UI concept, mood surface, comparison board, reference-backed variation, or revision
   - format: square, wide, tall, mobile, desktop, or side-by-side board
   - variant strategy: one image, 2-3 separate images, or one comparison board
3. Build a prompt with:
   - purpose of the image
   - product context and target user
   - surface type, such as dashboard, onboarding, workspace, mobile screen, or landing view
   - desired feel in concrete words
   - composition and hierarchy
   - constraints and avoid list
4. Use image generation.
5. Inspect the result for quality and slop before presenting it.
6. In a project repo, copy the selected image into `docs/build/visuals/YYYY-MM-DD-<topic>-<purpose>.png` before presenting it. Leave the original `~/.codex/generated_images/` file in place.
7. Record the copied project-local path and the decision it clarified.

Read `references/prompt-patterns.md` before writing the image prompt.

## Actual Generation Protocol

For early visual exploration, "generate an image" means using the built-in `image_gen` tool.

1. Confirm the built-in image generation tool is actually available in this session. If it is not exposed, say: "Built-in image generation is not available in this Codex session." Then offer only these choices: start a session/surface with built-in imagegen, use API/CLI fallback with explicit approval, or switch to a coded mockup knowing it is not image generation.
2. Before calling `image_gen`, note the current time or newest PNG under `${CODEX_HOME:-$HOME/.codex}/generated_images/`.
3. Call the built-in `image_gen` tool directly with the final prompt.
4. Do not use Python, Pillow, HTML/CSS, SVG, canvas, screenshots, or local rendering as a substitute for image generation.
5. After the call, verify that the tool returned an image or that a newer PNG exists under `${CODEX_HOME:-$HOME/.codex}/generated_images/`.
6. If no image was returned and no newer file exists, say image generation failed. Do not claim success and do not create a fake replacement.
7. In a project repo, create `docs/build/visuals/` if needed and copy the selected generated PNG there before presenting the visual. Do not leave the final referenced artifact only under `.codex/generated_images/`.
8. Inspect the copied/generated image before presenting it. If it fails the rubric, retry once with a simpler, less text-heavy prompt.
9. If the retry also fails, stop and report the failure. API/CLI fallback requires explicit user approval. Coded mockups are only appropriate after the user chooses that fallback or when the workflow has moved into narrowed layout/interaction validation.

## Project Storage Rule

Prefer `docs/build/visuals/YYYY-MM-DD-<topic>-<purpose>.png` for generated brainstorming images.

- If the user names a different in-repo destination, use that destination.
- If there is no clear project repo or writable workspace, ask where to copy the image.
- If copying fails, report the generated source path and the copy failure. Do not present the `.codex` path as the durable project artifact.
- When showing the image in Codex Desktop, use the project-local absolute path in the Markdown image tag so the user sees the repo copy.

## Failure Handling

When image generation cannot complete, be exact about the failure mode:

- `image_gen` unavailable: the Codex session lacks the built-in tool.
- generation failed: the tool was available but did not return or save a usable image.
- artifact copied: a real generated image was copied into the project and should be referenced from the project-local path.
- coded mockup created: a deterministic local render was created, not an AI-generated image.

Do not phrase a coded mockup as "the image generator failed, so I generated an image another way." Say it was rendered locally and ask whether that fallback is acceptable.

## Taste Checks

Reject or revise outputs with:

- garbled text, tiny unreadable labels, fake paragraphs, or broken logos
- random icons, meaningless charts, impossible controls, or decorative dashboard noise
- default AI gloss: neon gradients, excessive glass, bokeh blobs, floating panels, or generic purple-blue SaaS haze
- inconsistent spacing, unclear hierarchy, illegible contrast, or cluttered composition
- people, hands, devices, 3D scenes, or cinematic backgrounds unless the user asked for them
- visuals that look like marketing art when the question is product structure

Prefer:

- product-specific surfaces and real workflow cues
- quiet hierarchy, clear grouping, and believable information density
- restrained but not one-note palettes
- concrete domain details over abstract decoration
- 2-3 meaningfully different directions instead of cosmetic variants

## UI Concept Rubric

Before showing a generated UI concept, check:

- instruction fit: it depicts the requested product surface and decision
- layout/hierarchy: primary actions or focal areas are obvious, secondary information is subordinate, related items are grouped
- legibility: any text is short, readable, spelled correctly, and not essential if it fails
- affordances: navigation, buttons, inputs, filters, charts, and cards look like plausible product UI
- slop severity: no distracting artifacts, random UI noise, decorative filler, or generic AI sheen

If a concept fails instruction fit or critical legibility, revise before presenting. If it is promising but flawed, present it only with the flaw called out.

## Source And Style Ethics

- Use references for layout, palette, composition, or mood only when the user provides or approves them.
- Do not imitate a specific living designer, brand, product, artwork, or copyrighted interface.
- Prefer generic, ownable visual directions over knockoffs.

## Presentation

When showing the image, say:

- what question it is answering
- what to look at
- what feels promising or suspect
- what decision or feedback you need from the user

Do not present a generated image as proof that the product is built.
