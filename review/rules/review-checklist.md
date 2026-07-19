# Review Checklist

**【maintainer-protected evaluation rule】本清單屬評價規則，受 agent-guardrails maintainer-protected evaluation rule——修改僅可提案，changes require maintainer approval。**
Package note: part of the agent-guardrails public package.

---

Default quality standards for review module diagnosis.
Users may customize this checklist for their specific needs.

## Universal checks (apply to all output types)

- [ ] Factual claims are traceable to source material or provided context
- [ ] No internal contradictions within the output
- [ ] No contradictions with previously established decisions or context
- [ ] All parts of the user's request are addressed
- [ ] Assumptions are stated, not hidden
- [ ] Uncertainty is marked where it exists
- [ ] Scope matches what was asked — no silent drift

## Code-specific checks

- [ ] Logic matches the stated intent
- [ ] Edge cases are handled or acknowledged
- [ ] No security vulnerabilities introduced (injection, exposure, etc.)
- [ ] Error handling is appropriate (not excessive, not missing)
- [ ] Changes are limited to what was requested — no unnecessary refactoring

## Document-specific checks

- [ ] Structure is clear and navigable
- [ ] Terminology is consistent throughout
- [ ] Claims are supported, not just asserted
- [ ] Version and status information is accurate
- [ ] No placeholder or draft content left unresolved

## Theory/research-specific checks

- [ ] Claims respect layer separation (LDRIT principle 5)
- [ ] New assertions do not contradict established first principles
- [ ] Evidence level is honestly stated (verified / supported / speculative)
- [ ] Definitions are precise and consistent with existing terminology
- [ ] Open questions are flagged, not silently assumed resolved

## LDRIT-specific checks (LDRIT research only — skip if not applicable)

- [ ] No cross-layer conflation without explicit marking
- [ ] Non-ontological declaration respected (no consciousness claims)
- [ ] External framework absorption follows the three-question filter
- [ ] Testable predictions include falsification conditions
- [ ] Mathematical claims distinguish precise formulas from directional relationships





