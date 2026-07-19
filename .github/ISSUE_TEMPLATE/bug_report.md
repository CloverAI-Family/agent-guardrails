---
name: Bug report
about: Report behavior that is broken, unclear, unsafe, or inconsistent.
title: "[Bug]: "
labels: bug
assignees: ""
---

## Summary

Describe the problem in one or two sentences.

## Affected area

Which part of agent-guardrails is involved?

- [ ] `defense/`
- [ ] `continuity/`
- [ ] `quality/`
- [ ] `review/`
- [ ] `watchdog/`
- [ ] `docs/`
- [ ] `examples/`
- [ ] Other:

## What happened

Explain what happened and what you expected instead.

## Steps to reproduce

Use synthetic or redacted examples only.

1. 
2. 
3. 

## Platform

- AI tool or agent platform:
- Operating system:
- Relevant instruction file, if any:
- Modules installed:

## Evidence

Include only safe evidence:

- File names
- Redacted snippets
- Screenshots with private data removed
- Test output with secrets removed

Do not include real tokens, API keys, private paths, private logs, or private conversation history.

## Safety impact

- [ ] Documentation confusion
- [ ] Trigger did not activate
- [ ] Guardrail wording is too weak or too strong
- [ ] Possible prompt-injection handling issue
- [ ] Possible privacy or secret-handling issue
- [ ] Other:

## Additional context

Add anything else that helps maintainers understand the issue.
