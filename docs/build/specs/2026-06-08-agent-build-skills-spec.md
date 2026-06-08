# Agent Build Skills Design

Date: 2026-06-08

## Purpose

Create a personal skillpack for building new software apps with AI coding agents while preserving user control, project clarity, and session continuity. The workflow should help the user move from fuzzy idea to spec, then from spec to thin verified vertical slices. It should prevent broad horizontal builds, fake-real demos, context-window drift, and automatic compaction without a handoff.

This design is for greenfield apps only for now.

## Design Principles

- Build for control, not raw speed.
- Vendor and adapt proven upstream skills where possible instead of reinventing their workflows or depending on their runtime availability.
- Keep every phase explicit: the agent should always know the current phase, artifact, and completion gate.
- Prefer thin vertical slices over broad horizontal layers.
- Treat verification evidence as stronger than narration.
- Treat context stewardship as part of the build process, not cleanup.
- Stop at specs and slice contracts, not full implementation plans.

## Skillpack Shape

The skillpack should use one orchestrator plus focused phase skills.

### orchestrator

Use this as the entrypoint for the build workflow. It should:

- detect the current project phase
- route to the correct workflow skill
- enforce greenfield-app scope
- enforce phase gates
- prevent implementation before a reviewed spec exists
- prevent full implementation-plan generation
- prevent broad horizontal work
- enforce context-budget and handoff rules

The orchestrator's main job is to stop drift.

### brainstorm

Use this to turn the user's rough product idea into a reviewed product spec.

This skill should vendor and adapt:

- Superpowers `brainstorming`
- Matt Pocock's `grill-with-docs`

It should reuse Superpowers' conversational design/spec discipline:

- explore context
- ask probing questions one at a time
- propose approaches with tradeoffs
- present design sections for approval
- write a spec
- self-review the spec
- ask the user to review the spec

It should reuse `grill-with-docs` for shared language and decision capture:

- maintain `CONTEXT.md`
- define domain terms in plain English
- sharpen fuzzy language
- create ADRs for meaningful hard-to-reverse decisions

Workflow-specific changes:

- Stop after the reviewed spec.
- Do not invoke Superpowers `writing-plans`.
- Require explicit stack choice during brainstorming.
- Require a truth boundary before implementation.
- Require a first vertical slice candidate.

### slice-plan

Use this after an approved spec. It should not create a full implementation plan.

It should create:

- a lightweight slice ladder for the product
- a detailed contract only for the next vertical slice

The slice ladder can outline likely future slices, but only the next slice should be detailed.

Each next-slice contract must include:

- user-visible flow
- real behavior that must work
- data/backend behavior, if relevant
- UI states needed for the slice
- tests or checks required
- browser/mobile verification required
- explicit non-goals
- fake/misleading behavior to avoid
- handoff notes to preserve

### build-slice

Use this to build exactly one vertical slice.

It should use relevant Superpowers discipline skills:

- `test-driven-development` before behavior changes or feature work
- `systematic-debugging` when tests fail or behavior is unclear
- `verification-before-completion` before claiming completion

Rules:

- Build only the current slice.
- Do not create broad horizontal layers unless the current slice needs them.
- Do not create fake production-looking features.
- Label any stub/mock/demo-only behavior visibly in the UI and in handoff docs.
- Maintain a truth ledger with `real`, `stubbed`, `not built`, and `broken/unknown`.
- Stop after verification instead of drifting into the next slice.

### verify-demo

Use this after a slice is built.

It should collect user-facing evidence:

- test command output summary
- browser screenshot or visual QA notes
- mobile viewport check
- local URL or file path
- phone-preview instructions when feasible
- optional screen recording when tool support exists
- plain-English "what you can try now"
- plain-English "what is not real yet"

Rule: verification evidence beats narration. A slice is not done because the UI looks plausible; it is done when the agreed checks pass and the truth ledger is clear.

### handoff

Use this whenever context pressure rises, a session is ending, or a new session needs to resume work.

This skill should be mandatory, not optional.

Each build workflow session should start by reading:

1. latest handoff doc, if present
2. product spec
3. `CONTEXT.md`
4. current slice contract
5. relevant source files only

At around 40 percent context usage, the agent enters clean-stop mode:

- stop starting new tasks
- finish only the smallest active verification step if that leaves a cleaner state
- do not add features
- do not refactor broadly
- do not fix adjacent issues unless required to complete the active verification step
- write a handoff before ending

