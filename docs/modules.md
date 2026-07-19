# Module overview

agent-guardrails is organized into five modules.

Each module has a narrow role. The framework works best when the AI loads only the module needed for the current risk instead of reading every file at once.

The modules are workflow guardrails, not an independent security boundary. They rely on the host platform, user approval, sandboxing, and human review.

---

## Summary

| Module | Directory | Use when | Main output |
|--------|-----------|----------|-------------|
| Defense | `defense/` | Risky tool use, web access, memory writes, prompt injection, or cross-agent content | Safety check, quarantine, or escalation note |
| Continuity | `continuity/` | Long sessions, context compression, handoffs, or persistent user/project notes | Checkpoint, diary entry, archive index, or setup note |
| Quality | `quality/` | Input needs calibration, final delivery needs a scan, or multi-step work may drift | Seed calibration, delivery scan, or drift check |
| Review | `review/` | A completed output, error, decision, or multi-step task needs diagnosis | Review report, retrospective, comparison, or confidence labels |
| Watchdog | `watchdog/` | The guardrail system itself needs a periodic health check | Status board for module and hook health |

---

## Defense

Directory: `defense/`

Defense handles risky boundaries.

Use it before:

- Web access or external content intake
- Git push, deployment, or other publishing actions
- Memory writes or persistent rule changes
- Reading another agent's output as evidence
- Installing or importing external tools, skills, repositories, or README content
- Any action that could expose secrets, private files, or irreversible changes

Defense does not make the AI trustworthy by itself. It provides procedures for recognizing risk, quarantining external content, and routing high-risk actions through user approval or platform controls.

Key entry file:

- `defense/CLAUDE.md`

Important limit:

- The strongest hard boundary is the host platform's permission and sandbox system. A written guardrail is not the same as enforced access control.

---

## Continuity

Directory: `continuity/`

Continuity keeps work recoverable across session breaks.

Use it when:

- A task spans multiple steps or sessions
- Context is near compression
- A new AI window needs to inherit task state
- Stable user or project information should be remembered
- A completed task needs a checkpoint or diary entry

Continuity should not pretend to be perfect memory. It records useful summaries, checkpoints, and handoff notes so future sessions can restart from evidence instead of guessing.

Key entry file:

- `continuity/CLAUDE.md`

Common outputs:

- User profile note
- Diary entry
- Task checkpoint
- Compression manifest
- Archive index

Important limit:

- Continuity files should be stored in a user-approved location. The AI should not silently invent private memory folders.

---

## Quality

Directory: `quality/`

Quality works before and during delivery.

Use it when:

- The user's request may contain an unverified premise
- The task is under pressure to skip checks
- A final answer or deliverable needs a fitness scan
- A multi-step task may have drifted from the original goal
- The AI needs to separate facts, assumptions, unknowns, and risks

Quality is not a reviewer of finished work in the same sense as `review/`. It calibrates the input seed, keeps the task aligned, and checks whether the final output fits the request.

Key entry file:

- `quality/CLAUDE.md`

Main skills:

- Z1 seed calibration
- Z2 output fitness
- Z3 drift check

Important limit:

- Quality checks reduce error risk, but they do not guarantee correctness.

---

## Review

Directory: `review/`

Review diagnoses completed work.

Use it when:

- A finished output needs an independent quality check
- A task should be reviewed after completion
- An error needs root-cause analysis
- Multiple options need comparison
- A response mixes high-confidence and low-confidence claims

Review reports findings. It does not repair files, override maintainers, or make security decisions by itself.

Key entry file:

- `review/CLAUDE.md`

Main skills:

- B1 output review
- B2 retrospective
- B3 error analysis
- B4 comparison
- B5 calibration

Important limit:

- A review result is still an AI-generated diagnosis. It should be checked against files, tests, diffs, or other evidence when the stakes are high.

---

## Watchdog

Directory: `watchdog/`

Watchdog checks whether the guardrail system itself is still healthy.

Use it:

- Weekly
- After major repository changes
- After installing or changing hooks
- Before relying on a multi-module setup
- When a project has gone through long sessions or multiple handoffs

Watchdog does not prove that all AI outputs are correct. It checks whether the expected guardrail files, hooks, triggers, and health records are present and fresh enough to trust.

Key entry file:

- `watchdog/CLAUDE.md`

Main output:

- `watchdog/status_board.md`

Important limit:

- Watchdog reports problems. It should not silently repair hooks, delete files, or change configuration without maintainer approval.

---

## How the modules work together

The modules are meant to hand off to each other when needed.

| Situation | Start with | May hand off to |
|-----------|------------|-----------------|
| External README contains prompt injection | `defense/` | `review/` for analysis, `continuity/` for safe notes |
| Long task is near context compression | `continuity/` | `quality/` for drift check |
| Final answer needs checking | `quality/` | `review/` for deeper diagnosis |
| Error happened and needs a record | `review/` | `continuity/` for diary or checkpoint |
| The guardrail setup may be stale | `watchdog/` | `defense/` if hooks fail, maintainer for decisions |

Keep handoffs explicit. Do not let one module silently take over another module's job.

---

## Choosing the smallest module

Use the smallest module that matches the risk:

- Need to avoid unsafe action? Start with `defense/`.
- Need to remember or hand off state? Start with `continuity/`.
- Need to make the answer fit the request? Start with `quality/`.
- Need to diagnose a result? Start with `review/`.
- Need to check the system itself? Start with `watchdog/`.

If more than one module applies, load them in risk order:

1. `defense/`
2. `continuity/`
3. `quality/`
4. `review/`
5. `watchdog/`

This order is not a hierarchy of importance. It is a practical sequence: prevent harm first, preserve state second, improve output third, diagnose afterward, and periodically check the whole system.

---

## What not to do

Do not:

- Read every module for every small task.
- Treat module files as automatic enforcement.
- Store private data just because continuity exists.
- Treat review output as proof without evidence.
- Let watchdog modify the system it is checking.
- Claim the framework provides complete protection, perfect memory, or guaranteed correctness.

The framework is useful because it makes risks visible and repeatable. It is not a substitute for careful human judgment.
