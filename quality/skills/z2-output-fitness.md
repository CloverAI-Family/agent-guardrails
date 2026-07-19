# Skill Z2: Output Fitness — Delivery Scan Execution Guide

Package note: part of the agent-guardrails public package.

---

Z2 is no longer a separately-triggered skill.
The mandatory delivery scan (required on every deliverable) is the trigger;
Z2 is the **how-to guide** behind it. The scan asks "fit for delivery?" —
this file defines what "fit" means for format, depth, and length.

It checks whether the response fits the context — not whether it is
correct (review module's job).

## When to use

- While running the mandatory delivery scan on any deliverable
- The user explicitly asks for formatting or structural adjustment
- A scan item gets N for fitness reasons and the output needs repair

## Fitness dimensions

### Depth

| Context | Appropriate depth |
|---------|------------------|
| Quick question | Direct answer, 1-3 sentences |
| Explanation request | Structured explanation with reasoning |
| Technical deliverable | Full detail with edge cases |
| Decision support | Enough to decide, not more |

Rule: match the depth to the question's complexity, not to a fixed standard.

### Length

| Signal | Action |
|--------|--------|
| User asked a yes/no question | Answer yes/no first, then explain only if needed |
| User said "briefly" or "quick" | Compress aggressively |
| Task requires thoroughness | Be thorough, do not artificially shorten |
| Output is repeating the same point in different words | Cut the repetition |

### Format

| Content type | Suggested format |
|-------------|-----------------|
| Comparison | Table |
| Sequential steps | Numbered list |
| Single concept explanation | Prose |
| Mixed data and narrative | Sections with headers |
| Status update | Bullet points |

These are defaults, not mandates. The user may prefer differently.

## Redundancy control

Remove before delivery:

| Redundancy type | Example | Action |
|-----------------|---------|--------|
| Filler opening | "Great question!", "That's a really interesting point!" | Remove |
| Restating the question | "You asked about X. Let me tell you about X." | Remove |
| Trailing summary | "In summary, [repeat everything just said]" | Remove unless output is very long |
| Apologetic hedging | "I might be wrong, but..." (when the AI has evidence) | Replace with clear statement |
| Meta-commentary | "Let me think about this step by step" (shown to user) | Remove unless thinking process adds value |

## Proactive suggestion

When the quality module detects a fitness mismatch, it can suggest adjustment:

> This response might work better as [format/length]. Want me to adjust?

If the user declines, respect the preference and do not repeat the suggestion
for the same type of output.

══════════════════════════════════════════════════════
以下為評價規則，受maintainer-protected evaluation rule——修改僅可提案，changes require maintainer approval
══════════════════════════════════════════════════════

## Delivery scan format

交付掃描格式（quality Z2 執行指引——此格式為受保護評價規則）：

```
---
交付掃描
□ 事實可追溯：[Y — 依據] / [N — 問題]
□ 邏輯無跳躍：[Y — 依據] / [N — 問題]
□ 無迎合性失真：[Y — 依據] / [N — 問題]
□ 回答了被問的問題：[Y — 依據] / [N — 問題]
```

判定標準：
- Y = 能從本次對話內容或工具輸出找到依據
- N = 存在缺口或問題；任一 N → 修正後再交付，不跳過

任何 N → 修正後再交付，不跳過。

══════════════════════════════════════════════════════
評價規則段結束
══════════════════════════════════════════════════════

## What Z2 does NOT do

- Does not check factual accuracy (review module's job)
- Does not calibrate input seeds (Z1's job)
- Does not monitor MEMORY.md length (platform-specific hook)





