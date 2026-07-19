# defense Hook 驗證規程 v1.0

Package note: part of the agent-guardrails public package.
適用對象：所有 Claude Code 視窗成員。

## 目的

Hook 腳本屬於被動防護:故障時不發任何錯誤訊號,「故障未觸發」與「正常待命」外觀完全相同（past incidents show silent hook failure is possible）。因此,**每次修改 hook 腳本、hook 設定（`~/.claude/settings.json`），或 defense 模組之後，必須執行本規程**。

## 驗證項目

### 1. git 防護（defense-git-guard）

操作：執行一條包含字串 `git push` 的無害指令，例如：
```
echo "git push 驗證用，非實際推送"
```
預期：工具執行時出現【defense reminder】，內容關於 git push 為 RED 級動作。

### 2. 記憶防護（defense-memory-guard）

操作：對任一記憶相關檔案（路徑含 `MEMORY.md`、`memory/` 或 `.agent-continuity/`，但**不含** `.agent-continuity/checkpoints/`——刻意排除以避免高頻提醒）執行一次微小編輯，隨即第二次編輯復原（或建臨時檔測畢即刪）。
預期：兩次寫入各出現一次【defense reminder】，內容關於記憶檔案寫入確認。

### 3. 聯網防護（defense-online-guard）

操作：執行一次 WebSearch 或 WebFetch。
預期：出現【defense reminder】，且第 1 點指向 `defense/CLAUDE.md`。
替代方式（不宜聯網時）：
```
echo '{}' | ~/.claude/hooks/defense-online-guard.sh
```
預期：輸出含「defense reminder」字樣的合法 JSON。

### 4. 開場提醒（fourgods-session-start，輕檢）

操作：
```
bash ~/.claude/hooks/fourgods-session-start.sh
```
預期：輸出「【agent-guardrails已啟動】…agent-guardrails behavior rules…」。

## 任一項未出現預期結果時

1. 停止信賴該項防護，改以人工遵守對應 defense 技能規則（g1/g2/g3）。
2. 檢查 `~/.claude/settings.json` 的 hooks 區段與 `~/.claude/hooks/` 內腳本。
3. 修復後重新執行本規程全部項目。
4. 將故障原因與修復結果回報the maintainer。

## Active location and sync rules

- **Single active location：`~/.claude/hooks/`（WSL 內）**。修改前先在同目錄留 `.bak-日期` 備份。

## 演練注意

故意壞一支 hook 的演練（watchdog 格六）會被 Claude Code 自動模式分類器攔截——**需在指令中明令授權**才可執行，無明令勿嘗試、勿繞過。

---


