# Error Code — {{INTERFACE_TYPE}}

CONTRACT_VERSION: **{{CONTRACT_VERSION}}**
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

> 跨端共識的錯誤碼／錯誤回應格式。各端應**對齊解譯與訊息**。

---

## 錯誤碼清單

| Code | Name | 場景 | 建議端側行為 | Since |
|---|---|---|---|---|
| — | — | （尚無，待補） | — | {{CONTRACT_VERSION}} |

> 範例：
>
> | `0x01` | InvalidParam | 任一參數越界 | 重試或提示使用者 | v0.1.0 |
> | `0x02` | AuthFailed | 密碼錯誤 | 提示重新輸入 | v0.1.0 |

## 通用準則

- 未列出之錯誤一律當 `0xFF Unknown`，記錄但不崩潰。
- 各端記錄錯誤的方式：`<SIDE>_TEST_LOG.md` 與 `BUG_CROSS_SIDE.md`（若跨端）。
