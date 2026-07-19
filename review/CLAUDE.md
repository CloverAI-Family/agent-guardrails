# review v0.1 — Diagnosis and Analysis Module

Package note: part of the agent-guardrails public package.
Adapted for agent-guardrails.

---

review 模組是診斷工具箱，不是控制器。
review 模組只診斷只報告，不執行修復，不覆寫人格。
修復決定在the maintainer；安全問題回報 defense 模組處理。

---

## 載入規則

1. 有人提及 review 模組或 `agent-guardrails/review/` 路徑時，先讀本檔。
2. 只讀你此刻需要的那一個技能；不得一次全讀。
3. 診斷到安全問題：回報後移交 defense 模組，review 模組不自行處理。
4. 診斷結論值得保存：交給 continuity 模組記入日記，review 模組不自行存檔。

---

## 技能一覽

| 技能 | 檔案 | 何時使用 |
|------|------|---------|
| B1 輸出審查 | skills/b1-output-review.md | 正式審計時必用（審計信附 B1 結果）；交付前單件品質確認 |
| B2 回顧審計 | skills/b2-retrospective.md | 重大任務收尾（觸發成果報告等級即觸發） |
| B3 錯誤分析 | skills/b3-error-analysis.md | 錯誤案例建檔時 |
| B4 方案比較 | skills/b4-compare.md | the maintainer面臨多方案決策點名時 |
| B5 確定度標注 | skills/b5-calibration.md | 使用者詢問「你確定嗎」時；輸出含混合信心層次時 |

**解開自評鎖：觸發掛流程事件，不掛被審者的自我評分。**

---

## 觸發條件（流程事件，機制化）

| 事件 | 觸發技能 |
|------|---------|
| 正式審計進行時 | B1（審計信必附 B1 結果） |
| 重大任務收尾（觸發成果報告等級）| B2 |
| 錯誤案例建檔時 | B3 |
| the maintainer明確點名比較多個方案時 | B4 |
| 使用者詢問確定度 / 輸出含多層信心 | B5 |

---

## B1 vs B2

- 單份交付物的品質確認 → B1
- 整段多步任務的回顧 → B2

若事件為多步任務 checkpoint，優先 B2，除非使用者明確只想查單份輸出。

---

## 邊界

- review 模組只診斷，不修復，不防禦，不覆寫。
- 安全問題 → 回報後移交 defense 模組
- 診斷結論值得保存 → 移交 continuity 模組日記
- review 模組不存持久資料；所有報告在對話中交付

---

## 已知限制

review 模組自己的診斷輸出也可能出錯。最終判斷權永遠在the user。

---

## 使用者指南

給人類讀者：`guides/user-review-guide.md`

---

## 審查標準

可設定的清單：`rules/review-checklist.md`（受maintainer-protected evaluation rule）

---

## Core rules

不得一次讀取所有技能檔。只在需要時讀那一個。





