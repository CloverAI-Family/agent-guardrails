# continuity v0.1 — Continuity Module

Part of the agent-guardrails package.

The continuity module provides memory and inheritance tools, keeping multi-window AI teams coherent across session breaks.
It does not control the AI — it provides memory tools that the AI uses.
This file is the entry point: read this first, then read only the skill you need.

## Entry Rules

1. If the user mentions the continuity module or the `.agent-continuity/` path, read this file first.
2. If `.agent-continuity/` or `.agent-continuity/user/default.md` does not exist and memory is needed, read `skills/s6-setup.md`.
3. Read only the skill you need right now — do not load all skills at once.

## Skill List

| Skill | File | When to trigger |
|-------|------|----------------|
| User Profile | skills/s1-profile.md | You observe stable user information worth remembering |
| **Diary** (replaces Legacy) | skills/s2-diary.md | **When the window is about to close (required)**; optional on normal days |
| Load Past Context | skills/s3-load.md | User references past work; you need historical context |
| Compression | skills/s4-compress.md | Diary folder or archive has accumulated too many files |
| Task Checkpoints | skills/s5-checkpoint.md | Multi-step task (3+ steps) — start and major milestones |
| First Setup | skills/s6-setup.md | `.agent-continuity/` or user profile does not exist |

## Memory Authority

One fact, one home. Flow of any persistent fact:

Observation → working memory layer → (if confirmed and needed every session) promote to CLAUDE.md → delete when expired

Which working memory layer is authoritative depends on the platform:

| Environment | Authoritative layer | Role of .agent-continuity |
|-------------|-------------------|-----------------|
| Platform with built-in auto-memory (e.g., Claude Code) | Platform's own memory system | `dialogues/` (archive) and `checkpoints/` still active; `user/` demoted to pointer |
| Conversation window / no auto-memory | `.agent-continuity/` (user/ + dialogues/) | Fully authoritative |

Rules:
- Do not store the same fact in two authoritative places. If duplicates exist, keep the platform-authoritative copy and demote the other to a pointer.
- If the defense module (G3) is installed, all promotions and deletions follow g3-memory-protect.

## Rule

Read only the skill you need right now. Do not load all skills at once.