The handoff must include:

- current objective
- phase and slice number
- latest known working state
- verification evidence
- files changed
- commands run
- truth ledger: real / stubbed / not built / broken or unknown
- architecture map in plain English
- decisions made and ADRs written
- open questions
- exact next recommended action
- what the next session should read first

For new sessions, the first move is not brainstorming again. It is: read the handoff, restate current truth, then continue the current phase or slice.

## Required Brainstorming Gates

The spec produced by `brainstorm` is not complete until it answers these gates.

### Product Clarity

- Who is the app for?
- What painful job does it do?
- What is the smallest real version worth building?

### Visible Loop

- What can the user see, click, submit, generate, inspect, or compare after the first slice?
- What proves the product is starting to work?

### Stack Choice

The agent must ask and lock:

- frontend
- backend
- database
- auth
- AI/provider choices, if any
- deployment target
- test stack
- local/mobile preview method

There is no default stack. The stack is chosen during brainstorming.

### Truth Boundary

The spec must say:

- what must be real
- what may be stubbed
- what is forbidden to fake
- how placeholders must be labeled
- how the user will know the difference

### Design Timing

The workflow should choose lightweight product/UI direction early enough to guide the first slice. Detailed UI polish should wait until real workflows exist.

### First Slice Candidate

The spec should end with a recommended first vertical slice and explain why it proves the product's core loop.

## Artifact Map

Recommended project artifacts:

- `CONTEXT.md` for shared language, domain glossary, and product assumptions
- `docs/build/specs/YYYY-MM-DD-<topic>-spec.md` for reviewed product specs
- `docs/adr/YYYY-MM-DD-<decision>.md` for meaningful architectural decisions
- `docs/build/slices.md` for the slice ladder
- `docs/build/current-slice.md` for the active next-slice contract
- `docs/build/truth-ledger.md` for real/stubbed/not-built/broken state
- `docs/build/handoffs/YYYY-MM-DD-<phase>-<slice>.md` for session handoffs
- `docs/build/upstream-attribution.md` or equivalent skillpack attribution file for copied/adapted upstream skill material

## Non-Goals

- Do not create a complete implementation plan after the spec.
- Do not optimize for autonomous multi-hour building without user checkpoints.
- Do not assume a default app stack.
- Do not support existing repos in the first version.
- Do not let polished UI imply backend/data behavior that is not real.
- Do not rely on automatic compaction as the normal continuity mechanism.

## Implementation Decisions For V1

- Vendor and adapt the upstream skills needed for the workflow instead of relying on their runtime availability. The workflow should keep working even if Superpowers, Matt Pocock's skills repo, or another agent's plugin system is unavailable.
- Copy only the useful skill instructions, prompts, and lightweight templates needed for this workflow. Do not copy entire plugin infrastructure unless a specific script or asset is required.
- Preserve required MIT license and copyright notices for copied or substantially adapted upstream material.
- Rewrite vendored upstream skills into workflow-specific versions rather than treating them as untouched copies. For example, remove Superpowers brainstorming's terminal transition to `writing-plans` and replace it with `slice-plan`.
- Repeat the short context-budget and handoff rule in every phase skill, even though `handoff` is a separate skill. This keeps the clean-stop behavior active under context pressure.
- Use Markdown references and templates for v1 instead of scripts. Add scripts later only if the same handoff or truth-ledger structure is being rewritten inconsistently.
- Build the skillpack as installable personal skills after confirming the target skills directory. The recommended target is the user's auto-discovered Codex skills directory, but the final location should be confirmed before scaffolding.
- Keep each skill agent-readable and agent-agnostic where possible, while still naming Codex/Superpowers behaviors explicitly when they are the intended upstream workflow.

## Acceptance Criteria

The implemented skillpack is acceptable when:

- A greenfield-app request triggers the orchestrator.
- Brainstorming produces a reviewed spec and does not continue into implementation planning.
- Stack choice is explicit in the spec.
- The first slice is vertical, visible, and verifiable.
- The build phase implements one slice only.
- Verification includes test evidence and browser/mobile evidence where applicable.
- Stubs/mocks/placeholders cannot be confused with real functionality.
- Context pressure causes a clean handoff instead of compaction drift.
- A fresh session can resume from the handoff without redoing the whole brainstorm.
