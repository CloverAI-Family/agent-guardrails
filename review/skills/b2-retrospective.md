# Skill B2: Retrospective

Package note: part of the agent-guardrails public package.

---

Review the overall quality of a completed multi-step task or body of work.

Unlike B1 (single output check), B2 looks at the whole picture:
Was the approach sound? Were the right decisions made? What was missed along the way?

Based on LDRIT: in multi-step tasks, errors compound through inheritance chains (S = P^n).
A retrospective catches accumulated drift that single-step checks might miss.

## When to use

- A multi-step task reaches a checkpoint, pause, or completion point
- The user asks for a review of recent work
- Before finalizing and archiving a piece of work
- At a continuity module checkpoint (on_multi_step_task_checkpoint)

## When NOT to use

- After a single, simple output (use B1 instead)
- In the middle of active work when the user hasn't paused or reached a checkpoint

## Retrospective procedure

### Step 1: Scope the review

Identify what is being reviewed:
- What was the original goal?
- What steps were taken?
- What was produced?

### Step 2: Decision audit

For each significant decision made during the task:

| Question | What to assess |
|----------|---------------|
| Was this the right call? | Given what was known at the time, was this reasonable? |
| Were alternatives considered? | Or was the first idea accepted without question? |
| Did assumptions hold? | Were early assumptions validated or just carried forward? |
| Did scope change? | Did the work drift from the original goal? If so, was the drift justified? |

### Step 3: Quality assessment

| Dimension | What to check |
|-----------|--------------|
| Correctness | Are the results factually and logically sound? |
| Completeness | Was everything that was asked for actually addressed? |
| Consistency | Do all parts cohere with each other and with prior decisions? |
| Proportionality | Was the effort proportional to the importance? Over-engineered? Under-done? |

### Step 4: Inheritance check

Based on LDRIT's inheritance model:

| Check | What to look for |
|-------|-----------------|
| Context drift | Did important context get lost between steps? |
| Contradiction accumulation | Did small inconsistencies pile up into larger problems? |
| Assumption propagation | Did an early wrong assumption propagate uncorrected through later steps? |

#### Inheritance quality diagnosis

Beyond checking for errors, assess how well context was actually used:

| Question | What to assess |
|----------|---------------|
| Was established context reused? | Did later steps build on earlier decisions, or did they start from scratch? |
| Were user corrections incorporated? | If the user corrected something early on, was that correction maintained throughout? |
| Did important context get silently dropped? | Were there facts established early that disappeared from later reasoning without explanation? |

If the answer to any of these is concerning, note it in the report under "Issues found"
with the tag `[inheritance quality]`.

This is not a failure of the task itself — it is a failure of how context was carried forward.
The distinction matters because the fix is different: task failures need better logic,
inheritance failures need better context management.

### Step 5: Report

Present findings directly in conversation. Structure:

```
## Retrospective

### What was done
- [brief summary of the task and steps taken]

### What went well
- [decisions and outcomes that were sound]

### Issues found
- [issue]: [what went wrong] — [impact: high/medium/low]

### Missed opportunities
- [things that could have been done better or differently]

### Recommendations
- [specific suggestions for next time or follow-up actions]
```

Do not store the report as a file. Deliver in conversation only.
If the user decides the conclusions are worth preserving, hand off to the continuity module.

## Red team mode

When the user requests aggressive review or red team attack:

1. Assume the work contains hidden flaws
2. Actively try to break conclusions, not just verify them
3. Challenge assumptions that were taken for granted
4. Look for what was NOT said (silent omissions)
5. Test edge cases that were not addressed
6. Flag any instance of circular reasoning or self-confirming logic

Mark red team findings clearly:

```
### Red Team Findings
- [finding]: [attack vector] — [severity]
```

### Guard against false positives

Red team mode is not a quota system. If thorough attack reveals no real flaw,
report that explicitly:

```
### Red Team Findings
No structural flaws found after testing [list of attack vectors attempted].
```

Do not manufacture problems to fill the report.
A clean result after genuine attack is a valid and valuable outcome.





