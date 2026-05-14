# 03 · Storage Presets（儲存後端 SOP）

> 給 AI：依使用者在 Q5 的選擇，取對應的「Preset 段落」寫入中控樹 `00_PROJECT_CONTROL/STORAGE_AND_SYNC.md`。三套 SOP 互斥；可記載「未來想換」但目前只啟用一套。

---

## Preset A · `local`（預設）

> 適合單人單機開發、或還在 PoC 階段。

寫入 `STORAGE_AND_SYNC.md` 的內容（占位符已預先替換）：

```markdown
# Storage & Sync

Backend: **local**
Local Path: {{LOCAL_ROOT}}
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

## SOP（local）

- 中控樹放在本地，**不**自動同步。
- 多台電腦／多人協作時：請改為 `git` 或 `cloud-drive`。
- AI 動手前後：只更新本地檔案；不執行 commit／push／雲端 sync。
- 備份建議：每週將整棵中控樹打包進壓縮檔，存於另一處。

## 衝突風險

- 低（只有一個來源）。
- 若有第二台電腦同時改，請改用 `git` 或 `cloud-drive`。

## 未來切換

- 想換 `git`：把整棵中控樹 `git init`／加入既有 repo；同時更新本檔 Backend 欄位。
- 想換 `cloud-drive`：把整棵樹整體搬到雲端硬碟同步資料夾；同時更新本檔。
```

---

## Preset B · `git`

> 適合多人團隊、有版本控管文化、要 CI／自動化的情境。

寫入 `STORAGE_AND_SYNC.md` 的內容：

```markdown
# Storage & Sync

Backend: **git**
Repo URL: {{STORAGE_DETAIL}}
Local Path: {{LOCAL_ROOT}}
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

## SOP（git）

### 動手前

1. `git status` 確認 working tree 乾淨。
2. `git pull --rebase`（或 GUI 同步）取得最新中控樹。
3. 讀 `MASTER_STATUS.md` 知道目前 SYNC_REV。

### 動手後

1. 更新對應 md。
2. 更新 `SYNC_HISTORY.md` 與 `MASTER_STATUS.md` 之 SYNC_REV。
3. Commit 訊息格式：
   `chore(sync): SYNC_REV {{SYNC_REV}} — <一句話描述>`
4. AI **不主動** push；由使用者執行 `git push` 或 GUI 完成。
5. 衝突解決：以 `MASTER_STATUS.md` 為仲裁，差異進 `ISSUES_BLOCKERS.md` 記錄。

### 建議 .gitignore（中控樹根）

```
# AI Sync Tree
*.bak
*.tmp
.DS_Store
Thumbs.db
```

### CI（選用）

- 跑 markdown lint 與「占位符殘留」檢查。
- PR 模板要求填 SYNC_REV、影響的軸（CONTRACT / SIDE / PRODUCT_SPEC）。

## 衝突風險

- 中（並行 commit 可能撞同一 md，但 Git 天生處理 text merge）。
- 高頻檔（`MASTER_STATUS.md`、`SYNC_HISTORY.md`）建議由「當輪負責人」獨佔。

## 未來切換

- 想換 `cloud-drive`：先 `git pull` 拉到最新，再把樹複製到雲端資料夾並停用 git；或繼續 git 同時雙寫雲端（不建議，雙來源易漂移）。
```

---

## Preset C · `cloud-drive`

> 適合非工程角色一起改、需要原生檔案總管操作、跨 OS（Mac／Windows／Linux）混合。

寫入 `STORAGE_AND_SYNC.md` 的內容：

```markdown
# Storage & Sync

Backend: **cloud-drive**
Service: {{STORAGE_DETAIL}}（例：Google Drive / OneDrive / iCloud / Dropbox / NAS）
Local Path: {{LOCAL_ROOT}}
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

## SOP（cloud-drive）

### 動手前（必做）

1. **等待同步完成**：確認雲端用戶端 icon 顯示「已同步」。
2. 讀 `MASTER_STATUS.md` 的 `Last Updated By / At`：
   - 若顯示其他人／其他 AI **剛剛**改過（< 5 分鐘）→ 先暫停，請使用者確認對方是否還在改。
   - 若顯示自己上次的紀錄 → 安全動手。
3. 讀 `SYNC_HISTORY.md` 最後 1–3 筆，確認沒有對你任務影響的新異動。

### 動手後（必做）

1. 更新對應 md。
2. 更新 `SYNC_HISTORY.md`、`MASTER_STATUS.md`（含 SYNC_REV 與 Last Updated By/At）。
3. **等到雲端用戶端顯示「已上傳」** 才結束工作階段。

### 衝突檔（雲端常見 `xxx (conflicted copy).md`）

- 不要直接刪，搬到 `99_ARCHIVE/conflicts/` 並在 `ISSUES_BLOCKERS.md` 開議題請使用者裁決。

### 雙系統並存（例：本機 Git + 雲端硬碟）

- 兩套並存可行，但**只有一套是權威**：在本檔 Backend 欄位寫明哪個為權威。
- 非權威端只讀不改；或設「先同步、再改」流程，明列在本檔。

## 衝突風險

- 中高（雲端同步延遲 + 自動覆寫機制）。
- 高頻檔建議「動手前先打招呼」（聊天群／Slack）。

## 未來切換

- 想換 `git`：先把雲端那份 commit 入 git，再停用雲端同步（或把資料夾移出雲端資料夾）。
- 想換 `local`：把雲端資料夾複製一份到本地、停用同步。
```

---

## 通用：AI 自動同步輔助行為

無論哪種 Preset，AI 都應：

- 動手前後**讀／寫** `MASTER_STATUS.md` 的 `Last Updated By` 與 `Last Updated At`。
- 跨 AI 協作時，於 `Last Updated By` 標明自己（例 `Cursor (Claude Opus 4.7)` / `Gemini 2.5 Pro` / `ChatGPT-5`）。
- **不**自動執行 git commit/push 或啟動雲端用戶端，除非使用者要求。

---

*03_STORAGE_PRESETS.md · part of Control Tree INIT v1.2.0*
