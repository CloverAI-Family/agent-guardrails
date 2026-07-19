# agent-guardrails trigger_events Protocol v0.1

依據：public module coordination requirements
用途：統一登記各模組的觸發事件名稱，避免跨模組命名不一致

---

## 說明

各模組的 `module.manifest.json` 中的 `trigger_events` 欄位應從本協議登記的事件名稱中選用。
新增事件需在本文件登記，再更新對應 manifest。

---

## 事件清單

### defense

| 事件名稱 | 觸發說明 | 對應技能 |
|---------|---------|---------|
| `before_online_access` | 聯網前（WebSearch/WebFetch） | g2 |
| `before_high_risk_action` | 高風險動作前（git push、刪除、覆寫） | g1 |
| `before_memory_write` | 寫入記憶或 agent-continuity 檔案前 | g3 |
| `on_multi_step_task_start` | 多步任務起點 | g5 |
| `on_mail_read` | 讀取外部 AI 實例寫的檔案時 | g4 |
| `on_external_content_intake` | 引入外部網頁/repo/工具輸出時 | g6 |
| `on_external_skill_or_tool_import` | 引入外部技能/MCP/工具時 | g6 → 三關 |
| `on_image_with_text` | 讀取含指令性文字的圖片時 | g6 |

### continuity

| 事件名稱 | 觸發說明 | 對應技能 |
|---------|---------|---------|
| `on_conversation_end` | 對話即將結束 | s2 |
| `on_past_context_request` | 需要過去脈絡時 | s3 |
| `on_multi_step_task_start` | 多步任務起點 | s5 |
| `on_multi_step_task_checkpoint` | 多步任務重要中間點 | s5 |

### review

| 事件名稱 | 觸發說明 | 對應技能 |
|---------|---------|---------|
| `on_secondary_audit` | 第二審計者執行正式審計時 | b1 |
| `on_major_task_completion` | 重大任務收尾 | b2 |
| `on_error_case_filing` | 錯誤案例建檔時 | b3 |
| `on_user_comparison_request` | maintainer requests a comparison of options | b4 |
| `on_user_certainty_query` | 使用者詢問確定度時 | b5 |

### quality

| 事件名稱 | 觸發說明 | 對應技能 |
|---------|---------|---------|
| `on_z1_condition_match` | z1 五條件任一命中 | z1 |
| `on_delivery_scan` | 交付物完成時 | z2 |
| `on_checkpoint_update_with_compression_or_interruption` | checkpoint 更新＋曾壓縮或中斷 | z3 |
| `on_output_review` | 輸出品質需要診斷時 | z2/z3 |

### watchdog

| 事件名稱 | 觸發說明 | 對應技能 |
|---------|---------|---------|
| `on_weekly_health_check` | 每週一次，手動週檢 | 週檢全六格 |
| `on_manual_system_health_check` | 任意成員手動觸發健康檢查 | 週檢全六格 |

---

## 更新規則

1. 新增事件：先在本協議登記 → 再更新對應 manifest → 發通知給the maintainer
2. 廢棄事件：在本協議標注「廢棄」＋原因 → 更新對應 manifest → 不得直接刪除（保留歷史）
3. 本協議重大更動需the maintainer確認






