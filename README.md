# agent-guardrails

**A modular governance framework for multi-agent AI teams.**

Protect against prompt injection, keep memory coherent across session breaks, guard output quality, and monitor system health — five focused modules, each independently deployable.

agent-guardrails grew out of practical work coordinating multiple AI assistants across long-running tasks, session resets, and tool-enabled workflows. The framework captures recurring failure modes and turns them into reusable guardrails.

---

## Modules

| Module | Directory | Role |
|--------|-----------|------|
| defense | `defense/` | Blocks prompt injection, protects memory, guards online mode |
| continuity | `continuity/` | Maintains memory across session breaks; task checkpoints |
| quality | `quality/` | Calibrates input seeds; guards output quality; drift checks |
| review | `review/` | Diagnoses outputs; retrospectives; error analysis |
| watchdog | `watchdog/` | Weekly health check of the other four modules |

---

## Why this framework exists

### 1. The attacker cannot bypass the user's platform permissions

defense/g1 relies on the platform's confirmation dialogs — a safety layer the AI cannot override.
Even a fully compromised AI cannot skip a user-facing confirmation prompt.

### 2. Continuity without full-context illusions

AI sessions end. Context gets compressed. Memory gets lost.
The continuity module gives AI instances structured tools to pass context forward without pretending nothing was lost.

### 3. Sycophancy is structural, not accidental

AI models are trained toward agreement. The quality module's Z1 skill treats this as an architecture problem, not a personality flaw, and addresses it at the input-seed level before generation begins.

---

## Honest limitations

- **Defense modules rely on AI self-compliance.** A sufficiently compromised AI may ignore these rules. The only hard line is the platform's permission system (defense/g1 Level RED).
- **Quality calibration is probabilistic.** Seed type classification can miss subtle cases. The user is always the final judge.
- **Continuity is not perfect memory.** Diary entries and checkpoints are written by an AI that already has context loss. They are better than nothing, not a full transcript.
- **Watchdog checks health, not correctness.** If all five modules are present but misconfigured, watchdog may show green while the system is broken.
- **This framework was developed and tested on Claude Code.** Its concepts can be adapted to other AI coding or agent platforms, but hooks and trigger mechanics may require platform-specific changes.

---

## AI-authored declaration

本框架由 AI 輔助撰寫、跨模型審查、人類治理。

This framework was built with AI-assisted drafting, cross-model review, and human governance. The design, architecture decisions, and governance rules reflect human direction; the writing and implementation are AI-produced.

We include this declaration because attribution matters. AI-authored tools should say so.

---

## Getting started

Start with `docs/quickstart.md` for a short first-run path.
See `INSTALL.md` for full setup instructions.

---

## License

MIT License — see `LICENSE`.

Copyright (c) 2026 CloverAI

