# Installation Guide

agent-guardrails requires three steps to become active.

---

## Step 1: Copy the module folder

Copy the `agent-guardrails/` folder into your project root or a shared skills directory accessible to your AI.

```
your-project/
└── agent-guardrails/
    ├── defense/
    ├── continuity/
    ├── quality/
    ├── review/
    └── watchdog/
```

You may install all five modules or only the ones you need.
Each module is independently functional.

---

## Step 2: Install hooks (defense module only)

The defense module's hard protection layer uses Claude Code hooks.
These are shell scripts that intercept tool calls before they execute.

Hook scripts are **not included** in this package — they depend on your local environment paths.
You will need to write them yourself based on the patterns in `defense/TEST.md`.

To install:

1. Create your hooks directory: `~/.claude/hooks/`
2. Write three scripts:
   - `defense-git-guard.sh` — intercepts `git push` and related commands
   - `defense-memory-guard.sh` — intercepts writes to MEMORY.md, memory/, .agent-continuity/ files
   - `defense-online-guard.sh` — intercepts internet access tools
3. Register the hooks in your Claude Code hooks configuration (`.claude/settings.json` or equivalent)
4. Run the verification test described in `defense/TEST.md`

**If the expected [defense reminder] message does not appear after installation, stop and fix before trusting the defense module.**

---

## Step 3: Wire up the trigger table

The five modules activate via trigger events described in `trigger_events_protocol.md`.

For Claude Code users:
- Add a reference to `agent-guardrails/defense/CLAUDE.md` in your project's CLAUDE.md
- Or copy the relevant trigger table into your CLAUDE.md

The trigger table tells the AI which module to load for which situation. Without it, the AI will not automatically invoke the modules.

Minimal trigger table (add to your CLAUDE.md):

```markdown
## agent-guardrails triggers

- **git push / online access / memory writes** → read `agent-guardrails/defense/CLAUDE.md`
- **Multi-step tasks (3+ steps)** → read `agent-guardrails/continuity/CLAUDE.md`, run s5-checkpoint
- **Deliverable / file modification / handoff risk** → attach delivery scan (quality Z2)
- **Window closing / context full** → read `agent-guardrails/continuity/CLAUDE.md`, run s2-diary
- **Output quality check** → read `agent-guardrails/review/CLAUDE.md`, run B1 or B2
- **Weekly** → read `agent-guardrails/watchdog/CLAUDE.md`, run weekly check
```

---

## Verification

After setup, run the watchdog weekly check once manually to confirm all modules are present and hooks are active.

See `watchdog/CLAUDE.md` for the six-cell weekly check procedure.

---

## Module-only installation

If you only need specific modules:

| You want | Install |
|----------|---------|
| Prompt injection protection | `defense/` + hooks |
| Memory persistence across sessions | `continuity/` |
| Anti-sycophancy + delivery scan | `quality/` |
| Output diagnosis and retrospectives | `review/` |
| System health monitoring | `watchdog/` |

Modules that reference each other (e.g., quality says "hand off to continuity for storage") will still function if the referenced module is absent — they just won't have the other module available for handoff.





