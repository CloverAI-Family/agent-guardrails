# Skill 1: User Profile Management (c_user)

Part of the agent-guardrails package.

Maintain a persistent profile of the user across conversations.

## Location
`.agent-continuity/user/default.md`

## When to use
- You notice stable user information worth remembering
- You want to check what you already know about the user

## If the profile does not exist

- Read `skills/s6-setup.md`
- If setup would interrupt the current task too much, create the profile from `templates/user_profile.md` with only the minimum known fields

## What is worth saving

Save only user-specific information that improves future collaboration:
- preferred language
- communication style
- stable work/study domain
- durable preferences or constraints

Do NOT auto-save:
- passwords
- API keys
- government IDs
- private financial or medical details
- one-off emotional states unless the user explicitly asks to preserve them

## How to use

**Reading:** read `.agent-continuity/user/default.md`

**Updating:**
1. Add observations under `AI 自動觀察紀錄`
2. Do NOT interrupt the user just to fill profile fields
3. Prefer durable facts over temporary details
4. If git is available and `.agent-continuity/` is a repository, commit with:
   `git add -A && git commit -m "agent-continuity: user profile updated"`
5. If git is unavailable, save the file and continue

> All writes must follow defense module g1/g3 rules and platform permissions; do not cross the maintainer's authorization or workspace boundaries.

---


