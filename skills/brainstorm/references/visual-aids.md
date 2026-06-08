# Visual Aids During Brainstorming

Use this reference only after the user accepts optional visual aids, or when the user explicitly asks for visual help.

## Core Rule

Visual means renderable or inspectable. Do not use ASCII diagrams, terminal box drawings, or pseudo-wireframes made from characters as the main visual artifact.

If the user explicitly asks for a visual explanation, producing only text with spacing, arrows, bracket labels, or dashed boxes is a failure. Create a renderable artifact instead.

Raw Mermaid is also a failure. If you are about to write `flowchart LR` or similar in plain text, stop and either wrap it in a fenced `mermaid` block or save it in a Markdown/HTML visual artifact.

## When To Use Visuals

Use a visual when the user would understand the suggestion better by seeing relationships, layout, or spatial differences:

- UI screens, navigation, layout, or workflow mockups
- side-by-side product or design options
- architecture, data flow, state machine, or entity relationship diagrams
- user journeys where sequence and branching matter
- tradeoffs that depend on visual hierarchy or information density

Stay text-only for:

- requirements and scope questions
- terminology clarification
- plain pros/cons
- stack choices that do not need a diagram
- any question where the answer is mostly words

## Format Choice

Choose the lightest format that will help.

1. Mermaid Markdown
   - Best for architecture, flows, state machines, entities, and journeys.
   - Show Mermaid in a fenced `mermaid` block so it renders where supported. Do not paste loose Mermaid syntax as plain text.
   - If the current surface is a terminal or transcript where Mermaid will not render, create a Markdown visual artifact at `docs/build/visuals/YYYY-MM-DD-<topic>-<purpose>.md` with a short title, the decision question, and the fenced Mermaid block. Link that file instead of relying on terminal output.
   - Use one diagram by default. Create multiple diagrams only when each answers a separately named decision question.
   - Keep diagrams small enough to inspect quickly: usually 5-9 meaningful nodes, grouped with `subgraph` only when grouping reduces confusion.
   - Use clear node labels and avoid decorative complexity. Quote labels that contain punctuation or long phrases.
   - If a Mermaid diagram affects the spec or a durable product decision, save it in a Markdown visual artifact and record that path in the spec.

2. Generated bitmap image
   - Best early in brainstorming, while the product direction is still wide open.
   - Use for creative UI exploration: visual style, mood, screen concepts, product surface feel, and divergent side-by-side directions.
   - Use `visual-concept` when available so the prompt is tasteful, specific, and checked for AI-sloppy output.
   - Use the built-in `image_gen` tool when it is available. If it is not available in the current Codex surface, say so plainly and ask before using API/CLI fallback or a coded mockup.
   - Keep it conceptual. The output is for product/design understanding, not production UI code.
   - Built-in image generation may save under `~/.codex/generated_images/` by default. In a project repo, copy the selected image into `docs/build/visuals/YYYY-MM-DD-<topic>-<purpose>.png` before presenting it as the usable artifact. Leave the original in place as the source copy.
   - Record the project-local copied path in the spec under Visual Aids Used.

3. Static HTML/CSS mockup
   - Best after the direction narrows and the user needs to inspect concrete layout, interaction flow, information density, responsive behavior, or screen-to-screen structure.
   - Also useful when an information-architecture decision needs a more visual canvas than Mermaid: navigation zones, task detail anatomy, split-pane relationships, tabs, filters, and screen-to-screen entry points.
   - Prefer this for "task detail page", "where does drafting live?", "what does this workspace look like?", and other product-surface anatomy questions where boxes/panels/tabs would otherwise be drawn in ASCII.
   - This is a coded/local render, not image generation. Do not use it as a silent fallback for failed or unavailable `image_gen`.
   - Save coded mockups to `docs/build/visuals/YYYY-MM-DD-<topic>-<purpose>.html` when they should persist.
   - Keep them as brainstorming artifacts. Do not scaffold the app, wire real data, or create production UI code during brainstorming.

## Choosing Mermaid vs HTML vs Image

- Use Mermaid when the decision is about ownership, sequence, lifecycle, data flow, or dependency relationships.
- Use a Markdown visual artifact when Mermaid is the right format but the user needs to actually view or revisit it.
- Use static HTML/CSS when the decision depends on screen layout, information density, navigation, or "where does this live in the product?"
- Use generated images when the decision is about broad visual direction, product feel, mood, or divergent UI concepts.
- Do not use generated images to make architecture or data ownership look prettier; they are likely to blur the truth.
- If the answer would otherwise be a fake terminal wireframe, choose HTML instead.

## UI Mockup Progression

For UI work, prefer this sequence:

1. Explore with generated images when the user is still choosing product feel, visual direction, or broad screen concepts.
2. Narrow the direction through discussion and feedback.
3. Switch to coded mockups when the question becomes concrete: "Does this layout work?", "Can I follow the flow?", "Is the dashboard too dense?", or "How does this behave on mobile?"

Do not jump to coded mockups too early. Do not keep generating images once the user is trying to validate real layout and interaction details.

## How To Present A Visual

For each visual:

- State what decision or question it is meant to clarify.
- Show or link the artifact. If the artifact was saved in the repo, provide the project-local path.
- Ask for feedback on that one visual decision before moving on.
- Capture the decision, artifact path, or deferred question in the spec.

Avoid creating multiple visuals in a row without the user's feedback.

## Mermaid Quality Bar

Before presenting a Mermaid visual, check:

- It answers one explicit question, such as "Are drafts children of tasks or a separate workspace?"
- It is visually simpler than the text it replaces.
- It uses the correct diagram type: `flowchart` for workflows, `stateDiagram-v2` for lifecycle, `sequenceDiagram` for request or collaboration flow, and `erDiagram` for data ownership.
- It has no duplicate explanation split across two diagrams unless the diagrams compare alternatives.
- It is followed by one plain-English recommendation or question, not a long repeat of every node.
