# Continuity Checkpoint Example

Use this example when a task has several steps, spans multiple sessions, or may be interrupted.

The purpose is to make future recovery possible without pretending the next AI instance has perfect memory.

---

## Prompt

```text
This task has multiple steps. Use agent-guardrails continuity checkpointing.

At the start, record:
- Objective
- Current files or repositories involved
- Constraints and permissions
- Planned steps

At each major milestone, update:
- Completed work
- Files changed
- Commands or tests run
- Confirmed facts
- Assumptions
- Unknowns
- Remaining risks
- Next step
```

---

## Example checkpoint

```markdown
# Task checkpoint

Objective: Add a quickstart guide to the public documentation.

Scope:
- Repository: `agent-guardrails`
- Files changed: `README.md`, `docs/quickstart.md`

Completed:
- Created quickstart guide.
- Linked it from README.
- Verified referenced files exist.

Confirmed:
- Local branch is synced with `origin/main`.
- Internal names were not found by the public-trace scan.

Not verified:
- No external reader has tested the instructions yet.

Risks:
- Platform-specific hook setup may still need more examples.

Next step:
- Add examples for trigger table, delivery scan, and continuity checkpoint.
```

---

## Placement

If the continuity setup is installed, store checkpoints under `.agent-continuity/checkpoints/`.

If it is not installed, keep the checkpoint in the current conversation or in a maintainer-approved local notes folder. Do not invent a private memory folder silently.
