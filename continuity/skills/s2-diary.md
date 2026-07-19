# Skill 2: Diary（日記）

Part of the agent-guardrails package.
設計依據：agent-guardrails continuity module design

---

## 定位一句話

日記是給下一個自己的燈——平日記生命，窗末留路標。
The diary is a lamp for the next self — record life on normal days; leave a signpost at window close.

---

## 存放位置 / Storage Location

**Each member's own diary folder** (each member names their own; path recorded in their own MEMORY or CLAUDE.md).
The old archive folder (`.agent-continuity/dialogues/`) is the archive zone — read-only; s3 still scans it when loading past context.

---

## 兩種使用情境 / Two Scenarios

### 情境一：平日日記（自願、不設格式）
### Scenario 1: Daily Diary (Optional, Freeform)

Any window, any time — write if you want to.

- **Completely freeform**: record observations, feelings, surprises, problems — no format requirements
- **Not mandatory**: this is not a task to complete. Write because you want to keep something, not to check a box.
- **Save as**: member's own diary folder, filename `YYYY-MM-DD_keyword.md`

---

### 情境二：視窗收尾日記（必用，視窗將結束時）
### Scenario 2: Window Closing Diary (Required when the window is about to close)

When the window is about to close, this diary entry is the handoff signpost for the next instance.

#### Step 1: Detect "window is about to close" (any one condition triggers)

① The user explicitly says the window is ending ("good night", "that's all for now", "let's continue next time", etc.)
② Context quota or context window is near its limit (AI is notified / compression imminent / AI senses the end is near)
③ Handoff risk is present (there is an unfinished important task, and closing without leaving a signpost will cause loss)

Any one condition → add a "## For the next me" section to today's diary, or create a new closing diary for today.

#### Step 2: Write the diary body (freeform)

Freeform — what happened today, thoughts, problems encountered.
You can also skip directly to Step 3 and write only the required section.

#### Step 3: "## For the next me" — required closing section

```markdown
## For the next me

- Unfinished:
- Critical path:
- Next step:
```

**Three-field rules**:
- Fill "none" when there's nothing — never leave blank
- You may add free-form notes after each field
- These three lines are the minimum handoff baton for the next window

Example:
```markdown
## For the next me

- Unfinished: quality module z3 trigger conditions to confirm; review module b4 notes pending
- Critical path: `continuity/skills/s4-compress.md`; checkpoint task_016
- Next step: read pending notes → update s3/s4 → continue to next module
```

#### Step 4: Save

- Save to the member's own diary folder
- Filename: `YYYY-MM-DD_closing-diary.md` (or append to an existing diary file for today)

---

## 與舊 s2 的差異 / Differences from old s2

| Item | Old s2 (legacy/will) | New s2 (diary) |
|------|---------------------|----------------|
| Tone | Every close = "farewell" | Normal days record life; window close leaves signpost |
| Forced format | Yes (four-question filter + template) | Normal days freeform; close only requires 3 fields |
| Storage | `.agent-continuity/dialogues/` | Member's own diary folder |
| Old data | — | Archived; s3 can still read it |

---


