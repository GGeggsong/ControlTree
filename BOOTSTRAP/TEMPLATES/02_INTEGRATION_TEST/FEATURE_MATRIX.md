# Feature Matrix

Last Updated At: **{{TODAY}}**
Last Updated By: {{AI_AGENT}}
Reconcile Ref: **SYNC_REV {{SYNC_REV}}**

**CONTRACT_VERSION**：**{{CONTRACT_VERSION}}** — 與各 `<SIDE>_STATUS.md` 之 **Based On** 應一致。

**Integration Status 字彙**：`Pending` | `Waiting <SIDE>` | `Waiting Integration Test` | `Done` | `Blocked` | `Contract Pending` | `Need Verify`

---

## 功能矩陣

| Feature | Contract Version | {{COL_SIDES}} | Integration Status | Next Owner | Notes |
|---|---|---|---|---|---|
| — | {{CONTRACT_VERSION}} | — | Pending | User | （尚無功能，待補） |

> `{{COL_SIDES}}` 由 AI 依端別清單展開為多欄，例：`Firmware Status | iOS Status | Android Status`。

---

## 說明

- **未實機者不可標 `Done`**；最高僅 `Waiting Integration Test`。
- 「兩端實作差異」屬 `Contract Pending`，進 `01_INTERFACE_CONTRACT/CHANGE_REQUESTS.md`。
- 「邏輯一致但細節未驗」屬 `Need Verify`。

## 對帳節律

- 每次 contract 改版（feature／major）→ 重新對齊本表。
- 每月一次 ad-hoc Reconcile，產出 `INTEGRATION_TEST_LOG.md` 條目。
