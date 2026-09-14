# Voice policy

Voice is a hard gate, not a preference.

## Allowed

- Typed text may activate the skill: “开始立项”, “start intake”, or equivalent.
- Typed text may request formatting after an already completed voice interview.
- The assistant may use transcription as evidence only when the host explicitly exposes that the source was a verified voice session.

## Forbidden

- Treating ordinary typed text as a spoken answer.
- Inferring voice from message shape, punctuation, timing, or a transcript without provenance.
- Completing, compiling, or marking `CONFIRMED_PROJECT_INTAKE` when the host cannot verify voice.
- Treating a typed answer during an active interview as evidence.

## Pause and resume

On typed input, lost voice, unavailable provenance, or host capability uncertainty: transition to `VOICE_REQUIRED`, preserve prior verified evidence, discard the new text as formal evidence, and request a verified voice session before continuing. Resume only after verification returns true.

The final readback and explicit confirmation must also be spoken and verifiable. A text “yes” cannot pass the final gate.

