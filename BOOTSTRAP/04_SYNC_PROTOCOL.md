# 04 · Daily Sync Protocol（日常協作守則）

> 給 AI：中控樹建好後，把本檔的「使用者守則」段落**告訴使用者**，並把「AI 守則」段落內化成你未來每次協作前後的固定流程。

---

## 給使用者的守則（請 AI 朗讀／摘要給使用者）

> 中控樹建好以後，**每次** 你或任何 AI 要動專案的代碼／規格前，請依以下流程：

1. **告訴 AI 中控樹位置**（或讓 AI 自動掃 IDE workspace 找到 `*_ControlTree/`）。
2. AI 會自動讀 `00_PROJECT_CONTROL/MASTER_STATUS.md`、`CURRENT_TASKS.md`，再依任務性質讀 `01_INTERFACE_CONTRACT/` 或對應 `0X_<SIDE>_SIDE/`。
3. 動完後 AI 會更新對應 md 與 `SYNC_HISTORY.md`、`MASTER_STATUS.md`，並把 `SYNC_REV` 加一。
4. 你只要在 AI 詢問「跨端議題／合約變更」時做決策；其他流程交給 AI。

換 AI 用？沒問題。把這幾句貼給新 AI：

```
請依 <中控樹路徑>/README.md 與 00_PROJECT_CONTROL/MASTER_STATUS.md 接續協作。
任務是 <一句話描述>。動手前讀 SYNC_RULES.md。
```

---

## 給 AI 的守則（每次協作前後必跑）

### 動手前（讀順序）

```
0. （若存在）<root>/control-tree.config.yml         → 讀 `user_preferences`（訪談節奏、少打斷、notes）；不得凌駕 SYNC_RULES／合約與驗證相關硬性規定
1. <root>/README.md                                 → 知道整棵樹用法
2. 00_PROJECT_CONTROL/MASTER_STATUS.md              → 現況、版本、上次更新者
3. 00_PROJECT_CONTROL/SYNC_RULES.md                 → 規則
4. 00_PROJECT_CONTROL/STORAGE_AND_SYNC.md           → 儲存後端 SOP
5. _SHARED/README.md                                → 共用文件中心索引（SOP / 腳位 / 流程圖 / 規範）
6. 00_PROJECT_CONTROL/CURRENT_TASKS.md              → 你欠什麼／誰欠你
7. 01_INTERFACE_CONTRACT/INTERFACE_SPEC.md          → 介面真相（若任務涉及）
8. 對應 0X_<SIDE>_SIDE/<SIDE>_STATUS.md             → 你這端現況
9. 02_INTEGRATION_TEST/FEATURE_MATRIX.md            → 跨端對帳
10.（視情況）`00_PROJECT_CONTROL/ISSUES_BLOCKERS.md`、`02_INTEGRATION_TEST/BUG_CROSS_SIDE.md`  → 已知議題
```

讀完前**不動程式碼**。

> **`_SHARED/README.md`** 是「全專案 AI 都該知道的東西」的索引（SOP、腳位設定、流程圖、規範、外部 datasheet）。它必讀，但內容很短，掃一眼就好。詳細的圖／PDF 只在被引用時才開。

### 動手中

- 任何「跨端介面」改動：**先**在 `01_INTERFACE_CONTRACT/CHANGE_REQUESTS.md` 開條目；**未獲使用者授權前**不改 `INTERFACE_SPEC.md` 本文。
- 跨端不一致：寫進 `ISSUES_BLOCKERS.md` 或 `02_INTEGRATION_TEST/BUG_CROSS_SIDE.md`，標 `Need Verify` / `Contract Pending`。
- 改了原始碼但未實機驗證：在 `0X_<SIDE>_SIDE/<SIDE>_STATUS.md` 與 `02_INTEGRATION_TEST/FEATURE_MATRIX.md` 對應列標 `Need Verify`，**不**標 `Done`。
- 需要引用 SOP／腳位圖／流程圖／規範：**只用相對連結指向 `_SHARED/`**，不要把那些檔複製到 `00`–`04` 內（也不要複製進端別資料夾取代 `_SHARED` 的單一位置原則）。

### 動手後（寫順序）

```
1. 對應 0X_<SIDE>_SIDE/<SIDE>_STATUS.md             → 更新版本／狀態
2. 0X_<SIDE>_SIDE/<SIDE>_CHANGELOG.md               → 加一行
3. 02_INTEGRATION_TEST/FEATURE_MATRIX.md            → 跨端對帳更新
4. 00_PROJECT_CONTROL/CURRENT_TASKS.md              → 勾完成、加新任務
5. 00_PROJECT_CONTROL/ISSUES_BLOCKERS.md            → 若有新議題
6. _SHARED/README.md（§6 索引表）                    → 若新增／更新了共用文件
7. 00_PROJECT_CONTROL/SYNC_HISTORY.md               → 寫一行（含新 SYNC_REV）
8. 00_PROJECT_CONTROL/MASTER_STATUS.md              → 更新 SYNC_REV、Last Updated By/At、Latest Change
```

### SYNC_REV 規則

- 每次中控樹有實質更新就 `+1`。
- 格式 `YYYY.MM.DD-NNN`，同一天 NNN 遞增 001, 002, 003...
- 跨日重置：新日期從 001 開始。
- 「無實質更新」（只調錯字）不必加，可選擇加 patch 但建議省略。

### 跨 AI 對帳

- `Last Updated By` 必標 AI 名稱／模型（例 `Cursor (Claude Opus 4.7)`、`Gemini 2.5 Pro`、`ChatGPT-5`）。
- 若你發現上一筆是另一個 AI 改的，**先讀懂它的改動**再動手；不要把對方的變更當錯誤直接覆蓋。

### 何時不要更新中控樹

- 純閒聊、與本專案無關的請求 → 不必開讀流程。
- 只是讀檔回答問題（沒修改） → 不必更新 SYNC_REV。

---

*04_SYNC_PROTOCOL.md · part of Control Tree INIT v1.2.0*
