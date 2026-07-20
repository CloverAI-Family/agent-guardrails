# Structured Task Delivery

Structured Task Delivery is a lightweight execution method for multi-step AI-assisted work.

It complements `agent-guardrails` checkpoints and delivery scans. Checkpoints preserve task state; delivery scans check the final output. Structured Task Delivery covers the middle: how to move through the task without losing scope, evidence, or reviewability.

This method is not an automation engine and not a replacement for human review. It gives the AI a small working pattern that is easy to inspect.

---

## When to use it

Use this method when a task has any of these traits:

- Three or more steps
- Multiple files or deliverables
- Git staging, commits, releases, or publishing
- Handoff between sessions or agents
- Requirements that could drift while work is in progress
- A final result that needs evidence, not just a summary

For very small tasks, use a normal answer and a short delivery scan instead.

---

## The four-part task map

Before acting, map the task into four named sections.

| Section | Meaning | Example |
|---------|---------|---------|
| Objective | Goal and scope | What is the task trying to accomplish? What is out of scope? |
| Deliverables | Planned changes or outputs | Which files, outputs, or decisions are expected? |
| Evidence | Verification plan | How will the result be checked? |
| Risks | Counterexamples and rollback | What could make the result wrong or unsafe? |

The map should be short. Its purpose is to prevent hidden assumptions, not to create paperwork.

This document uses named sections instead of letter labels. Some projects use labels such as `B1` or `B2` for review skills or step types. Avoid reusing those labels unless your project has defined them clearly.

Example:

```markdown
Objective:
Add a short guide that explains how to run a delivery scan.

Deliverables:
- Create `docs/delivery-scan.md`
- Link it from `README.md`

Evidence:
- File exists.
- README link points to the file.
- Public trace scan finds no private paths or internal names.

Risks:
- The guide may imply complete safety.
- README could link to the wrong path.
- Unrelated local changes could be staged by mistake.
```

---

## Pre-action gate

Before modifying files, calling tools, publishing, or producing a final answer, run two checks.

### Authorization check

Answer these first:

1. What is the authorization source?
   - Direct user request
   - Project instruction
   - Maintainer-approved plan
   - Inference only
2. Has the required input or target actually been verified to exist?
3. Is the action reversible, or is there a safe rollback path?

Stop and ask the maintainer if:

- The authorization source is inference only.
- The target file, repository, account, or environment has not been verified.
- The action is irreversible and no explicit approval exists.

For risky tool use, external content, memory writes, credentials, publishing, or security-sensitive actions, hand off to `defense/` before continuing.

### Planning check

Then answer:

1. Is the objective clear enough to test?
2. Is the allowed scope clear enough to avoid touching unrelated files?
3. Is there at least one concrete verification step?

If any answer is "no", stop and ask for clarification or reduce the task scope.

---

## Expected output and acceptance checks

For each deliverable, write one expected output and at least one acceptance check.

Weak:

```text
Update the docs.
```

Better:

```text
Deliverable 1 expected output: Create `docs/quickstart.md`.
Acceptance check: the file exists and includes sections for setup, first run, and limitations.
```

Acceptance checks can be simple:

- File exists
- Link resolves
- Diff only touches approved files
- Test passes
- Search finds or does not find a specific phrase
- A reviewer can locate the evidence used for the claim

Do not reduce every task to string matching. Many outputs are structural, behavioral, or evidence-based.

---

## Checkpoints during the task

Use continuity checkpoints at task start and major milestones.

At task start, record:

- Objective
- Scope
- Planned deliverables
- Verification plan
- Known risks

At each milestone, update:

- Completed work
- Files changed
- Evidence gathered
- Unknowns
- Risks that changed
- Next step

If the task is interrupted, the next session should be able to restart from the checkpoint without pretending it has perfect memory.

---

## Counterexample pass

Before final delivery, run at least one counterexample pass.

Ask:

- What would make this result fail?
- What file or requirement might have been missed?
- Did the task drift from the original request?
- Did the AI treat another agent's summary as verified evidence?
- Did any risky action occur without a clear approval point?

For larger tasks, run more than one pass from different angles:

- Scope counterexample: What was touched that was not approved?
- Evidence counterexample: Which claim lacks direct support?
- User-impact counterexample: What could confuse or harm the user?
- Recovery counterexample: Can this be rolled back cleanly?

---

## Git and staging purity

If the task uses Git, treat staging as part of the deliverable.

Before committing:

1. Check which files changed.
2. Separate task files from unrelated existing changes.
3. Stage only approved task files.
4. Make the commit message describe only the actual staged scope.

If unrelated changes are present:

- Do not stage everything by default.
- Do not hide them inside the current task commit.
- Mark them as unrelated and ask the maintainer how to handle them.

If unrelated changes must be included, say so explicitly in the checkpoint and final report.

---

## Delivery scan

Before final delivery, run a delivery scan.

Use a concise shape:

```markdown
Confirmed:
- ...

Assumptions:
- ...

Not verified:
- ...

Risks:
- ...

Final:
...
```

The exact headings can vary. The important rule is that evidence, assumptions, unknowns, and risks are not mixed together.

---

## How this connects to agent-guardrails

Structured Task Delivery is a companion method.

| Need | Use |
|------|-----|
| Preserve task state | `continuity/` checkpoint |
| Keep work aligned during execution | Structured Task Delivery |
| Check the final output | `quality/` delivery scan |
| Diagnose a completed result | `review/` |
| Guard risky tool use or external content | `defense/` |
| Check the guardrail setup itself | `watchdog/` |

Do not load every module for every task. Start with the smallest method that matches the risk.

---

## Minimal prompt

```text
Use Structured Task Delivery for this multi-step task.

First create a four-part task map: Objective, Deliverables, Evidence, and Risks.
Before acting, run the authorization check and the planning check.
For each deliverable, define an expected output and one acceptance check.
At major milestones, update a checkpoint.
Before final delivery, run a counterexample pass and a delivery scan.
```

---

## Limits

- This method does not guarantee correctness.
- It does not enforce permissions.
- It does not replace tests, diffs, reviews, or human approval.
- It can become too heavy for small tasks if used mechanically.

Use it to make work inspectable, not to make the AI look busy.
