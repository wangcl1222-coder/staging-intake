# Interview coverage and control loop

## State machine

`IDLE → INTAKE_REQUESTED → MODE_SELECTED → INPUT_MODE_READY → INTERVIEW_ACTIVE → COVERAGE_CHECK → CONFIRMATION_REQUIRED → INTERVIEW_CONFIRMED → INTAKE_COMPILED → READY_FOR_HANDOFF`

For `REINTAKE`, insert `BASELINE_INGESTED → BASELINE_VALIDATED` between `INPUT_MODE_READY` and `INTERVIEW_ACTIVE`. Baseline validation means that material freshness, contradictions, and source limitations have been identified; it does not require every baseline statement to be independently verified.

Voice and text are both valid input modes, and switching channels keeps the flow in `INTERVIEW_ACTIVE`. Missing coverage or a blocking contradiction returns to `INTERVIEW_ACTIVE`. There are no planning, design, implementation, or task states.

## Ledger

Maintain these fields during the interview:

- `facts`: directly user-provided answers, with channel/source recorded when available.
- `hypotheses`: interpretations, each with confidence and a falsification question.
- `contradictions`: unresolved conflicts; blocking until resolved or explicitly accepted as unknown.
- `accepted_unknowns`: unknowns the user consciously accepts for later discovery.
- `asked_questions`: normalized questions already answered; do not repeat them.
- `coverage`: problem, users, desired outcome, scope, constraints, non-goals, success signal, risks, and unknowns.
- `intake_mode`: `GREENFIELD` or `REINTAKE`.
- For `REINTAKE`, `baseline_sources`, `baseline_facts`, `baseline_freshness`, `fixed_elements`, `revisitable_elements`, and `reassessment_trigger`.

## Question selection

Ask exactly one short question at a time. Select the question that most reduces uncertainty among missing coverage and blocking contradictions. Prefer questions that distinguish between competing hypotheses. Do not ask for solutions or technology. A question is resolved when the user's voice or text answer is specific enough to update the ledger.

For `REINTAKE`, reliable baseline evidence counts as an answered question. Prioritize changed intent, baseline conflicts, fixed-versus-revisitable boundaries, and success from the current stage forward. Do not replay the greenfield questionnaire against facts already established by the baseline.

## Completion gates

Before readback: every coverage dimension is present, no blocking contradiction remains, every non-accepted unknown has an owner or follow-up condition, and overall confidence is at least 0.95 (or the user explicitly accepts the remaining bounded unknowns). For `REINTAKE`, also confirm the current-state baseline, reassessment trigger, fixed elements, revisitable elements, and revised or reaffirmed success criteria. Then read back the complete solution-neutral intake and request explicit confirmation in the active channel. Either a clear voice confirmation or a clear typed confirmation permits compilation.
