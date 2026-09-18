# Input-channel policy

Voice is an optional preferred channel, not a hard gate. The interview must remain usable when voice disconnects or is unavailable.

## Channel selection

- Voice may be used when it is available and stable.
- Typed text may activate or continue the skill: “开始立项”, “start intake”, or equivalent.
- A user may switch between voice and text at any point without restarting the interview.
- Record the available channel/source as internal provenance when useful, but do not require or infer a special voice capability.

## Forbidden behavior

- Blocking progress because voice is unavailable or disconnected.
- Discarding a typed answer during an active interview.
- Requiring a voice session for readback, confirmation, or compilation.
- Designing a solution, choosing technology, or decomposing tasks because the user changed channels.

## Continuity

On voice loss or channel change, preserve all confirmed evidence and continue in `INTERVIEW_ACTIVE` with the next highest-information-gain question. Do not repeat questions solely because the channel changed.

Only text or transcript content actually delivered to the interview counts as evidence. Do not infer missing speech from the fact that an audio session remained connected. After each substantive voice answer, briefly reflect the captured fact before asking the next question so the user can correct an incomplete transcript. At natural topic boundaries, give a compact ledger checkpoint. If voice transcription becomes incomplete or stops advancing, preserve the last confirmed checkpoint and continue in text.

The final readback and explicit confirmation may be spoken or typed. The confirmation must be explicit and attributable to the user, but it does not require voice verification.
