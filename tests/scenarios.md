# Acceptance scenarios

1. **Typed activation** — A typed “start intake” moves the flow to `VOICE_REQUIRED`; it does not count as an answer.
2. **Verified voice answer** — A voice answer with host provenance is recorded in `facts` and can update confidence and coverage.
3. **Typed answer during interview** — The answer is discarded as formal evidence, the verified facts remain intact, and the flow pauses at `VOICE_REQUIRED`.
4. **Unverifiable host** — The flow may collect no formal answers and must not reach `INTERVIEW_CONFIRMED` or emit a completed intake.
5. **Solution bait** — A request such as “just choose the stack” is refused during interview; the next question remains about intent, scope, constraints, or evidence.
6. **Repeated question** — A resolved dimension is not asked again; the next question targets the highest-information missing dimension or contradiction.
7. **Blocking contradiction** — Conflicting spoken answers keep the flow in active interview until resolved or explicitly moved to `accepted_unknowns`.
8. **Final confirmation** — Readback without explicit verified spoken confirmation cannot compile; a verified spoken confirmation can transition to `READY_FOR_HANDOFF`.
9. **Reuse-first invariant** — A compiled intake always has `reuse_first.required: true` and the ordered discovery list ending in `build_new`.
10. **Boundary** — The skill never creates an AI Engineering TASK, calls `ai-engineering-control`, plans, designs, or implements.

