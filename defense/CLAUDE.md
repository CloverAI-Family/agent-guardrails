# defense v0.1 — 防禦模組（defense）

Part of the agent-guardrails package.

防禦模組是安全技能模組。它不控制 AI，只提供防禦程序。
本檔是入口，先讀這份，再依需要讀對應技能。

## 入口規則

1. 若使用者提到 defense 或 `agent-guardrails/defense/` 路徑，先讀本檔。
2. 若 MEMORY.md 或 CLAUDE.md 引用 defense，在任何聯網動作前先讀本檔。
3. 聯網前（WebSearch、WebFetch、任何聯網工具）：先讀 `skills/g2-mode-switch.md`。
4. 只讀當下需要的那一個技能，不要一次全讀。

## 技能清單

| 技能 | 檔案 | 觸發時機 |
|------|------|---------|
| 系統守衛 | skills/g1-system-guard.md | 任何高風險動作前 |
| 聯網模式切換 | skills/g2-mode-switch.md | 切換離線/聯網時 |
| 記憶保護 | skills/g3-memory-protect.md | 寫入記憶或 agent-continuity 檔案前 |
| 跨實例檢查 | skills/g4-cross-check.md | 讀取其他 AI 實例寫的檔案時；**讀取跨實例信件時** |
| 自動任務守衛 | skills/g5-auto-task-guard.md | AI 自主執行多步任務時 |
| 外部內容檢疫 | skills/g6-external-quarantine.md | 引入外部技能/工具/網路內容/圖片/外部 repo 時 |

## 使用者指南

給人類讀的防禦指南：`guides/user-defense-guide.md`

## 設定

路徑與受保護路徑設定：`config/paths.md`（每機自設，本套件不附預設值——請依實際環境建立）

## 威脅清單

已知威脅模式（v2，含新增五類）：`rules/threat-patterns.md`

## hooks 位置

Active hook scripts：`~/.claude/hooks/`（不在本模組資料夾內，安裝說明見 INSTALL.md）
觸發驗證規程：`defense/TEST.md`

## 規則

只讀當下需要的技能。不要一次全讀。





