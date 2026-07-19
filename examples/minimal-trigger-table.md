# Minimal Trigger Table

Use this example when you want the AI to know when to load agent-guardrails modules.

Add the block below to your project instruction file, such as `CLAUDE.md`.

```markdown
## agent-guardrails triggers

- Before final delivery, read `agent-guardrails/quality/CLAUDE.md` and run the smallest relevant delivery check.
- When reviewing a completed output, read `agent-guardrails/review/CLAUDE.md` and choose the smallest review skill that fits.
- For tasks with 3 or more steps, read `agent-guardrails/continuity/CLAUDE.md` and create checkpoints at major milestones.
- Before online access, memory writes, git push, or other high-risk tool use, read `agent-guardrails/defense/CLAUDE.md` and apply the relevant guardrail.
- For weekly maintenance, read `agent-guardrails/watchdog/CLAUDE.md` and run the module health check.
```

---

## Expected behavior

The AI should:

- Load only the module needed for the current event.
- Read only the specific skill needed after loading the module entry file.
- Explain which guardrail was used when it affects the result.
- Report checks performed instead of saying only "looks good".

---

## Failure signs

The trigger table is not working if the AI:

- Claims all modules are active without reading or applying them.
- Loads every skill file at once for a small task.
- Treats workflow prompts as hard security guarantees.
- Skips human confirmation for high-risk tool actions.
