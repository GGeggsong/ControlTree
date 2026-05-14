# Integration Test Plan

Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}
Based On Contract Version: **{{CONTRACT_VERSION}}**

> 跨端整合測試計畫。**和 `FEATURE_MATRIX.md` 對應**：每個矩陣列至少有一個對應測項。

---

## 1. 範疇與目標

- 範疇：{{SIDE_LIST_CSV}} 之跨端互動。
- 目標：驗證所有 `FEATURE_MATRIX` 列的 `Integration Status` 從 `Waiting Integration Test` 推進到 `Done`。

## 2. 測試環境

- 硬體：TODO
- 軟體版本：依當時各 `<SIDE>_VERSION`
- 工具：TODO（sniffer、模擬器、自動化框架等）

## 3. 測試矩陣

| Test ID | Feature | 條件 | 步驟 | 預期結果 | 對應 FEATURE_MATRIX 列 |
|---|---|---|---|---|---|
| T-001 | — | — | — | — | — |

## 4. 通過判定

- 全部 T-### 通過 → 該 contract 版本可標 stable。
- 任一通過率 < 100% → 把失敗項開 `BUG_CROSS_SIDE.md`。

## 5. 排程與責任

- 排程：TODO
- 主測：TODO
- 觀察員：各端 AI／開發者

## 6. 風險與假設

- TODO
