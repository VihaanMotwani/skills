# Skills For Human-Led App Builds

Agent skills for building new apps without losing control of the project.

Most agent workflows are either too vague or too ambitious. The agent chats for a while, then disappears into a giant backend pass, a giant UI pass, or a giant "I built the whole thing" pass. By the time it comes back, you have a lot of code, a shaky demo, and no clean sense of what actually works.

These skills are for a different rhythm: clarify the idea, write a real spec, choose one thin vertical slice, build only that slice, verify it, and hand off before the context window gets messy.

They are small, composable, and meant to be adapted. Use them as a starting point for your own agent build workflow.

## Quickstart

Install the skills with `skills.sh`:

```bash
npx skills@latest add VihaanMotwani/skills
```

Install all of them for Codex:

```bash
npx skills@latest add VihaanMotwani/skills --skill '*' -a codex -g --copy -y
```

Use another supported agent by replacing `codex`, for example:

```bash
npx skills@latest add VihaanMotwani/skills --skill '*' -a claude-code -g --copy -y
```

Then start a fresh agent session and invoke the orchestrator:

```text
Use $orchestrator to help me build a new app idea.
```

You can also install or inspect individual skills:

```bash
npx skills@latest add VihaanMotwani/skills --list
npx skills@latest add VihaanMotwani/skills --skill brainstorm
```

## Why These Skills Exist

I made these skills to fix the failure modes I keep running into when building new apps with coding agents.

### #1: The Agent Did Not Understand The Product

The Problem: You give the agent a rough idea. It nods, sounds confident, and starts coding. Then the first demo reveals that you and the agent were imagining different users, different workflows, and different success criteria.

The Fix: Start with `$brainstorm`.

`$brainstorm` keeps asking questions until the product, user, first visible loop, stack choice, truth boundary, and first slice are clear. It writes a reviewed spec and then stops. It does not turn the spec into an implementation plan.

### #2: The Agent Built Too Much At Once

The Problem: Agents like broad horizontal work. They build the database, then the backend, then the frontend, then maybe the demo. That can look productive, but it makes the project hard to follow and hard to correct.

The Fix: Use `$slice-plan`.

`$slice-plan` creates a lightweight slice ladder, then details only the next vertical slice. The goal is always one visible, testable increment that you can understand before moving on.

### #3: The Demo Looked Real But Was Fake

The Problem: Agents are very good at making mocked behavior look finished. Buttons appear to work, dashboards fill with data, flows "complete", and only later do you discover that the important parts were fixtures, stubs, or optimistic UI.

The Fix: Use `$build-slice` and `$verify-demo`.

`$build-slice` keeps implementation scoped to one approved slice and requires real behavior to be labeled honestly. `$verify-demo` collects proof before completion: tests, browser checks, mobile viewport notes, local preview details, and a plain-English truth summary of what is real, stubbed, broken, or not built.

### #4: The Context Window Ate The Project

The Problem: Long sessions drift. The agent forgets why decisions were made, compaction loses nuance, and the next session starts by re-discovering the project from scraps.

The Fix: Use `$handoff`.

`$handoff` writes a continuation document before the session gets crowded. It captures the objective, current phase, slice state, verification evidence, truth ledger, architecture notes, and next command sequence so a new session can resume cleanly.

### #5: The Human Lost The Steering Wheel

The Problem: A tool that can build fast can also make you feel behind your own project. Once you stop understanding the architecture and current product state, every future change becomes harder to judge.

The Fix: Use `$orchestrator`.

`$orchestrator` routes the build through the right phase: brainstorm, spec, slice planning, one-slice implementation, verification, or handoff. It is designed to keep the human in the loop and prevent broad, unsupervised implementation runs.

## Reference

### Build Workflow

Skills for taking a new app from idea to verified vertical slices.

- [`orchestrator`](skills/orchestrator) - Routes a greenfield app build through brainstorming, spec writing, slice planning, one-slice implementation, verification, and handoff.
- [`brainstorm`](skills/brainstorm) - Turns a rough idea into a reviewed product spec through a probing conversation.
- [`visual-concept`](skills/visual-concept) - Creates tasteful image-generated product visuals, copies repo-bound outputs into `docs/build/visuals`, and refuses silent coded-PNG substitutes.
- [`slice-plan`](skills/slice-plan) - Creates a lightweight vertical slice ladder and a detailed contract for only the next slice.
- [`build-slice`](skills/build-slice) - Implements exactly one approved vertical slice with TDD, debugging discipline, and truth-ledger updates.
- [`verify-demo`](skills/verify-demo) - Gathers evidence that the slice actually works and separates real behavior from stubs or missing work.
- [`handoff`](skills/handoff) - Writes a precise handoff before context drift, compaction, or session transfer.

### Project Artifacts

These skills create or maintain a small set of durable files inside the app project being built:

- `CONTEXT.md` - Shared product language and glossary.
- `docs/build/specs/*-spec.md` - Reviewed product specs.
- `docs/adr/*.md` - Meaningful hard-to-reverse decisions.
- `docs/build/slices.md` - Lightweight slice ladder.
- `docs/build/current-slice.md` - The active slice contract.
- `docs/build/truth-ledger.md` - Real / stubbed / not built / broken state.
- `docs/build/handoffs/*.md` - Session handoffs for continuation.

### Operating Rules

- New apps only for now.
- Choose the stack during brainstorming.
- Stop after the spec; do not generate a full implementation plan.
- Build thin vertical slices, not broad layers.
- Label stubs, mocks, fixtures, and demo-only behavior clearly.
- Treat verification evidence as stronger than confident narration.
- Keep context under control with explicit handoffs instead of relying on compaction.

## Credits

This repo vendors and adapts ideas from:

- Superpowers skills by Jesse Vincent
- Matt Pocock's skills, especially `grill-with-docs`

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for license notices.
