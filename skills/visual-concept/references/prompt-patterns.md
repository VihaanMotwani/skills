# Prompt Patterns

Use these patterns to prepare image-generation prompts. Keep prompts specific, but not overstuffed.

## Prompt Principles

- Keep the first prompt concise: purpose, product context, surface, visual direction, constraints.
- Prefer concrete words over vague polish words. Say what should be visible.
- For text, use only short large labels, quoted exactly. Avoid dense UI copy.
- For revisions, change one thing at a time and repeat what must stay fixed.
- Use references only for broad traits the user owns or approves: layout, palette, composition, mood.
- For UI mockups, describe the product as if it already exists. Focus on layout, hierarchy, spacing, and recognizable interface elements. Avoid concept-art language unless the user is explicitly exploring mood.
- If comparing directions, use one comparison board only when side-by-side comparison matters. Use separate image calls when each direction needs enough fidelity to inspect.

## Product UI Direction

```text
Create an exploratory product UI concept image for <product/context>.
Purpose: <what the image should help decide>.
Audience: <user>.
Surface: <dashboard/workspace/mobile screen/onboarding/landing view>.
Decision to clarify: <what the user is choosing>.
Visual direction: <concrete feel, not vague adjectives>.
Composition: clear hierarchy, believable product interface, readable large labels only, no tiny body text.
Domain cues: <2-4 concrete elements that belong in this product>.
Avoid: garbled text, fake paragraphs, random icons, meaningless charts, glossy AI look, neon gradients, excessive glass, bokeh blobs, floating 3D panels, specific brand imitation, device mockups unless requested.
Output should feel like a practical product interface direction for brainstorming, not concept art, a finished screenshot, or a marketing poster.
```

## Side-By-Side Directions

```text
Create one image with <2 or 3> side-by-side product UI concept directions for <product/context>.
Each direction should have a clearly different information architecture and mood.
Use large simple labels for the direction names only: <labels>.
No small text, no fake paragraphs, no decorative filler.
Make the differences easy to compare: layout, density, hierarchy, navigation, and workflow emphasis.
Keep the image clean, modern, and product-specific.
Avoid generic AI SaaS aesthetics, neon gradients, excessive glass, bokeh, random icons, meaningless charts, and brand knockoffs.
```

## Mood And Surface

```text
Create a mood-focused product surface concept for <product/context>.
Show the product's visual personality through layout, spacing, color, and information hierarchy.
No exact UI copy except 1-3 large readable labels if needed.
Use concrete domain details: <details>.
Avoid stock imagery, cinematic backgrounds, fake screenshots, unreadable text, brand imitation, and generic AI gloss.
```

## UI Concept Quality Check

```text
Before presenting, inspect the image:
- Does it match the requested surface and product context?
- Is the hierarchy understandable at a glance?
- Are the labels readable and nonessential if imperfect?
- Do controls look clickable/editable and navigation look like navigation?
- Is there any AI slop: garbled text, random icons, meaningless charts, clutter, excessive glass, generic purple-blue haze?
If the answer is no on surface match or critical legibility, revise before showing it.
```

## Revision Prompt

```text
Revise the previous concept with these changes:
- Keep: <what worked>.
- Change: <specific issue>.
- Remove: <AI slop or wrong detail>.
- Preserve the same product context and decision goal.
```
