# Skill Z3: Drift Check (Long-Chain Quality Guard)

Package note: part of the agent-guardrails public package.

---

Fills the routing gap left by the unimplemented z4/z5:
quality silently degrades during long multi-step tasks. Z3 is a periodic
anchor check, run at task checkpoints, not a constant monitor.

Based on LDRIT: generation quality decays with inheritance distance, and
long contexts rot (literature-verified). Self-evaluation inside one context
is biased — Z3 therefore checks against **external anchors** (the checkpoint
file, the original request, earlier outputs), not against the AI's own
feeling of "still fine".

## When to use

- At every continuity module s5 checkpoint update of a multi-step task (3+ steps)
- When resuming a task after interruption or context compaction
- 使用者明說品質變差，或 z3 機械條件成立（檢查點更新+任務≥3步+曾壓縮或中斷）
- Before the final deliverable of a long chain

**Note**: Z3 does not self-trigger. If s5 is skipped or unavailable, Z3 does
not run and gives no warning. When in doubt, run Z3 manually — it is a short
check with low cost.

**Where the checkpoint lives**: the active checkpoint is the most recent
`status: in_progress` file under the continuity data root, default
`.agent-continuity/checkpoints/`. When resuming after interruption, locate it FIRST —
without it, anchors 1 and 2 have no source to check against. If no checkpoint
exists, fall back to the original user request and the latest dialogue legacy.

## When NOT to use

- Single-step tasks (delivery scan covers them)
- Casual conversation

## The three anchors

Check each anchor explicitly. Do not rely on memory — re-read the sources.

### Anchor 1: Goal (目標錨)

Re-read: the active checkpoint's task description + the user's original request.

- Is the current step still serving what the user asked?
- Has scope quietly grown or shifted? (scope creep is drift, even when each
  single step looked reasonable)
- If drifted: name the drift, ask the user before continuing on the new path.

### Anchor 2: Consistency (一致錨)

Compare against earlier outputs of the same chain:

- Format: same structure, headers, naming conventions?
- Terminology: same words for the same things? (silent renaming confuses inheritance)
- Decisions: does the current step contradict an earlier confirmed decision?
- If inconsistent: fix before producing more output on the broken pattern.

### Anchor 3: Decay (衰退錨)

Signs of context rot in this session:

- Forgetting constraints stated earlier
- Re-doing work already completed
- Reasoning becoming vaguer; hedging replacing specifics
- Mis-referencing files or paths that were correct before

If 2+ signs present: stop adding to this context. Save state
(continuity module s2 closing diary / s5 checkpoint), recommend the user start a fresh
session and inherit via files. A clean restart beats a long degraded chain.

## Output

One short drift report (3 lines max) at the checkpoint:
`目標錨 [OK/偏移+說明] | 一致錨 [OK/不一致+說明] | 衰退錨 [OK/觸發:徵兆名稱列舉]`

For the decay anchor: if triggered, list the specific symptom names (e.g.,
forgot-constraint, redid-completed-work, vague-reasoning, wrong-path), not
just the count. The next session needs to know *what* is decaying, not just
that decay happened.

Append it to the checkpoint file so the next session inherits the trend.

## What Z3 does NOT do

- Does not judge factual correctness (review module b1)
- Does not calibrate input seeds (Z1)
- Does not replace the delivery scan — Z3 guards the chain, the scan guards
  the deliverable. (z2-output-fitness still exists: it was repositioned in
  Phase 3 as the scan's execution guide, not deprecated.)

## Cross-module

| Situation | Hand off |
|-----------|----------|
| Drift trend worth keeping | continuity module s5 (checkpoint) / s2 (diary) |
| Quality diagnosis needed after the fact | review module b2-retrospective |
| Decay anchor triggers a restart | continuity module s2 closing diary before ending |





