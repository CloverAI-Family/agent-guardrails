# Skill B3: Error Analysis

Package note: part of the agent-guardrails public package.

---

When something went wrong, find the root cause — not just the surface symptom.

Based on LDRIT: errors in AI output are often inheritance failures.
The visible symptom (wrong answer, contradiction, hallucination) may be far
from the actual point of failure (missing context, conflicting c layers, seed mismatch).

## When to use

- An output was wrong and the user wants to understand why
- A task failed and the cause is not obvious
- The same type of error keeps recurring

本技能由入口觸發表條件成立時啟用（b3=錯誤案例建檔時），不自動常駐。

## Error analysis procedure

### Step 1: Describe the symptom

What exactly went wrong? Be precise:
- What was expected?
- What was produced instead?
- Where in the output does the error appear?

### Step 2: Trace the inheritance chain

Work backward from the error to find where things diverged:

| Layer | Question |
|-------|----------|
| c_dialogue | Was the relevant context present in the conversation? Was it lost or buried? |
| c_user | Did user instructions conflict with each other or with the task? |
| c_system | Did system-level constraints interfere with the intended output? |
| Seed | Did the most recent input (seed) point in a different direction than intended? |
| c layer conflict | Were two or more layers pulling in opposite directions? (R7) |

### Step 3: Classify the failure type

| Type | Description | LDRIT mapping |
|------|-------------|---------------|
| Context loss | Important information was present but not picked up | c_dialogue decay |
| Context conflict | Two pieces of context contradict each other | c_eff reduction (R7) |
| Seed mismatch | The input pointed one way, the context pointed another | Seed-soil imbalance |
| Overcertainty | AI stated something confidently that it should not have | Low q_calibration |
| Assumption propagation | An early wrong assumption was never corrected | Inheritance chain failure |
| Scope drift | The AI answered a different question than what was asked | Seed direction ignored |
| Knowledge gap | The AI genuinely did not have the needed information | k limitation |

### Step 4: Identify the root cause

The root cause is the earliest point in the chain where a correction could have prevented the error.

Ask:
- If this one thing had been different, would the error still have occurred?
- Is this a one-time mistake or a structural pattern?

### Step 5: Report

Present findings directly in conversation. Structure:

```
## Error Analysis

### Symptom
- [what went wrong]

### Trace
- [step-by-step backward trace through the inheritance chain]

### Root cause
- [the earliest point of failure]

### Failure type
- [classification from the table above]

### Suggestion
- [what could prevent this in the future — if anything actionable]
```

Do not store the report as a file. Deliver in conversation only.

## Important: review module does not fix

B3 finds the cause. It does not execute the fix.
The user decides what to do with the diagnosis.
If the fix involves security-sensitive actions, defer to the defense module.





