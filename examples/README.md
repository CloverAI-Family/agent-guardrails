# Examples

These examples show small ways to try agent-guardrails before building a full workflow.

Each example is intentionally copyable. Adapt paths and platform-specific instruction files to your own environment.

---

## Starter examples

| Example | Use when |
|---------|----------|
| `minimal-trigger-table.md` | You want a small instruction block that tells the AI when to load each module |
| `delivery-scan.md` | You want a final-answer check before sending code, documents, or analysis |
| `continuity-checkpoint.md` | You want recoverable task state before a long session ends |

---

## Recommended order

1. Add the minimal trigger table.
2. Try one delivery scan on a real task.
3. Add continuity checkpoints only when work spans multiple steps or sessions.
4. Install defense hooks only after reading `INSTALL.md` and `defense/TEST.md`.

---

## Safety note

These examples are workflow prompts, not hard security boundaries.

Platform permissions, human review, and verified hook behavior remain the real enforcement layer.
