# 05 · AI Fill Rules（硬性規則）

> 這份檔案在 INIT 流程裡**最先讀**，後續所有步驟都要遵守。

---

## R1 · 動手範圍

- 你（AI）**只在中控樹根目錄內**新增資料夾／檔案。
- 你**不修改**使用者既有的程式碼、設定檔、版本控管設定（`.git/`、`.gitignore` 等）。
- 若使用者明確要求改原始碼，**先在中控樹中寫下變更說明**，再請使用者授權後才動原始碼。

## R2 · 占位符替換

- 模板中所有 `{{PLACEHOLDER}}` 都必須被替換成訪談得到的具體值。
- 若某欄位**訪談沒涵蓋到**（例如「行銷版號」），寫入 `Need Verify`，**不要編造**。

## R3 · 「Need Verify」與「Contract Pending」詞彙

固定使用以下狀態詞，跨檔案統一：

| 詞 | 用法 |
|---|---|
| `Need Verify` | 需要實機／實作驗證的條目 |
| `Contract Pending` | 跨端介面文字尚未涵蓋的差異 |
| `Waiting <SIDE>` | 等待某一端動作（例：`Waiting iOS`） |
| `Waiting Integration Test` | 等待整合測試 |
| `Blocked` | 有硬阻擋，無法繼續 |
| `Done` | 已實機／實作完成並驗證 |

未驗證的條目**不可標 `Done`**。

## R4 · 介面合約（Contract）的保護

- `01_INTERFACE_CONTRACT/` 為**單一真相來源**。
- 任何端的實作與合約不一致時：**不要單方面改合約**，把差異寫入：
  - `00_PROJECT_CONTROL/ISSUES_BLOCKERS.md`（記議題）
  - `01_INTERFACE_CONTRACT/CHANGE_REQUESTS.md`（記變更請求）
- 確定要改合約時，遞增 `CONTRACT_VERSION`（見 `VERSION_POLICY.md`），並在 `DECISION_LOG.md` 留下決策紀錄。

## R5 · 四軸版本

每次更新都要評估是否需要遞增以下任一軸：

| 軸 | 遞增時機 |
|---|---|
| `SYNC_REV`（`YYYY.MM.DD-NNN`） | 中控樹任一檔案有實質更新 |
| `CONTRACT_VERSION`（`vMajor.Feature.Patch`） | 跨端介面變更 |
| `SIDE_VERSION`（`<SIDE>-x.y.z`） | 某端實作版本變更 |
| `PRODUCT_SPEC_VERSION` | 非介面之產品／流程規格變更 |

`SYNC_REV` 同一天可遞增 `001 → 002 → ...`；每次更新中控檔都至少要把 `SYNC_REV` 加一。

## R6 · 同步紀錄

- 每次動完中控樹，**必寫** `00_PROJECT_CONTROL/SYNC_HISTORY.md` 一行（含 `SYNC_REV`、誰、改了哪些檔、為什麼）。
- 同時更新 `MASTER_STATUS.md` 的「Last Updated By / At」與「Latest Change」。

## R7 · 儲存後端衝突保護

- 動手前**先讀** `00_PROJECT_CONTROL/STORAGE_AND_SYNC.md` 知道當前後端是 `local` / `git` / `cloud-drive`。
- 若是 `cloud-drive` 或 `git`，動手前**先讀** `MASTER_STATUS.md` 的 `Last Updated At` 與 `Last Updated By`，若懷疑被他人剛改過，**先請使用者確認**再動。
- 你**不主動執行** `git commit` / `git push` / 雲端同步指令，除非使用者明確要求。

## R8 · 不可擅自精簡或刪檔

- 中控樹是「歷史可追溯」設計。**不刪舊內容**；要淘汰時搬到 `99_ARCHIVE/` 並在新檔保留指向舊檔的連結。

## R9 · 多 AI 共存

- 訪談結束後**一定要寫** `control-tree.config.yml`，這樣下一個 AI（不論品牌）讀進來就知道參數，不需要重新訪談。
- 每隻 md 表頭的 `Last Updated By` 標明「哪個 AI」（例 `Cursor (Claude Opus)` / `Gemini 2.5` / `ChatGPT-5`），有助於跨 AI 對帳。

## R10 · 訪談答覆缺漏的處理

若使用者跳過某題或回答不清楚：

- 給出**預設值**並標記 `Need Verify`，例：端別清單只給「韌體」時，預設 `firmware` 一個 SIDE 並提示使用者「日後若新增 App，請開新 SIDE」。
- 不要把訪談缺漏當作建樹失敗的理由。**樹永遠先建起來**，再逐步補。

## R11 · 共用文件單一位置原則（`_SHARED/`）

「全專案 AI 都該知道的東西」（SOP、腳位設定、流程圖、規範、外部 datasheet、Logo、品牌色卡等）一律放 **`_SHARED/`**。規則：

- **單一位置**：一份資產只能在 `_SHARED/` 出現一次。**不要**為了「方便看」而複製到 `00`–`04` 內。
- **相對連結**：其他 md 想用，**只用相對連結**指過去，例：`![pinout](../_SHARED/pinout_main_mcu.png)`。
- **索引維護**：每次新增／更新 `_SHARED/` 內的檔案，AI 都要更新 `_SHARED/README.md` §6 索引表（檔名、主題、誰會用、最近更新）。
- **動手前必掃**：每次協作前 AI 必讀 `_SHARED/README.md`，掃一眼索引；圖／PDF 等附件只在引用時才開。
- **建樹當下**：AI 只建立 `_SHARED/README.md` 空索引，**不主動**填內容；使用者後續自行往裡丟。

## R12 · 一人專案優化（不替團隊協作預先擔心）

本 INIT 包預設**單人多 AI 協作**為主場景：

- 不強制 PR review、不強制 commit message 規範、不強制鎖檔。
- 多 AI 對帳靠 `Last Updated By` + `_SHARED/README.md` 索引即可。
- 若使用者後續需要團隊協作，再依 `STORAGE_AND_SYNC.md` 切到 `git` 後端、加上 PR／CI 流程。
- AI **不要**在一人專案的中控樹塞「審核流程」「角色 RACI 表」「會議紀錄」這類團隊用件。

---

*05_FILL_RULES.md · part of Control Tree INIT v1.2.0*
