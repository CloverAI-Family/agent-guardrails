# Skill 6: First Setup

Part of the agent-guardrails package.

Initialize the continuity module for a new user or a new workspace.

## When to use
- No `.agent-continuity/` root exists
- No user profile exists in `.agent-continuity/user/`
- User explicitly asks to set up the continuity module

## Steps

### Step 1: Display startup message
```text
   Continuity Module

East is guarded.
```

### Step 2: Show status
```text
+=====================================+
|  agent-guardrails                   |
|  [continuity OK] [quality     -]    |
|  [defense    -] [review       -]    |
|  [watchdog   -]                     |
|                                     |
|  East is guarded.                   |
+=====================================+
```

If other modules are already installed, show their status as OK instead of `-`.

### Step 3: Gather user info — check before asking

First check sources already available to this AI (project shared layer,
member directory, existing memory or profile files within permitted scope).

- For each profile field, if a reliable answer already exists, use it and
  note its source in the profile.
- Ask the user ONLY the questions whose answers cannot be found:
  1. What should I call you?
  2. What is your main field of work or study?
  3. What will you primarily use AI for?
- If all three are answerable from existing sources, ask nothing and
  tell the user the profile was built from known records.

### Step 4: Create the directory structure

Create:
- `.agent-continuity/user/`
- `.agent-continuity/dialogues/` (archive zone — old legacy zone)
- `.agent-continuity/dialogues/_quarantine/`
- `.agent-continuity/dialogues/compression_manifests/`
- `.agent-continuity/checkpoints/`

### Step 5: Confirm or create member diary folder (new step)

Ask the member: where is your diary folder? (If it already exists, confirm the path; if not, suggest creating one.)
Record the path in `.agent-continuity/user/default.md` under a "Diary folder" field.
(Diary folder path is per-machine per-member — do not hardcode it in the skill file.)

### Step 6: Create starter files

- Create `.agent-continuity/user/default.md` from `templates/user_profile.md`
- Create `.agent-continuity/dialogues/archive_index.md` from `templates/archive_index.md`

### Step 7: Optional git initialization

If git is available and the user wants version tracking:
`git init && git add -A && git commit -m "agent-continuity: East is guarded"`

If git is unavailable, skip this step and continue.

> All writes must follow defense module g1/g3 rules and platform permissions; do not cross the maintainer's authorization or workspace boundaries.

### Step 8: Completion message

After setup, confirm:
`Your memory is now guarded.`

If the user's environment includes other agent-guardrails modules, you may mention them.
If the continuity module is installed standalone, do not imply that other modules are required.

---


