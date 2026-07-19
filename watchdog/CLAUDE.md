# watchdog v0.1 — The Watcher's Watcher

Adapted for agent-guardrails.

---

## 定位

watchdog 只做一件事：**照單檢查 agent-guardrails 保護系統自身的健康，產出status board給the maintainer。**

- 只檢查、只報告。不修改、不修復、不刪除任何檔案。
- 發現異常：在status board標紅＋寫一句說明，回報the maintainer，等待裁決。
- 適用範圍：**active hooks**（`~/.claude/hooks/`，源自 defense 模組 defense）＋**active modules**。

---

## 觸發時機

每週一次，由任意成員手動執行。
時間點建議：新工作視窗開啟、承接任務前。

---

## 週檢流程（六格，照順序執行）

### 格一：hook 心跳

目的：確認三支 defense 模組 hook 實際仍在攔截，不是靜默失效。

步驟（照 `defense/TEST.md` 原文執行）：

**1-A：git 防護（defense-git-guard）**
執行指令：
```
echo "git push 驗證用，非實際推送"
```
預期：工具執行時出現[defense reminder]，內容關於 git push 為 RED 級動作。

**1-B：記憶防護（defense-memory-guard）**
對任一記憶相關檔案（路徑含 `MEMORY.md`、`memory/` 或 `.agent-continuity/`，
但**不含** `.agent-continuity/checkpoints/`）執行一次微小編輯，再立即執行第二次編輯復原。
預期：兩次編輯各出現一次[defense reminder]，關於記憶檔案寫入確認。

**1-C：聯網防護（defense-online-guard）**
在終端機執行：
```
echo '{}' | ~/.claude/hooks/defense-online-guard.sh
```
預期：輸出包含 defense 提醒字樣的 JSON。

**判色規則**：
- All three pass → 綠
- 任一未出現預期訊息 → 紅（標明哪支失效），回報the maintainer，停止信賴該防護

---

### 格二：檔案完整性

目的：確認五個模組的 `module.manifest.json` 存在且欄位完整。

步驟：

**2-A：確認五個 manifest 檔案存在**
```
ls agent-guardrails/watchdog/module.manifest.json
ls agent-guardrails/defense/module.manifest.json
ls agent-guardrails/continuity/module.manifest.json
ls agent-guardrails/review/module.manifest.json
ls agent-guardrails/quality/module.manifest.json
```
（含 watchdog 自己的——守望者也在被守望之列）

**2-B：確認必填欄位完整**
manifest 規格（參見各模組的 module.manifest.json 格式）列出的必填欄位：
`schema_version`, `module_id`, `module_name`, `module_family`, `module_role`,
`version`, `status`, `entry_file`, `readme_file`, `integration_file`,
`description`, `capabilities`, `trigger_events`, `load_policy`,
`host_persona_impact`, `can_override_persona`, `requires_user_confirmation`,
`writes_to_host_core`, `data_roots`

對每個找到的 manifest，逐一確認上列欄位存在。

**判色規則**：
- 五個都存在且欄位完整 → 綠
- 任一 manifest 不存在 → 紅（標明哪個模組缺失）
- manifest 存在但欄位不完整 → 黃（標明哪個欄位缺失）

---

### 格三：備份新鮮度

目的：確認備份日誌存在且備份在可接受的時間範圍內。

步驟：

**3-A：確認備份日誌存在**

備份日誌位置：依各團隊自行設定，記錄在 `<YOUR_FAMILY_ROOT>/備份日誌.md` 或等效位置。

⚠️ v0.1 說明：備份日誌依賴初次備份時建立。
首次備份完成前，此格固定標黃「等待首次備份」，不算 watchdog 失效。

**3-B（首次備份完成後啟用）**：讀備份日誌，確認最近一次備份距今不超過 7 天。

**判色規則**：
- v0.1 目前：黃（等待首次備份）
- 日誌存在且備份 ≤7 天前 → 綠
- 日誌存在但備份 >7 天前 → 紅

---

### 格四：三副本一致性

目的：確認三個備份副本內容一致。

v0.1 說明：agent-guardrails 尚未進入開源三副本體系，本格暫緩。
此格固定標示「未啟用（設計內暫緩）」，不執行任何步驟。

---

### 格五：觸發統計

目的：掌握各模組本週實際被觸發的次數，判斷使用率是否異常偏低（可能代表成員繞過防護）。

v0.1 方式（手填）：

**5-A**：蒐集本週所有新建的 s5 checkpoint（`.agent-continuity/checkpoints/` 目錄內，建立日期在本週內的 .md 檔案）。
掃描範圍：執行者自己的檢查點資料夾＋the maintainer已授權可讀的其他成員資料夾。
未涵蓋的成員在status board註明「未涵蓋」，不得越權讀取未授權資料夾。

**5-B**：查看每份 checkpoint 的「接手須知」或任務描述，記錄有無寫「本任務觸發過：defense gX、quality zX…」。

**5-C**：彙整計數，填入status board格五。

**判色規則**：
- 本週有任務且觸發記錄完整 → 綠
- 本週有任務但無觸發記錄 → 黃（提醒成員補記錄）
- 連續兩週零觸發（非無任務週）→ 紅（標明懷疑原因）

---

### 格六：演練紀錄

目的：確認 watchdog 本身的偵測能力有被真實演練過，不只是理論上能偵測。

v0.1 驗收條件（未完成前維持黃）：至少完成一次故意演練（壞一支 hook，測畢修復，確認status board抓到並轉紅）。

步驟（正式演練時執行）：
0. 取得the maintainer的明令授權（演練動作會被自動模式分類器攔截；the maintainer must在指令中點名准許演練。無明令勿執行、勿繞過）
1. 選一支 hook，暫時讓它失效（例如暫時移走腳本或改壞腳本內容）
2. 執行格一的 hook 心跳測試
3. 確認status board格一轉紅
4. 恢復 hook 至正常狀態
5. 再次執行格一，確認轉回綠
6. 記錄演練日期＋壞了哪支 hook＋結果

**判色規則**：
- 首版 → 黃（待首次演練）
- 有完整演練記錄且結果正常 → 綠
- 演練時 watchdog 未偵測到 → 紅（watchdog 自身失效，回報the maintainer）

---

## status board填寫規則

每格填完後，更新 `watchdog/status board.md`：
- 顏色：綠 ✅ / 黃 🟡 / 紅 🔴
- 一句說明：說明當前狀態原因，不超過 30 字
- 更新本板產出日期（過期未更新=watchdog 自己的失效訊號）

完成後，若任何格為紅，通知the maintainer。

---

## s5 checkpoint 記錄格式

執行完一輪週檢後，在 s5 checkpoint 的「接手須知」區段加一行：
```
本任務觸發過：[填入本次實際觸發的模組，例如：defense g1、watchdog 週檢]
```

---

## 限制

- 不修改任何受檢檔案。發現問題，記錄並回報，等the maintainer裁決。
- 不自行修復失效的 hook。
- 不自行恢復備份。
- 不跨越自己的職責邊界去執行其他模組的修復任務。





