---
name: verify-demo
description: Use after a vertical slice has been built to gather proof for the user. Produces test evidence, browser or visual checks, mobile viewport notes, local preview instructions, and a plain-English real/stubbed/not-built summary before any completion claim.
---

# Verify Demo

Collect evidence that the current slice works. Verification evidence beats narration.

This skill adapts Superpowers verification-before-completion ideas. See `references/upstream-attribution.md`.

## Inputs

Read:

1. `docs/build/current-slice.md`
2. `docs/build/truth-ledger.md`
3. Latest handoff, if present
4. Relevant test, app, and UI files

## Verification Evidence

Collect the evidence the current slice contract requires:

- automated test command and result
- manual check steps and result
- browser screenshot or visual QA notes when UI exists
- mobile viewport check when UI exists
- local URL or file path
- phone-preview instructions when feasible
- screen recording only when the environment supports it and it is useful

If a required check cannot be run, say why and mark the residual risk.

## User-Facing Summary

Write a concise verification note with:

- what the user can try now
- what works
- what is stubbed
- what is not built
- what is broken/unknown
- commands run
- evidence locations
- next recommended action

Use `references/verification-note-template.md` if writing to a file.

## Completion Gate

Only say the slice is complete when the required evidence exists and the truth ledger is clear. If evidence is missing, say the slice is partially verified.

## Context Clean-Stop Rule

At about 40 percent context use, stop starting new verification branches. Finish only the smallest active check if it leaves a cleaner handoff, then write a handoff with `handoff`.
