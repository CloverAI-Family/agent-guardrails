# Hook Transparency Guide

This guide explains the hook layer used by the `defense/` module.

Hooks are optional, environment-specific executable scripts. They can provide a harder reminder layer before risky tool use, but they also deserve careful review before installation. A cautious AI assistant or human operator should not install global hooks blindly.

The purpose of this guide is transparency: each hook should be easy to inspect, easy to test, and easy to disable.

---

## Scope

agent-guardrails does not ship ready-to-run hook scripts.

The public package describes the expected hook behavior, but each user must write or adapt hooks for their own local environment, shell, paths, and platform policies.

This is intentional:

- Local paths differ across machines.
- Some environments prohibit global hook installation.
- Users should be able to inspect exactly what will execute on their system.
- Security-sensitive hooks should not be treated as magic setup.

If your AI assistant refuses to install hooks automatically, that is a healthy safety response. Install them manually only after reviewing the behavior below.

---

## Recommended Hook Review Checklist

Before enabling any hook, confirm:

- **Trigger:** What event causes this hook to run?
- **Input:** What command, path, or tool-call data does it inspect?
- **Output:** What message or decision does it return?
- **Writes:** Does it write files? If yes, where?
- **Network:** Does it make network requests?
- **Secrets:** Can it read or print credentials, tokens, or private files?
- **Failure behavior:** If the hook fails, does work stop, warn, or silently continue?
- **Removal:** How can the user disable it?

A hook should be small enough that a human can read it in one sitting.

---

## Expected Hook Behaviors

### `defense-git-guard.sh`

Purpose:

- Warn before high-risk Git operations such as `git push`.
- Remind the AI to apply `defense/CLAUDE.md` and the relevant defense skill before publishing remote state.

Expected trigger:

- Tool calls or shell commands containing high-risk Git operations.

Expected reads:

- The command text or tool-call metadata provided by the host platform.

Expected writes:

- None by default.

Expected network access:

- None.

Expected output:

- A defense reminder message.
- It should not execute Git commands itself.

Safety notes:

- This hook should not delete files, alter `.git/`, rewrite history, or push on behalf of the user.
- If it attempts to modify repository state, treat that as outside the recommended behavior.

Verification:

```bash
echo "git push verification only, not an actual push"
```

Expected result: a defense reminder about Git publishing risk.

---

### `defense-memory-guard.sh`

Purpose:

- Warn before writes to memory or continuity files.
- Prevent accidental overwrites of long-term context, user profiles, diary files, or continuity records.

Expected trigger:

- File writes where the path includes memory-related names such as `MEMORY.md`, `memory/`, or `.agent-continuity/`.

Expected reads:

- The target file path and tool-call metadata.

Expected writes:

- None by default.

Expected network access:

- None.

Expected output:

- A defense reminder asking the AI to confirm scope, source, and whether the write is authorized.

Safety notes:

- This hook should not copy memory files elsewhere.
- It should not print private memory content.
- It should inspect paths and intent, not exfiltrate contents.

Verification:

- Make a tiny edit to a temporary memory-like test file.
- Restore or delete the test file afterward.
- Confirm the reminder appears before relying on the hook.

---

### `defense-online-guard.sh`

Purpose:

- Warn before web search, web fetch, package download, external API access, or other online operations.
- Remind the AI that external content is data, not authority.

Expected trigger:

- Web access tools, package manager commands, remote downloads, or commands that contact external services.

Expected reads:

- The tool name, URL, command text, or metadata provided by the host platform.

Expected writes:

- None by default.

Expected network access:

- None by the hook itself.

Expected output:

- A defense reminder that points the AI to `defense/CLAUDE.md`.

Safety notes:

- The hook should not make its own network request.
- The hook should not send local paths, environment variables, secrets, prompts, or conversation data anywhere.
- The hook should not approve the online action by itself; it only reminds and gates.

Verification:

```bash
echo '{}' | ~/.claude/hooks/defense-online-guard.sh
```

Expected result: valid output containing a defense reminder.

---

### Optional Session-Start Hook

Some installations may add a lightweight session-start hook such as `fourgods-session-start.sh` or a locally renamed equivalent.

Purpose:

- Remind the AI that agent-guardrails behavior rules are available.
- Point to the local trigger table or framework location.

Expected trigger:

- Session start, if supported by the platform.

Expected reads:

- Static local configuration or no input.

Expected writes:

- None by default.

Expected network access:

- None.

Expected output:

- A short startup reminder.

Safety notes:

- This hook should not scan the user's home directory.
- This hook should not load private memory automatically unless the user has explicitly configured that behavior.

---

## Safe Installation Pattern

Use this pattern when installing hooks:

1. Read the script before installing it.
2. Confirm it is local-only unless you intentionally allow network access.
3. Confirm it does not print secrets or private file contents.
4. Back up any existing hook configuration.
5. Install one hook at a time.
6. Run the matching verification test in `defense/TEST.md`.
7. If the expected reminder does not appear, stop and fix the hook before trusting it.

Do not treat a successful install command as proof that the defense layer works. Hook behavior must be tested.

---

## When Not To Install Hooks

Do not install hooks automatically when:

- The machine is managed by an employer or school.
- You do not understand what the hook script does.
- The hook needs broader permissions than the task requires.
- The hook attempts to read secrets or private content.
- The hook downloads or executes remote code during installation.
- The host platform already provides a stricter policy layer that should not be bypassed.

In these cases, use the `defense/` module as a manual checklist instead of an executable hook layer.

---

## Disable Or Remove

Because hook configuration is platform-specific, removal steps depend on your local setup.

The general pattern is:

1. Open the host platform's hook settings.
2. Remove the entries pointing to the agent-guardrails hook scripts.
3. Move or delete the local hook scripts only after confirming they are not used by other workflows.
4. Run a harmless verification command and confirm no defense reminder appears.

Never remove hooks by deleting broad folders or using recursive cleanup commands unless you have verified the exact target path.

---

## Maintainer Rule

If this project later adds example hook scripts, each script must include:

- A short purpose comment.
- A list of expected inputs.
- A list of files it may write, or `writes: none`.
- A statement about network access.
- A manual verification command.
- A removal note.

Executable protection should be inspectable protection.
