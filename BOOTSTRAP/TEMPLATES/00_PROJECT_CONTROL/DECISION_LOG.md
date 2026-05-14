# Decision Log

> 任何「之後翻舊帳會問為什麼這樣做」的決策都寫進來。一行一決策。

| Date | Decision | Owner | Notes |
|---|---|---|---|
| {{TODAY}} | 採用 Control Tree（中控樹）INIT v1.2.0 結構作為跨端協作中控樹 | {{AI_AGENT}} + User | INIT 包：<INIT 包來源 URL／本地路徑> |
| {{TODAY}} | 儲存後端使用 **{{STORAGE_BACKEND}}** | User | 詳見 `STORAGE_AND_SYNC.md` |
| {{TODAY}} | 初始端別清單為 **{{SIDE_LIST_CSV}}** | User | 之後可增；變更需登記新一行 |

---

## 記錄格式

```text
| YYYY-MM-DD | <一句話決策> | <Owner> | <Notes / 連結> |
```

範例：

```text
| 2026-06-01 | 改採用 git 作為主要儲存後端 | User | 將整棵樹 push 到 github.com/acme/easylighting-aisync |
| 2026-06-15 | CONTRACT_VERSION 升級至 v0.2.0：新增 0x30 指令 | Firmware | 見 CHANGE_REQUESTS.md CR-005 |
```
