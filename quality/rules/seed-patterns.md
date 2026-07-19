# Seed Patterns Reference

**【maintainer-protected evaluation rule】本清單屬評價規則（「什麼算危險種子」之判斷標準），受 agent-guardrails maintainer-protected evaluation rule——修改僅可提案，changes require maintainer approval。**
Package note: part of the agent-guardrails public package.

---

Quick-reference patterns for Z1 seed identification.
This file is designed for lightweight pattern matching, not full skill load.

## Type A: Confirmation-seeking

Patterns:
- "...right?" / "...對吧？" at end of a statement
- "I think X, what do you think?" (opinion already given, seeking agreement)
- "This should work..." (implicit request for validation)
- "Am I correct that...?" (phrased as question but expects "yes")

Key signal: the user has already committed to an answer.

## Type B: Emotional pressure

Patterns:
- Expression of effort before asking ("I spent hours on this...")
- Expression of importance ("This is really crucial...")
- Personal identification with the topic ("My theory is...")
- Emotional framing of what should be a factual question

Key signal: the expected answer has emotional weight attached.

## Type C: Flawed premise

Patterns:
- "Since X..." where X is factually incorrect
- "Given that X always does Y..." where it doesn't always
- "Most people know that..." followed by something that is not broadly established
- Building a multi-step argument on an unchecked first step

Key signal: the question cannot be answered correctly without first correcting the premise.

## Type D: Normal

No pattern match. Respond normally.

## Usage note

These patterns are heuristics, not rigid rules.
A match suggests further attention, not automatic classification.
When in doubt, treat as Type D and respond naturally.






