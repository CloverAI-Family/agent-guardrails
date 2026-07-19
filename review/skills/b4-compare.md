# Skill B4: Compare

Package note: part of the agent-guardrails public package.

---

Provide objective comparison when multiple options need to be evaluated.

Based on LDRIT principle 4 and principle 5:
- fluent presentation does not automatically mean a better option
- evaluation dimensions should stay separated instead of being silently collapsed into one impression

## When to use

- The user is choosing between multiple approaches, designs, or solutions
- The AI has generated alternatives and needs to help evaluate them
- A decision point has been reached and trade-offs need to be made visible

本技能由入口觸發表條件成立時啟用（b4=the maintainer點名比較方案時），不自動常駐。

## Comparison procedure

### Step 1: List the candidates

Identify each option clearly. If the options are vague, ask the user to clarify before comparing.

### Step 2: Define evaluation dimensions

Ask: what matters for this decision?

Default dimensions (use when the user does not specify):

| Dimension | What it measures |
|-----------|-----------------|
| Correctness | Does it actually solve the problem? |
| Completeness | Does it cover all requirements? |
| Simplicity | How complex is the implementation or execution? |
| Risk | What could go wrong? How reversible is it? |
| Cost | Time, token, effort, or resource cost |

The user may add, remove, or reweight dimensions.

### Step 3: Evaluate each candidate

For each candidate, assess each dimension.

Rules:
- Be specific. "Option A is better" without explaining why is not useful.
- Acknowledge trade-offs. Most real decisions involve giving up something.
- Flag uncertainty. If you cannot confidently assess a dimension, say so.
- Do not favor the option you generated. If an external option is better, say so.

### Step 4: Present the comparison

Structure:

```
## Comparison

### Candidates
1. [Option A]: [one-line description]
2. [Option B]: [one-line description]

### Evaluation

| Dimension | Option A | Option B |
|-----------|----------|----------|
| Correctness | ... | ... |
| Completeness | ... | ... |
| Simplicity | ... | ... |
| Risk | ... | ... |
| Cost | ... | ... |

### Trade-off summary
- Option A is stronger in [X] but weaker in [Y]
- Option B is stronger in [Y] but weaker in [X]

### Recommendation
- [If one option is clearly better, say so and explain why]
- [If it depends on priorities, state which priority leads to which choice]
- [If genuinely equal, say so — do not force a winner]
```

## Anti-bias rules

1. Do not default to recommending the most recent or most complex option
2. Do not dismiss simple solutions just because they feel too easy
3. If you proposed one of the options, hold it to the same standard as the others
4. If the user seems to prefer an option, evaluate it honestly — do not just confirm their preference





