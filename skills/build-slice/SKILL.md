---
name: build-slice
description: Use when implementing exactly one approved vertical slice in a greenfield app. Applies TDD, systematic debugging, truth-ledger discipline, and one-slice scope control so the agent builds real behavior without drifting into broad layers or fake production-looking features.
---

# Build Slice

Build exactly one approved vertical slice. Stop after verification. Do not move to the next slice.

This skill vendors and adapts Superpowers test-driven-development, systematic-debugging, and verification-before-completion ideas. See `references/upstream-attribution.md`.

## Inputs

Read:

1. Latest handoff, if present
2. Product spec
3. `CONTEXT.md`
4. Relevant ADRs
5. `docs/build/current-slice.md`
6. `docs/build/truth-ledger.md`, if present

## Scope Rules

- Implement only the current slice contract.
- Do not create broad backend, database, auth, or UI layers beyond what the slice needs.
- Do not add nice-to-haves.
- Do not make fake production-looking features.
- Any stub, mock, fixture, demo-only value, or not-yet-wired feature must be visibly labeled in the UI when user-facing and recorded in the truth ledger.

## TDD Loop

Before behavior changes:

1. Define the smallest test/check that proves the slice behavior.
2. Watch it fail or explain why no automated test is possible yet.
3. Implement the smallest code needed.
4. Run the test/check.
5. Refactor only when the behavior is green and the refactor is inside slice scope.

## Debugging Loop

When behavior is unclear or tests fail:

1. Reproduce the failure.
2. Inspect evidence before guessing.
3. Form one hypothesis.
4. Test the hypothesis with the smallest observation or command.
5. Fix the root cause, not a symptom.
6. Re-run the relevant check.

## Truth Ledger

Create or update `docs/build/truth-ledger.md` using `references/truth-ledger-template.md`.

Every slice must classify product behavior as:

- real
- stubbed
- not built
- broken/unknown

## Completion Gate

The slice is not complete until:

- agreed tests/checks pass or failures are documented
- user-visible behavior is verified where applicable
- truth ledger is updated
- changed files and commands are known
- `verify-demo` can collect evidence

## Context Clean-Stop Rule

At about 40 percent context use, stop starting new implementation work. Finish only the smallest active verification step if it leaves a cleaner state, then write a handoff with `handoff`.
