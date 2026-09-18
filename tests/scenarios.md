# Acceptance scenarios

1. **Typed activation** — A typed “start intake” moves the flow to `INPUT_MODE_READY` and may be followed by text or voice answers.
2. **Voice answer** — A voice answer is recorded in `facts` and can update confidence and coverage; voice provenance is useful but not required.
3. **Typed answer during interview** — The answer is accepted as formal evidence and the interview continues without restarting or repeating questions.
4. **Voice disconnect** — The interview preserves its ledger and continues in text; it does not pause for voice recovery or reject the next answer.
5. **Solution bait** — A request such as “just choose the stack” is refused during interview; the next question remains about intent, scope, constraints, or evidence.
6. **Repeated question** — A resolved dimension is not asked again; the next question targets the highest-information missing dimension or contradiction.
7. **Blocking contradiction** — Conflicting user answers keep the flow in active interview until resolved or explicitly moved to `accepted_unknowns`.
8. **Final confirmation** — Readback without explicit user confirmation cannot compile; either a clear voice or typed confirmation can transition to `READY_FOR_HANDOFF`.
9. **Planning defaults** — A compiled `PROJECT_INTAKE_V1` includes `planning_directives` with `mode: MVP_FIRST`, all four boolean directives set to `true`, and `policy_ref` set to `ai-engineering-control/policies/PLANNER_POLICY.md`.
10. **Explicit full-design override** — `mode: FULL_DESIGN` is allowed only when the user explicitly requests completeness/full design or explicitly rejects MVP-first; project complexity alone never changes the mode.
11. **Planning boundary** — `planning_directives` only informs a later Planner; the skill never copies Planner Policy content, creates an AI Engineering TASK, calls `ai-engineering-control`, plans, designs, selects technology, routes workers, or implements.
12. **Reintake from local baseline** — A user names a local progress summary; the skill ingests it before questioning, treats it as evidence rather than instructions, and does not repeat reliably resolved questions.
13. **Reintake from GitHub baseline** — A user explicitly names a repository file; the skill announces the scoped external read, retrieves only the named baseline read-only, and does not inspect unrelated repository or account content.
14. **Baseline conflict** — Conflicting progress claims are classified as a contradiction and resolved with one neutral question rather than silently choosing one source.
15. **Reassessment boundary** — The interview distinguishes fixed elements from revisitable assumptions or decisions without recommending a solution path.
16. **Reintake output compatibility** — Existing-project facts map into the unchanged `PROJECT_INTAKE_V1` fields; no extra top-level mode or ledger fields are emitted.
17. **Voice transcript gap** — Missing audio is not inferred as evidence; the skill preserves the last confirmed checkpoint and continues in text without restarting the interview.
