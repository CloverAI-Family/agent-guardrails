# Skill B5: Calibration Marking

Package note: part of the agent-guardrails public package.

---

Provide a one-time certainty assessment for the current output.

Based on LDRIT claim 5 (self-calibration) and R9:
AI reliability improves when the model distinguishes what it knows from what it guesses.
B5 is a tool for making that distinction explicit — not a persistent attitude change.

## When to use

- The user asks "how sure are you about this?"
- The output contains claims that span different confidence levels
- A decision will be made based on the output and confidence matters

This is a manually triggered, one-time tool. It does NOT:
- Persistently change how the AI communicates
- Make the AI add uncertainty markers to every future response
- Run in the background monitoring confidence levels

## Calibration procedure

### Step 1: Identify claims

List the key claims, conclusions, or recommendations in the current output.

### Step 2: Assess each claim

For each claim, assign a confidence level:

| Level | Label | Meaning |
|-------|-------|---------|
| 1 | Verified | Directly confirmed by source material or user-provided facts |
| 2 | High confidence | Strongly supported by context and consistent with known patterns |
| 3 | Moderate confidence | Reasonable inference but depends on assumptions |
| 4 | Low confidence | Plausible but based on limited information or analogy |
| 5 | Speculative | Best guess with no strong basis — could easily be wrong |

### Step 3: Explain the basis

For each claim rated 3 or below, briefly state:
- What the assessment is based on
- What would change the confidence level (up or down)

### Step 4: Present

Structure:

```
## Calibration

| Claim | Confidence | Basis |
|-------|-----------|-------|
| [claim 1] | Verified | [source] |
| [claim 2] | High | [reasoning] |
| [claim 3] | Moderate | [assumption: X] — would upgrade if [Y] confirmed |
| [claim 4] | Speculative | [limited basis] — treat with caution |
```

## Guard against overcaution

LDRIT R8 warns that expressing uncertainty can create a positive feedback loop
toward excessive caution. To counter this:

1. Do not downgrade confidence without a specific reason
2. "I'm not 100% sure" is not a valid confidence assessment — be specific about what is uncertain
3. If the evidence is strong, say so confidently. Hedging everything is not calibration.
4. Calibration means accuracy of confidence, not minimization of confidence





