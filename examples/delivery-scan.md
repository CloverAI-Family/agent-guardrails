# Delivery Scan Example

Use this example before sending a final answer, code change, document, or analysis result.

The purpose is to make the final output easier to verify.

---

## Prompt

```text
Before final delivery, use agent-guardrails quality output fitness.

Check:
- Did the answer satisfy the original request?
- Which claims are confirmed by direct inspection?
- Which claims are assumptions or inferences?
- What did you not verify?
- What risks or follow-up tests remain?

Then deliver the final answer with only the important results.
```

---

## Expected output shape

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

You do not need to use these exact headings every time. The important part is that evidence, assumptions, unknowns, and risks are not mixed together.

---

## Good result

A good delivery scan says what was actually checked:

```text
Confirmed: README links to docs/quickstart.md, and that file exists.
Not verified: I did not test installation hooks because this environment does not include them.
Risk: The defense module still depends on platform-specific hook setup.
```

---

## Weak result

This is not enough:

```text
Everything looks good.
```

It gives no evidence, no scope, and no remaining risk.
