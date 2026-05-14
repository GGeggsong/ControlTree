# Control Tree（中控樹）· INIT

> **正式名稱（中文）**：中控樹 · **英文名稱**：Control Tree（全文其餘處以「Control Tree（中控樹）」併列呈現）。

> 這份檔案是「給 AI 看的入口劇本」。任何人類使用者只要把這份 md 的網址（或本地路徑）餵給任一 AI（Cursor / Claude / Gemini / ChatGPT / Codex …），AI 讀完後會主動進行訪談、建立中控樹、並填好初始檔案。

---

## 0. 給 AI 的執行指示（必讀）

你正在執行 **Control Tree（中控樹）建樹流程**。請依下列規則行動：

1. **不要直接動使用者既有的程式碼或專案檔案**；你只在「中控樹根目錄」內新增資料夾與 md。
2. **不要跳過訪談**。即使使用者已經給了部分參數，也要把 6 題（見 `BOOTSTRAP/01_INTERVIEW.md`）**逐題**走完，缺漏的補問。
3. **依序讀以下五份檔案**後再開始動手：
   1. `BOOTSTRAP/05_FILL_RULES.md` — 你必須遵守的硬性規則（含「Need Verify」「不可擅改 contract」等）
   2. `BOOTSTRAP/01_INTERVIEW.md` — 訪談腳本
   3. `BOOTSTRAP/02_BUILD_TREE.md` — 建樹規則與目錄命名
   4. `BOOTSTRAP/03_STORAGE_PRESETS.md` — 依使用者選擇的儲存後端套用 SOP
   5. `BOOTSTRAP/04_SYNC_PROTOCOL.md` — 告知使用者「日後協作前後該怎麼用這棵樹」
4. 訪談結果**同時**寫入：
   - 中控樹各 md 的表頭（從 `BOOTSTRAP/TEMPLATES/` 拷出來、替換 `{{PLACEHOLDER}}`）
   - 中控樹根目錄的 `control-tree.config.yml`（給下一次／其他 AI 快速讀，免重訪談）
5. 完成後產出**摘要回報**（見本檔最後一節 §4）。

---

## 1. 這套工具是什麼

**Control Tree（中文名：中控樹）**是一套以 **純 md 檔** 組成的協作中控樹，把「跨平台（Mac / Windows / Linux）、跨 AI（Cursor / Claude / Gemini / Codex …）、跨端（韌體／App／硬體／雲端／機構…）」的協作脈絡**檔案化**，讓任何 AI 都能在任何環境讀到「現在這個專案到哪了、誰欠誰、規格是什麼版本、共用文件去哪找」。

設計理念四句話：

- **Sync as Files**：脈絡是檔案，不是某一個 AI 的記憶。
- **核心固定、端別動態、儲存可換**：骨架不變，端別自由組合，本地／Git／雲端硬碟都能用。
- **共用文件單一位置**：SOP、腳位圖、流程圖、規範丟 `_SHARED/`，他處用相對連結指過去。
- **任何 AI、任何 OS**：只要這個 AI 能讀 md，就能加入協作。

---

## 2. 使用者只需要做的事

把這段話貼給任一 AI（自行替換 `<...>`）：

```
請依 https://raw.githubusercontent.com/<owner>/<repo>/main/INIT.md
（或本地路徑 <path>）執行 Control Tree（中控樹）建樹流程。
我的本地專案根目錄是 <C:\path\to\project>。
我想使用 <local | git | cloud-drive> 作為儲存後端。
```

AI 會接手完成所有步驟。使用者只需要在 AI **逐題**問 6 題訪談時依序回答即可。

---

## 3. AI 執行流程（必照順序）

```
STEP 1  讀 BOOTSTRAP/05_FILL_RULES.md       → 內化硬性規則
STEP 2  讀 BOOTSTRAP/01_INTERVIEW.md        → 對使用者做 6 題訪談
STEP 3  讀 BOOTSTRAP/02_BUILD_TREE.md       → 依答案決定資料夾與檔案
STEP 4  讀 BOOTSTRAP/03_STORAGE_PRESETS.md  → 取對應後端的 STORAGE_AND_SYNC 內容
STEP 5  從 BOOTSTRAP/TEMPLATES/ 拷貝模板    → 替換占位符後寫入中控樹
STEP 6  寫 control-tree.config.yml           → 把訪談答案存成單一真相
STEP 7  讀 BOOTSTRAP/04_SYNC_PROTOCOL.md    → 把日常協作守則告訴使用者
STEP 8  產出摘要回報（見 §4）
```

中控樹的根名稱預設為 `<ProjectName>_ControlTree/`，可由使用者改名。

---

## 4. 完成後 AI 必須回報的內容

請以條列式回報，至少包含：

- **中控樹根路徑**（絕對路徑）
- **已建立的一級資料夾清單**（數字編號核心 6 個：`00`–`04` 與 `99`，外加 `_SHARED/` 與自 `05_` 起之端別資料夾）
- **`SYNC_REV` 起始值**（格式 `YYYY.MM.DD-001`）
- **`CONTRACT_VERSION` 起始值**（若有多分支共用規格或通訊協定須版本化；無則可 `v0.0.0` 並於文中註明）
- **各 `SIDE_VERSION` 起始值**
- **儲存後端**：`local` / `git` / `cloud-drive`，以及對應 SOP 摘要
- **下一步建議**：例如「請先把 `01_INTERFACE_CONTRACT/INTERFACE_SPEC.md` 中的 `TODO` 段補完」

---

## 5. 版本與授權

- INIT 包版本：`v1.2.0`（品牌：Control Tree／中控樹；中控樹根目錄預設 `<ProjectName>_ControlTree/`；設定檔 `control-tree.config.yml`；固定一級目錄：`00_PROJECT_CONTROL`、`01_INTERFACE_CONTRACT`、`02_INTEGRATION_TEST`、`03_SKILLS_EXTRACTION`、`04_PRODUCT_SPEC`、`_SHARED`、`99_ARCHIVE`；端別自 `05_<SIDE>_SIDE` 至 `98_<SIDE>_SIDE`；完整規則見 `BOOTSTRAP/02_BUILD_TREE.md`）
- 規格授權：使用者可自由複製、改造這套中控樹結構，不需署名。
- 中控樹內**業務內容**之版權歸使用者所有，與本 INIT 包無關。

---

## 6. 相關檔案索引

| 檔案 | 用途 |
|---|---|
| `BOOTSTRAP/01_INTERVIEW.md` | 訪談腳本（6 題） |
| `BOOTSTRAP/02_BUILD_TREE.md` | 建樹規則、命名、編號（含 `_SHARED/`） |
| `BOOTSTRAP/03_STORAGE_PRESETS.md` | local / git / cloud-drive 三套 SOP |
| `BOOTSTRAP/04_SYNC_PROTOCOL.md` | 日常協作守則 |
| `BOOTSTRAP/05_FILL_RULES.md` | AI 硬性規則（先讀；含共用文件單一位置原則） |
| `BOOTSTRAP/TEMPLATES/` | 中控樹所有檔案的模板 |
| `BOOTSTRAP/TEMPLATES/_SHARED/README.md` | **共用文件中心**索引模板（SOP／腳位／流程圖／規範統一放這裡） |
| `control-tree.config.example.yml` | 訪談答案的範例設定檔 |
| `README.md` | 給人類讀的五分鐘上手 |
| `ARTICLE.md` | 設計理念長文 |

---

*Control Tree（中控樹）· INIT v1.2.0*
