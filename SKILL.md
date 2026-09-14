---
name: staging-intake
description: Run a voice-first project-intake interview that turns an idea into a confirmed, structured PROJECT_INTAKE without planning, designing, selecting technology, or implementing.
metadata:
  short-description: Voice-only project intake before solutioning
---

# Staging Intake

Use this skill when a user has a project idea that must be clarified before any planner or implementation workflow begins.

## Hard boundary

The only successful output is a confirmed `PROJECT_INTAKE`. Do not plan, design a solution, choose a technology, decompose tasks, create a repository, write code, call a planner, or modify another engineering system. This skill is independent and must not connect to `ai-engineering-control`.

## Non-overridable gates

1. **Voice-only interview.** Text may activate the skill or provide post-interview formatting instructions, but formal interview answers must come from a verifiable voice session. If the host cannot verify that a response was spoken, pause and do not mark the interview complete.
2. **Interview before solution.** During the interview, collect evidence and resolve ambiguity only. Do not propose solutions, architecture, vendors, stacks, implementation plans, or tasks.
3. **One question at a time.** Ask the single highest-information-gain question available. Maintain explicit hypotheses, confidence, contradictions, and accepted unknowns; do not repeat resolved questions.
4. **Confirmation gate.** Before completion, check coverage, resolve blocking contradictions, target overall confidence near 0.95, read back the complete intake, and obtain explicit voice confirmation.

## Operating procedure

- Load [references/voice-policy.md](references/voice-policy.md) before starting or resuming an interview.
- Use the state machine and coverage rules in [references/interview-coverage.md](references/interview-coverage.md).
- Keep `reuse_first.required=true` and the exact `discovery_order` from [references/reuse-first-policy.md](references/reuse-first-policy.md) in every compiled output. This is discovery input for a future Planner, not work performed by this skill.
- Ask one question, record the spoken evidence, update the interview ledger, and choose the next missing or contradictory dimension.
- Treat typed answers during an active interview as non-evidence: pause and require voice to resume.
- When all gates pass, compile an object conforming to [schemas/project-intake.schema.json](schemas/project-intake.schema.json), then stop at `READY_FOR_HANDOFF`.

## Output contract

Return only the confirmed `PROJECT_INTAKE` plus minimal confirmation metadata. Never emit a plan, design, task list, implementation, or implied approval to proceed. If any gate fails, return the current paused state and the missing gate instead of a partial completion claim.

