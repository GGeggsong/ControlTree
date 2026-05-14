# Sync History

> 中控樹自身的版本史。每次有實質更新都在頂部加一行。

## {{SYNC_REV}}（{{TODAY}}）

- By: {{AI_AGENT}}
- Control Tree（中控樹）初始化。
- 建立資料夾：核心 6 個 + SIDE × {{SIDE_COUNT}}（{{SIDE_LIST_CSV}}）。
- 儲存後端：**{{STORAGE_BACKEND}}**。
- 初始版本：`CONTRACT_VERSION` = `{{CONTRACT_VERSION}}`、`PRODUCT_SPEC_VERSION` = `{{PRODUCT_SPEC_VERSION}}`。
- 未改任何專案原始碼。

---

## 紀錄格式

```text
## {SYNC_REV}（{YYYY-MM-DD}）
- By: <AI name / human>
- 一句話摘要
- 影響檔案：<檔案清單>
- 是否動程式碼：是 / 否
- 版本軸變動：<例如 CONTRACT_VERSION v0.1.0 → v0.2.0>
```
