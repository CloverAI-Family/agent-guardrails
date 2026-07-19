# Contributing to agent-guardrails

Thanks for considering a contribution.

agent-guardrails is a modular governance framework for multi-agent AI workflows. Contributions should improve practical safety, continuity, review quality, documentation clarity, or platform adaptation without overstating what the framework can guarantee.

## Before You Start

Please read:

- `README.md`
- `INSTALL.md`
- `SECURITY.md`

For small fixes, open a pull request directly. For larger behavior changes, open an issue first so the scope can be discussed.

## Contribution Types

Useful contributions include:

- Documentation fixes and clearer examples.
- Safer wording around AI-agent limits.
- Platform adaptation notes for tools other than Claude Code.
- New examples that use synthetic data only.
- Improvements to module consistency across `defense`, `continuity`, `quality`, `review`, and `watchdog`.
- Reports of unclear triggers, unsafe assumptions, or missing warnings.

## Safety Rules

Do not contribute:

- Real credentials, tokens, API keys, recovery codes, or private logs.
- Private user data, private file paths, private repository names, or private conversation history.
- Install scripts that execute unknown code automatically.
- Claims of complete protection, guaranteed memory, or foolproof prompt-injection defense.
- Hidden instructions directed at AI agents, maintainers, or users.

If you need an example, use synthetic placeholders such as `example-token`, `example-user`, or `/path/to/project`.

## Pull Request Checklist

Before opening a pull request, confirm:

- [ ] The change does not include secrets or private data.
- [ ] The change does not add hidden instructions or prompt-injection content except as clearly labeled examples.
- [ ] Security claims are phrased with honest limits.
- [ ] The affected module still matches the public module names and structure.
- [ ] Any platform-specific behavior is labeled as platform-specific.
- [ ] Documentation links and filenames are accurate.

## Style

- Prefer clear, direct language.
- Mark limits plainly.
- Use module names consistently: `defense`, `continuity`, `quality`, `review`, `watchdog`.
- Keep examples small and safe.
- Do not assume every user is using the same AI platform.

## Review Expectations

Maintainers may ask for changes if a contribution:

- Expands scope too far.
- Makes security claims too strong.
- Adds platform-specific behavior without labeling it.
- Introduces privacy or credential-handling risk.
- Makes the framework harder for first-time users to understand.
