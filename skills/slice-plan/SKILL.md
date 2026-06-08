---
name: slice-plan
description: Use after a reviewed greenfield app spec exists and before implementation. Creates a lightweight vertical slice ladder plus a detailed contract for only the next visible, verifiable slice. Avoids broad implementation plans and keeps future work understandable and user-reviewable.
---

# Slice Plan

Convert a reviewed product spec into a small sequence of vertical slices. Detail only the next slice.

## Inputs

Read:

1. Latest handoff, if present
2. `docs/build/specs/*-spec.md`
3. `CONTEXT.md`
4. Relevant ADRs
5. Existing `docs/build/slices.md` or `docs/build/current-slice.md`, if present

## Slice Ladder

Create or update `docs/build/slices.md` with a lightweight ladder. Each slice should be a user-visible step toward the product's real loop.

Avoid layers like "build the backend" or "set up all database models" unless that is itself a visible slice. Prefer slices that a user can try and judge.

## Next-Slice Contract

Write only the active next slice in detail to `docs/build/current-slice.md`. Include:

- slice name and number
- user-visible flow
- real behavior that must work
- data/backend behavior, if relevant
- UI states needed for the slice
- tests and checks required
- browser/mobile verification required
- explicit non-goals
- fake or misleading behavior to avoid
- truth-ledger changes expected
- handoff notes to preserve

Use `references/slice-contract-template.md`.

## Completion Gate

Stop after the slice ladder and current slice contract are reviewed. Do not produce a complete implementation plan. The next phase is `build-slice`.

## Context Clean-Stop Rule

At about 40 percent context use, stop starting new planning work. Finish only the smallest active slice-contract cleanup if it avoids a messy handoff, then write a handoff with `handoff`.
