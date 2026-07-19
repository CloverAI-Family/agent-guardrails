# Quickstart

This guide helps you try agent-guardrails in a new project without installing every module at once.

The goal is not to make the AI autonomous. The goal is to make AI-assisted work easier to verify, recover, and govern.

---

## 1. Choose a starting scope

Pick one of these paths:

| You need | Start with |
|----------|------------|
| Safer tool use and prompt-injection defense | `defense/` |
| Better handoff across long sessions | `continuity/` |
| Cleaner final answers and deliverables | `quality/` |
| Independent review or error diagnosis | `review/` |
| Periodic system health checks | `watchdog/` |

For a first trial, start with `quality/` and `review/`. They do not require hooks and are easy to test on ordinary writing or coding tasks.

---

## 2. Copy the framework

Copy this repository into your project root:

```text
your-project/
|-- agent-guardrails/
`-- your existing project files
```

You can also copy only the module folders you want to test.

---

## 3. Add a minimal trigger table

Add this to your project instruction file, such as `CLAUDE.md`:

```markdown
## agent-guardrails triggers

- Before final delivery, read `agent-guardrails/quality/CLAUDE.md` and run the output fitness scan.
- When reviewing a result, read `agent-guardrails/review/CLAUDE.md` and choose the smallest review skill that fits.
- Before ending a long session, read `agent-guardrails/continuity/CLAUDE.md` and write a checkpoint or diary entry if needed.
- Before online access, memory writes, or git push, read `agent-guardrails/defense/CLAUDE.md` and apply the relevant guardrail.
```

This table is intentionally small. Expand it only after you have tested the workflow.

---

## 4. Run a first quality check

Give your AI a normal task. Before the final answer, ask it to:

```text
Use agent-guardrails quality output fitness before final delivery.
Report confirmed facts, assumptions, unknowns, and remaining risks.
```

Expected result:

- The AI should check whether the answer actually matches the request.
- It should separate evidence from assumptions.
- It should name missing tests, unverified claims, or risky next steps.

If the AI only says "looks good" without concrete checks, the guardrail was not applied correctly.

---

## 5. Add continuity only when needed

Use `continuity/` when tasks span multiple sessions, long context windows, or several AI assistants.

The continuity setup can create a local `.agent-continuity/` folder when you run the setup flow. It should ask where user notes or diary files belong instead of inventing a private memory location silently.

For details, see:

- `continuity/CLAUDE.md`
- `continuity/skills/s6-setup.md`
- `continuity/templates/`

---

## 6. Treat defense as a separate installation

The `defense/` module is the most security-sensitive part.

Do not assume it is active just because the files exist. For Claude Code, the hard defense layer requires local hooks, and hook scripts are environment-specific.

Before relying on defense:

1. Read `INSTALL.md`.
2. Read `defense/TEST.md`.
3. Install hooks for your environment.
4. Verify that the expected defense reminder appears.

If the defense reminder does not appear, stop and fix the setup before trusting the module.

---

## 7. Use the weekly health check

After installing more than one module, run the watchdog weekly check manually:

```text
Read `agent-guardrails/watchdog/CLAUDE.md` and run the weekly module health check.
Report missing files, inactive triggers, stale continuity records, and untested hooks.
```

The watchdog checks whether the framework is wired together. It does not prove that every answer is correct.

---

## First-run checklist

- [ ] Repository copied into the project.
- [ ] Minimal trigger table added to the project instruction file.
- [ ] One quality scan completed before final delivery.
- [ ] One review scan completed on a finished output.
- [ ] Continuity setup used only if long-session memory is needed.
- [ ] Defense hooks installed and tested before relying on prompt-injection protection.
- [ ] Watchdog health check run after multi-module setup.

---

## Next steps

- Read `INSTALL.md` for full installation details.
- Read module-level `CLAUDE.md` files before using each module.
- Try the starter workflows in `examples/`.
- Start small, verify behavior, then add more automation.
