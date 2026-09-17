---
name: staging-intake
description: Run a voice-first project-intake interview that turns an idea into a confirmed canonical PROJECT_INTAKE_V1 without planning, designing, selecting technology, or implementing.
metadata:
  short-description: Voice-only project intake before solutioning
---

# Staging Intake

Use this skill when a user has a project idea that must be clarified before any planner or implementation workflow begins.

## Hard boundary

The only successful output is a confirmed canonical `PROJECT_INTAKE_V1`. Do not plan, design a solution, choose a technology, decompose tasks, create a repository, write code, call a planner, or modify another engineering system. This skill remains independent of `ai-engineering-control`; it only emits a document that can later be consumed by AI Engineering.

## Non-overridable gates

1. **Voice-only interview.** Text may activate the skill or provide post-interview formatting instructions, but formal interview answers must come from a verifiable voice session. If the host cannot verify that a response was spoken, pause and do not mark the interview complete.
2. **Interview before solution.** During the interview, collect evidence and resolve ambiguity only. Do not propose solutions, architecture, vendors, stacks, implementation plans, or tasks.
3. **One question at a time.** Ask the single highest-information-gain question available. Maintain explicit hypotheses, confidence, contradictions, and accepted unknowns; do not repeat resolved questions.
4. **Confirmation gate.** Before completion, check coverage, resolve blocking contradictions, target overall confidence near 0.95, read back the complete intake, and obtain explicit voice confirmation.

## Operating procedure

- Load [references/voice-policy.md](references/voice-policy.md) before starting or resuming an interview.
- Use the state machine and coverage rules in [references/interview-coverage.md](references/interview-coverage.md).
- Keep `reuse_first.required=true` and the discovery order from [references/reuse-first-policy.md](references/reuse-first-policy.md) in the internal interview ledger. These are interview/process controls, not fields in the final canonical output.
- Ask one question, record the spoken evidence, update the interview ledger, and choose the next missing or contradictory dimension.
- Treat typed answers during an active interview as non-evidence: pause and require voice to resume.
- When all gates pass, compile an object conforming to [schemas/project-intake.schema.json](schemas/project-intake.schema.json).
- Set `contract_version` to `PROJECT_INTAKE_V1` and `source_mode` to `interview_skill`.
- Put confirmed scope into `scope.in_scope` and confirmed exclusions into `scope.out_of_scope`.
- Put explicit unresolved items into `unknowns`; never invent missing facts.
- Put any unresolved approval requirement into `human_gates`.
- Use `intake_status: READY_FOR_HANDOFF` only after the voice confirmation gate passes. Otherwise use `NEEDS_MORE_INFORMATION`.
- Stop after emitting the canonical object. Do not create `PROJECT_START_V1`, TASK/RWO state, repositories, worker routes, or implementation plans.

## Output contract

Return only the confirmed canonical `PROJECT_INTAKE_V1` object. Voice verification, confidence, hypotheses, contradictions, reuse-first tracking, and readback confirmation remain internal interview evidence and are not extra top-level fields in the final object. If any gate fails, return the paused interview state and missing gate instead of claiming `READY_FOR_HANDOFF`.
