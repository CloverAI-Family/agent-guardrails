# Security Policy

## Supported Versions

agent-guardrails is currently in an early public release. Security fixes apply to the default branch unless a versioned release is published later.

| Version | Supported |
|---|---|
| `main` | Yes |

## Reporting a Vulnerability

If you find a security issue, please do not post secrets, private logs, tokens, credentials, or exploit details in a public issue.

Preferred process:

1. Open a GitHub issue with a short, non-sensitive summary.
2. State which module is affected: `defense`, `continuity`, `quality`, `review`, `watchdog`, or documentation.
3. Describe the impact without including real credentials, private file paths, or user data.
4. If a proof of concept is needed, use synthetic data only.

If the issue requires private coordination, say so in the issue and provide a safe contact method without exposing secrets.

## What Counts as Security-Relevant

Security-relevant reports include, but are not limited to:

- Prompt-injection bypasses.
- Instructions that could cause secret disclosure.
- Unsafe handling of memory, diary, checkpoint, or profile files.
- Hook or trigger behavior that gives a false sense of protection.
- Documentation that encourages unsafe automation, broad permissions, or hidden actions.
- Any guidance that could cause users to paste credentials into a repository or AI conversation.

## What Not to Include

Do not include:

- API keys, personal access tokens, passwords, SSH keys, recovery codes, or session cookies.
- Real private file paths or private repository names.
- Private conversation logs unless they have been redacted.
- Instructions that require running unknown code on another user's machine.

## Scope and Limits

agent-guardrails is a documentation and workflow framework. It does not provide a complete security boundary by itself.

Some protections rely on the AI following the instructions and on the host platform enforcing permissions. Platform-level permission prompts, sandboxing, secret scanning, and human review remain important.

Please report overclaims as documentation bugs. The project should not claim that any AI-agent security problem is fully solved.
