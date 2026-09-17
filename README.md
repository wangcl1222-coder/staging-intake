# staging-intake

An independent Agent Skill for converting an early project idea into a user-confirmed `PROJECT_INTAKE` through a focused voice-or-text interview.

## Scope

This repository deliberately stops before planning or implementation. It does not integrate with `ai-engineering-control`, create tasks, choose technology, or change user projects. A future Planner may consume the confirmed intake and enforce its `reuse_first` discovery order.

## Layout

- `SKILL.md` — entrypoint and non-overridable workflow rules.
- `schemas/project-intake.schema.json` — JSON Schema for the handoff object.
- `references/voice-policy.md` — optional voice preference and cross-channel continuity rules.
- `references/interview-coverage.md` — state machine, ledger, question policy, and completion gates.
- `references/reuse-first-policy.md` — required future discovery order.
- `examples/simple-project.yaml` — readable example of a confirmed intake.
- `tests/scenarios.md` — behavioral acceptance scenarios.

## Source and mirror

Canonical source: `https://github.com/wangcl1222-coder/staging-intake`

The local Agent Skills mirror is installed at `~/.agents/skills/staging-intake/` when that path is available.
