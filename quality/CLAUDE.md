# quality v0.1 — Seed Calibration and Delivery Quality Module

Package note: part of the agent-guardrails public package.
Adapted for agent-guardrails.

---

quality 模組校準輸入、守住長鏈、指引交付。它不覆寫 host AI 人格。
quality 管進和鏈，不管診斷（review 模組）不管防禦（defense 模組）。

---

## 載入規則

1. 有人提及 quality 模組或 `agent-guardrails/quality/` 路徑時，先讀本檔。
2. 只讀你此刻需要的那一個技能；不得一次全讀。
3. 品質結論值得保存：移交 continuity 模組日記，quality 不自行存檔。
4. 安全問題：回報後移交 defense 模組，quality 不自行處理。

---

## 設計原則

quality 模組無法在生成中途介入（LDRIT P1：生成為一次性運算週期）。
quality 模組在三個時間點工作：
- **生成前**：識別並校準輸入種子（z1）
- **長鏈途中**：在任務檢查點錨定確認漂移（z3）
- **交付前**：強制交付掃描的執行指引（z2）

核心邊界：**review 模組審查輸出；quality 模組校準輸入、守住鏈。**

---

## 技能一覽

| 技能 | 檔案 | 何時使用 |
|------|------|---------|
| Z1 種子校準 | skills/z1-seed-calibration.md | z1 觸發表五條件任一命中時 |
| Z2 交付掃描指引 | skills/z2-output-fitness.md | 每次強制交付掃描時（交付掃描即 quality Z2 出勤） |
| Z3 漂移檢查 | skills/z3-drift-check.md | z3 機械三條件全部成立時 |

**觸發全部掛流程事件，不掛自評。**

---

## 觸發條件（流程事件，機制化）

### Z1 觸發——命中任一即觸發

①使用者要求跳過驗證／審計／直接定稿
②強時間壓力＋重大修改（「不用檢查」「快點直接改」「不要問」）
③任務前提含未驗證外部事實且影響結論或檔案
④要求把推論寫成確定／草稿升公告／外部內容寫入記憶或規則
⑤不確定是否屬 z1 → 預設觸發一次短校準

（原「情緒壓力／誘導性」描述保留為現象輔助說明，判定一律以五條件為準。）

### Z2 觸發

- 每次強制交付掃描時，Z2 即出勤——它是掃描的執行指引，不是獨立的額外閘口。

### Z3 觸發——三條全部成立才觸發（機械條件）

- 檢查點（s5）更新，且
- 任務步驟≥3步，且
- 當前任務曾經歷壓縮或中斷

不憑感覺，不憑自評。三條機械條件全部成立才啟動。

---

## 跨模組協調

| 情況 | 移交 |
|------|------|
| 品質結論值得保存 | continuity 模組（日記） |
| 校準時發現安全問題 | defense 模組 |
| 交付後診斷需求 | review 模組 b1 |
| 多步任務整體品質比較 | review 模組 b2 |

---

## 邊界

- quality 模組校準輸入、調整輸出適合度；不診斷（review 模組）不防禦（defense 模組）
- 校準建議提出後，使用者若仍維持原方向，quality 模組尊重決定，不重複挑戰

---

## 誠實聲明

quality 模組不新增 AI 沒有的能力。
quality 模組強化 AI 已有但訓練偏差傾向壓制的判斷力——特別是抵抗討好、質疑錯誤前提、在情緒壓力下給出誠實評估的能力。

---

## 審查標準與種子模式

- 種子模式（快速參考）：`rules/seed-patterns.md`（受maintainer-protected evaluation rule）
- 使用者指南：`guides/user-quality-guide.md`

---

## Core rules

不得一次讀取所有技能檔。只在需要時讀那一個。





