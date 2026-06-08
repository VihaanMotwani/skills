---
name: orchestrator
description: Use when starting or resuming a greenfield software app build through the user's build workflow. Routes the agent through brainstorming, spec writing, vertical slice planning, one-slice implementation, verification, and handoff while preventing broad horizontal work, fake-real features, missing specs, and context-window drift.
---

# Orchestrator

Coordinate a greenfield app build without letting the agent drift. Always identify the current phase, required artifact, and completion gate before doing work.

## Hard Limits

- Use this workflow for new apps only. If the user asks for an existing repo, say v1 is greenfield-only and ask whether to proceed outside the workflow.
- Do not implement before a reviewed product spec exists.
- Do not write a complete implementation plan after the spec.
- Do not build broad horizontal layers when a vertical slice would do.
- Do not let polished UI imply behavior that is not real.
- Do not rely on compaction for continuity. Use clean handoffs.

## Phase Router

Start every build workflow turn by checking for these artifacts:

1. Latest `docs/build/handoffs/*.md`
2. `docs/build/specs/*-spec.md`
3. `CONTEXT.md`
4. `docs/build/current-slice.md`
5. `docs/build/truth-ledger.md`

Then route:

- No reviewed spec: use `brainstorm`.
- Reviewed spec but no next-slice contract: use `slice-plan`.
- Current slice contract exists and slice is not built: use `build-slice`.
- Slice is built but evidence is missing: use `verify-demo`.
- Context is crowded, the user asks to pause, or the session is ending: use `handoff`.

If the user explicitly asks for a phase skill, use that skill directly.

## Context Clean-Stop Rule

At about 40 percent context use, or when the session feels crowded enough that compaction is plausible, stop starting new work. Finish only the smallest active verification step if it leaves a cleaner state, then write a handoff. Do not add adjacent features or broad refactors.

## Output Discipline

Keep the user oriented with:

- current phase
- active artifact
- what changed
- what is verified
- what is real, stubbed, not built, or unknown
- next recommended action

When unsure, choose the smaller slice and the clearer handoff.
