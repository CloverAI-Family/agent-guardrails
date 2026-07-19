# Platform adaptation guide

agent-guardrails was developed and tested on Claude Code, but the concepts can be adapted to other AI coding or agent platforms.

This guide explains what must change when you use the framework outside its original platform.

The short version: keep the governance concepts, but do not assume triggers, hooks, memory files, or permission prompts work the same way everywhere.

---

## What is portable

These parts are usually portable:

- Module roles: `defense`, `continuity`, `quality`, `review`, and `watchdog`
- Trigger thinking: load the smallest guardrail that matches the risk
- Evidence labels: confirmed, inferred, unknown, and risk
- Continuity records: checkpoints, diary entries, handoff notes, and archive indexes
- Review patterns: output review, retrospective, comparison, and error analysis
- Safety boundaries: least privilege, privacy minimization, and human approval for irreversible actions

These concepts can be adapted as plain instructions even when a platform has no hook system.

---

## What is platform-specific

These parts must be checked on each platform:

- Where project instructions live
- Whether the AI can automatically read module files
- Whether hooks or pre-tool interceptors exist
- Whether file writes require user confirmation
- Whether web access is available and how it is approved
- Whether memory files can be written safely
- Whether Git operations run inside the agent environment or an external shell
- Whether subagents can provide verifiable evidence or only summaries

Do not copy a trigger table blindly. First map the platform's real capabilities.

---

## Adaptation checklist

Before using agent-guardrails on a new platform, answer these questions:

| Question | Why it matters |
|----------|----------------|
| Where do persistent project instructions live? | Trigger tables must be visible to the agent. |
| Can the agent read files on demand? | Module files are not active unless the agent can load them. |
| Are tool calls intercepted before execution? | Defense hooks require real enforcement, not just reminders. |
| Can the user approve or deny risky actions? | Human approval is the hard boundary for irreversible work. |
| Where should checkpoints be stored? | Continuity should not invent a private memory location silently. |
| How are Git operations performed? | Some environments leave background Git processes or hide staging state. |
| How are secrets protected? | Examples and logs must avoid tokens, keys, and private data. |
| How are outputs verified? | "Looks good" is not a review result. |

If a question cannot be answered, mark that area as unverified.

---

## Suggested adaptation process

### 1. Start with documentation-only use

First, copy only the module files and read them manually.

Do not install hooks, background services, or automation until you understand the platform's permission model.

### 2. Add a small trigger table

Add a short trigger block to the platform's project instruction file.

Example:

```markdown
## agent-guardrails triggers

- Before final delivery, run `quality` output fitness.
- Before long-session handoff, write a `continuity` checkpoint.
- Before risky file, web, or Git actions, apply `defense` guidance.
- When reviewing completed work, use the smallest `review` skill that fits.
- Weekly, run the `watchdog` health check.
```

Keep the first version small. Expand it only after observing real behavior.

### 3. Test one module at a time

Use a synthetic task and verify the result.

Good first tests:

- Ask for a final answer and require a quality delivery scan.
- End a long task and require a continuity checkpoint.
- Review a small document and require an output review.

Avoid testing with private data.

### 4. Add enforcement only after verification

If the platform supports hooks or pre-tool checks, test them with harmless commands first.

For example, a defense hook should show a reminder or block condition before a risky action. If it does not appear, the defense layer is not active.

### 5. Record platform notes

Keep a short adaptation note in your project.

Minimum fields:

```markdown
# agent-guardrails platform notes

- Platform:
- Instruction file:
- Modules enabled:
- Hooks or enforcement:
- Checkpoint location:
- Git workflow:
- Known limitations:
- Last verified:
```

---

## Platform examples

### Claude Code

Claude Code can use project instruction files and local hooks.

Recommended approach:

- Put trigger references in `CLAUDE.md`.
- Use hooks only after reading `INSTALL.md` and `defense/TEST.md`.
- Treat hook behavior as unverified until the expected reminder appears.

### Codex-style coding agents

Codex-style agents may use project instruction files, skills, sandboxing, and approval prompts, depending on the environment.

Recommended approach:

- Put a minimal trigger table in the project instruction file supported by the environment.
- Keep Git work conservative if the desktop app or shell leaves background Git processes.
- Prefer evidence-based verification over agent self-report.
- Do not assume Claude Code hook paths or hook scripts apply.

### Other multi-agent tools

For agent frameworks, IDE assistants, or orchestration tools:

- Map each guardrail to the framework's real lifecycle events.
- Keep subagent reports separate from verified evidence.
- Store checkpoints in a visible project folder, not hidden memory.
- Require user confirmation before irreversible file, network, or deployment actions.

---

## Common mistakes

- Assuming files are active just because they exist.
- Treating a reminder as an enforcement boundary.
- Copying Claude Code hook paths into another platform.
- Letting continuity write private memory files without asking the user where they belong.
- Using real logs, real credentials, or private conversations as examples.
- Treating subagent completion reports as verified results.
- Expanding trigger tables until every small task becomes too heavy.

---

## Adaptation result labels

When documenting a platform adaptation, use these labels:

- **Confirmed**: tested on the platform with observable evidence.
- **Inferred**: likely based on documentation or similar behavior, but not tested.
- **Unknown**: not checked or not accessible.
- **Risk**: could cause privacy, safety, reliability, or workflow problems.

This keeps platform notes honest and prevents accidental overclaiming.

---

## Minimum successful adaptation

A minimal adaptation is successful when:

- The agent can find the module files.
- The trigger table is visible in the project context.
- At least one quality or review check produces concrete evidence.
- Continuity files go to a user-approved location.
- Risky actions still require platform or user approval.
- Limits are written down instead of hidden behind confident language.

If those conditions are not met, treat the adaptation as experimental.
