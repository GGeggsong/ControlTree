# Sync Rules

> 本中控樹的基本協作規則。任何 AI / 開發者在動手前都應遵循。

## 1. 入口

- 中控樹根目錄 `README.md` 是人類入口；`00_PROJECT_CONTROL/MASTER_STATUS.md` 是 AI／團隊現況入口。

## 2. 真相層級

- **`01_INTERFACE_CONTRACT/`** 為跨端介面的單一真相。
- **`04_PRODUCT_SPEC/`** 為非介面（產品、流程、商業規則）的單一真相。
- **`_SHARED/`** 為「全專案共用資產」（SOP、腳位圖、流程圖、規範、外部 datasheet、品牌素材）的單一位置。其他 md 想用**只用相對連結**指過去，**不複製檔案**。索引維護於 `_SHARED/README.md` §6。
- 各端的 `STATUS.md` 是該端**實作現況**的真相；當實作與合約不一致 → 走 `ISSUES_BLOCKERS.md` 與 `01_INTERFACE_CONTRACT/CHANGE_REQUESTS.md`，**不**單方面改合約。

## 3. 讀寫順序

- 動手前讀順序：`README.md` → `MASTER_STATUS.md` → `SYNC_RULES.md` → `STORAGE_AND_SYNC.md` → **`_SHARED/README.md`** → `CURRENT_TASKS.md` →（任務相關）`01_INTERFACE_CONTRACT/INTERFACE_SPEC.md` / `0X_<SIDE>_SIDE/<SIDE>_STATUS.md` / `02_INTEGRATION_TEST/FEATURE_MATRIX.md`。
- 動手後寫順序：`0X_<SIDE>_SIDE/<SIDE>_STATUS.md` → `0X_<SIDE>_SIDE/<SIDE>_CHANGELOG.md` → `02_INTEGRATION_TEST/FEATURE_MATRIX.md` → `CURRENT_TASKS.md` →（如有議題）`ISSUES_BLOCKERS.md` →（若新增共用文件）`_SHARED/README.md` 索引 → `SYNC_HISTORY.md` → `MASTER_STATUS.md`。

## 4. 狀態詞彙（跨檔案統一）

`Need Verify` | `Contract Pending` | `Waiting <SIDE>` | `Waiting Integration Test` | `Blocked` | `Done`

未驗證／未實機者**不可標 `Done`**。

## 5. SYNC_REV 規則

- 每次更新中控樹都遞增 `SYNC_REV`（見 `VERSION_POLICY.md`）。
- 同一天可遞增多次（NNN）。

## 6. 跨 AI 對帳

- 每個 md 表頭的 `Last Updated By` 必標明 AI 名稱／模型（如 `Cursor (Claude Opus 4.7)`、`Gemini 2.5`、`ChatGPT-5`）。
- 接手前先讀上一筆 AI 的更新意圖，不要直接覆蓋。

## 7. 儲存後端 SOP

- 動手前後依 `STORAGE_AND_SYNC.md` 對應後端 SOP 行動。
- AI 不主動 commit／push／啟動雲端同步指令，除非使用者要求。
