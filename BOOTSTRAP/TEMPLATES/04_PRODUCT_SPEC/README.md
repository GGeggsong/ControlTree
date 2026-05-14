# 07 Product Spec

PRODUCT_SPEC_VERSION: **{{PRODUCT_SPEC_VERSION}}**
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

> **非介面層**的產品／流程／商業規則。**不**取代 `01_INTERFACE_CONTRACT/`；那裡只放 byte／UUID／API endpoint 等通訊定義。

---

## 範疇

- 產品行為（例：定時器排程邏輯、亮度旋鈕 UI 行為）
- 設定／配對／註冊流程
- 商業規則（例：每帳號 N 台、保固期）
- 邊界與例外（例：斷電復原、離線行為）

## 檔案組織

- 每個主題一份 md，從 `TOPIC_TEMPLATE.md` 複製。
- 命名：`<TOPIC_UPPER>.md`，例：`TIMER_PRODUCT_SPEC.md`、`SETTINGS_AND_DEVICE_FLOW.md`、`BILLING_RULES.md`。

## 版本

- `PRODUCT_SPEC_VERSION` 用於整個 07_ 資料夾。
- 個別主題 md 表頭可額外標自己的小版本（選用）。

## 與 `01_INTERFACE_CONTRACT/` 的分工

- 同一行為若同時涉及「使用者體驗」與「封包定義」：
  - 使用者體驗描述放這裡。
  - byte／UUID／endpoint 仍只在 `01_` 定義。
- 兩處互相連結（連結 + 一句話導引），不複寫兩份內容。
