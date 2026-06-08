---
name: handoff
description: Use when a build workflow session is ending, context is nearing the user's 40 percent budget, compaction feels likely, or a new session needs to resume. Writes a precise handoff with objective, phase, slice state, verification evidence, truth ledger, architecture map, open questions, and next action.
---

# Handoff

Preserve continuity before context gets crowded. A handoff is part of the build workflow, not an afterthought.

## When To Stop

At about 40 percent context use, enter clean-stop mode:

- stop starting new tasks
- finish only the smallest active verification step if it leaves a cleaner state
- do not add features
- do not refactor broadly
- do not fix adjacent issues unless required for the active verification step
- write a handoff before ending

## Resume Order

At the start of a resumed build workflow session, read:

1. latest `docs/build/handoffs/*.md`
2. product spec
3. `CONTEXT.md`
4. current slice contract
5. truth ledger
6. relevant source files only

Then restate current truth before continuing.

## Handoff Contents

Write handoffs to `docs/build/handoffs/YYYY-MM-DD-<phase>-slice-<n>.md` when a slice exists, or `docs/build/handoffs/YYYY-MM-DD-<phase>.md` before slicing.

Include:

- current objective
- current phase and slice number
- latest known working state
- verification evidence
- files changed
- commands run
- truth ledger summary: real / stubbed / not built / broken or unknown
- architecture map in plain English
- decisions made and ADRs written
- open questions
- exact next recommended action
- what the next session should read first

Use `references/handoff-template.md`.

## Quality Bar

A new agent should be able to read the handoff, inspect only the named artifacts, and continue without redoing the brainstorm.
