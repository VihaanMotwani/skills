---
name: brainstorm
description: >-
  Use when turning a greenfield app idea into a reviewed product spec for the user's build workflow.
  Vendors and adapts Superpowers brainstorming plus grill-with-docs: probes the user one question at a
  time, maintains CONTEXT.md as a glossary, writes sparse ADRs, forces explicit stack and truth-boundary
  choices, and stops after the spec without creating an implementation plan. Visual aids must be renderable
  artifacts such as fenced Mermaid, Markdown/HTML files, or generated images; never ASCII diagrams or raw Mermaid.
---

# Brainstorm

Turn a rough app idea into a reviewed product spec. Do not implement. Do not write a full implementation plan.

This skill vendors and adapts Superpowers `brainstorming` and Matt Pocock's `grill-with-docs`. See `references/upstream-attribution.md`.

## Required Flow

1. Explore the empty or new project context: files, docs, existing handoff, and current workspace state.
2. If UI, layout, flow, architecture, or visual tradeoffs are likely, offer optional visual aids once. Use the Visual Aid Protocol below. If visual aids are accepted, read `references/visual-aids.md` before producing the first visual.
3. Interview the user one question at a time until the product, user, painful job, non-goals, and visible first loop are clear.
4. Maintain `CONTEXT.md` as a glossary only. Create or update it as terms are resolved.
5. Offer ADRs sparingly only for decisions that are hard to reverse, surprising without context, and real tradeoffs.
6. Propose 2-3 approaches with tradeoffs and a recommendation.
7. Present the design in sections and ask for approval after each section.
8. Write the reviewed spec to `docs/build/specs/YYYY-MM-DD-<topic>-spec.md`.
9. Self-review the spec for placeholders, contradictions, ambiguity, and scope drift.
10. Ask the user to review the written spec.
11. Stop. The next phase is `slice-plan`, not an implementation plan.

## Required Spec Gates

The spec is incomplete until it covers:

- product clarity: user, painful job, smallest real version
- visible loop: what can be seen, clicked, submitted, generated, inspected, or compared
- explicit stack choice: frontend, backend, database, auth, AI/provider, deployment, tests, local/mobile preview
- truth boundary: real, stubbed, forbidden to fake, placeholder labeling
- lightweight UI/product direction
- recommended first vertical slice

Use `references/spec-template.md` when writing the spec. Use `references/context-format.md` and `references/adr-format.md` when creating supporting docs.

## Visual Aid Protocol

Visual aids are optional because they can consume extra tokens and time.

If upcoming discussion would be easier to understand by seeing it, offer visual aids once in a short standalone message before asking the next clarifying question:

> Some of this may be easier to understand visually. I can create optional diagrams, image-generated explorations, or coded UI mockups when seeing beats reading. This can take extra tokens/time. Want visual aids for moments where they would genuinely help?

If the user declines, continue text-only unless they ask again. If the user asks for visual help, treat that as consent for the current brainstorming session.

Decide per question. Use visuals for UI mockups, layout comparisons, architecture diagrams, data flow, state machines, user journeys, or spatial tradeoffs. Use text for requirements, scope, conceptual choices, tradeoff lists, and terminology.

Hard rule for visual requests: if the user asks "explain visually", "show visually", "draw this", "diagram this", or similar, do not answer with indented arrows, dashed boxes, bracketed pseudo-panels, terminal wireframes, or text arranged to look visual. Read `references/visual-aids.md` first and create one of the approved artifacts below.

If the response contains Mermaid keywords such as `flowchart`, `graph`, `sequenceDiagram`, `stateDiagram-v2`, or `erDiagram`, they must be inside a fenced `mermaid` block or inside a saved Markdown/HTML artifact. Plain Mermaid syntax in chat is invalid.

If the current surface will not render Mermaid inline, do not rely on inline Mermaid. Save a Markdown visual artifact or static HTML artifact under `docs/build/visuals/` and link the project-local path.

Do not use ASCII art or terminal box diagrams as the visual aid. Use a renderable or inspectable artifact instead:

- Mermaid Markdown for flows, architecture, state machines, and entity relationships. Mermaid must be emitted as a fenced `mermaid` block in chat or saved in a Markdown visual artifact, not as loose text.
- Image generation for early creative UI exploration: visual style, product feel, rough screen concepts, and divergent side-by-side directions.
- Lightweight coded mockups for narrowed UI decisions: layout, interaction flow, information density, responsive behavior, and screen-to-screen structure.

If image generation is requested but the built-in `image_gen` tool is unavailable, say so directly. Do not silently switch to API/CLI image generation or coded/local rendering. Ask before changing paths, and label coded mockups as coded mockups.

Keep each visual attached to one decision or question. Summarize what the user is looking at, ask for feedback, and record any visual artifacts or decisions in the spec. Read `references/visual-aids.md` before creating a visual artifact.

## Question Style

Ask one question per message. Prefer multiple choice when it helps the user answer quickly. If a question can be answered by inspecting files, inspect files instead of asking.

Challenge fuzzy terms immediately. Example: "When you say account, do you mean the customer organization or the individual user?"

## Context Clean-Stop Rule

At about 40 percent context use, stop starting new work. Finish only the smallest active spec-review step if it avoids a messy handoff, then write a handoff with `handoff`.
