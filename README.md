# Control Tree（中控樹）

> **正式名稱（中文）**：中控樹 · **英文名稱**：Control Tree  
> 路徑或識別字中常見的 `ControlTree`（連寫）與上述英文品牌指同一套方法與 INIT 套件，僅為檔名／程式慣例。

> 一棵以**純 md 檔**組成的通用協作中控樹。讓**任何 AI**（Cursor / Claude / Gemini / ChatGPT / Codex …）在**任何 OS**（Mac / Windows / Linux）下，對**任何專案**（韌體 / App / 硬體 / 雲端 / 機構…）共同維護同一份規格、進度、議題與版本。

無需安裝、無需 CLI、無需特定 AI。**把 `INIT.md` 餵給 AI，AI 自動完成建樹。**

---

## 五分鐘上手

### 1. 把這段話貼給任一支 AI

```
請依 https://raw.githubusercontent.com/<you>/<repo>/main/INIT.md
執行 Control Tree（中控樹）建樹流程。
我的本地專案根目錄是 <C:\path\to\project>。
我想使用 <local | git | cloud-drive> 作為儲存後端。
```

（沒網路時：把這個資料夾下載到本地，把 `INIT.md` 的本地路徑給 AI 也可以。）

### 2. AI 會問你 6 題（**一題一題**，答完才下一題）

1. 專案名稱（英數短代號，例 `EasyLighting`）
2. 中控樹要放在哪個本地路徑
3. **有幾條要分開追的線**（產品／平台／交付物皆可；可用中文說，AI 會幫你對成小寫代號後再確認）
4. **多條分支有沒有共用規格**（甲：BLE／Wi‑Fi／REST…；乙：平面圖、合約預算…；都沒有就說沒有）
5. 儲存後端（`local` / `git` / `cloud-drive`）
6. 版本：問一句「先預設 v0.0.0／各線 0.0.0 可以嗎？」可貼板號／版號

### 3. AI 自動建出中控樹

```
<your-project>_ControlTree/
├── README.md
├── control-tree.config.yml
├── 00_PROJECT_CONTROL/        ← 儀表板（總狀態、任務、議題、版本、決策、儲存約定）
├── 01_INTERFACE_CONTRACT/     ← 多分支共用規格（通訊／API／或共用準則）
├── 02_INTEGRATION_TEST/       ← Feature Matrix / 跨端 bug / 測試
├── 03_SKILLS_EXTRACTION/      ← 可重用的 AI skill 萃取
├── 04_PRODUCT_SPEC/           ← 非介面之產品／流程／商業規則
├── 05_<SIDE1>_SIDE/           ← 第 1 個端（5 隻檔案）
├── 06_<SIDE2>_SIDE/           ← 第 2 個端
├── …                          ← 依端別數量遞增至 98
├── _SHARED/                   ← 共用文件中心（SOP / 腳位 / 流程圖 / 規範）
└── 99_ARCHIVE/                ← 封存
```

> 端別資料夾編號規則見 [`BOOTSTRAP/02_BUILD_TREE.md`](./BOOTSTRAP/02_BUILD_TREE.md)。

> **`_SHARED/`** 是「你只要丟、其他人指過去」的地方。任何全專案 AI 都該知道的東西（韌體腳位圖、軟體 release SOP、外部 datasheet PDF、規範文件…）都丟這裡，其他 md 用相對連結引用。**單一位置，不複製。** 儲存上不另開一套：與整棵中控樹一樣預設在本機；換機就整包備份／複製，或改用 Git／雲端同步整棵樹（見 [`ARTICLE.md`](./ARTICLE.md) §2.3、§2.4）。

### 4. 之後換 AI 也沒問題

把這段話貼給新 AI：

```
請依 <中控樹路徑>/README.md 與 00_PROJECT_CONTROL/MASTER_STATUS.md 接續協作。
任務是 <一句話描述>。動手前讀 SYNC_RULES.md。
```

新 AI 會自動接上脈絡，繼續推進。

---

## 為什麼要用這個

跨平台、跨 AI、跨端協作時最常見的痛：

- **A 改了規格，B 不知道**
- **AI 換了一個品牌，整個前因後果歸零**
- **本地／Drive／Git 三個版本各自演化**
- **誰欠誰、進度到哪、問題卡在誰，永遠在群組訊息裡翻來翻去**

Control Tree（中控樹）把這些脈絡**檔案化**到一棵中控樹：

- 真相在 md，不在某一個 AI 的記憶
- 版本軸有四條（`SYNC_REV` / `CONTRACT_VERSION` / `SIDE_VERSION` / `PRODUCT_SPEC_VERSION`）
- 任何 AI 都能在 30 秒內讀完入口、知道現況、開始幹活
- 動完後也能寫回，下一個 AI 接得上

---

## 包裡有什麼

```
control-tree/                    ← meta 專案資料夾名可自訂；此為範例
├── INIT.md                       ← AI 入口劇本（給 AI 用）
├── README.md                     ← 本檔（給人看）
├── ARTICLE.md                    ← 設計理念長文
├── control-tree.config.example.yml ← 訪談結果範例設定檔
└── BOOTSTRAP/
    ├── 01_INTERVIEW.md           ← 訪談 6 題腳本
    ├── 02_BUILD_TREE.md          ← 建樹規則（含 _SHARED）
    ├── 03_STORAGE_PRESETS.md     ← local / git / cloud-drive 三套 SOP
    ├── 04_SYNC_PROTOCOL.md       ← 日常協作守則
    ├── 05_FILL_RULES.md          ← AI 硬性規則（含共用文件單一位置原則）
    └── TEMPLATES/                ← 所有中控樹檔案的模板
        ├── 00_PROJECT_CONTROL/
        ├── 01_INTERFACE_CONTRACT/
        ├── 02_INTEGRATION_TEST/
        ├── 03_SKILLS_EXTRACTION/
        ├── 04_PRODUCT_SPEC/
        ├── _SIDE/                ← 端別通用模板
        ├── _SHARED/              ← 共用文件中心索引模板
        ├── 99_ARCHIVE/
        └── README.tree.md        ← 中控樹根的 README 模板
```

---

## FAQ

**Q: 不同 AI 看到的東西會不會不一樣？**
A: 全部都是純 md 檔，任何能讀文字的 AI 都能解。差異只在「AI 怎麼遵守 `FILL_RULES`」；遵守得好的 AI（Cursor / Claude / Gemini / Codex 等近代模型）幾乎無差。

**Q: 多人同時改會不會打架？**
A: 視儲存後端。`local` 沒這問題；`git` 走 commit / merge；`cloud-drive` 依賴雲端用戶端的 conflict copy 機制，並透過 `MASTER_STATUS.md` 的 `Last Updated By/At` 互相打招呼（見 `03_STORAGE_PRESETS.md`）。

**Q: 我可以中途換儲存後端嗎？**
A: 可以。每個 Preset 都有「未來切換」段落。

**Q: AI 會擅自改我規格嗎？**
A: 不會，依 `05_FILL_RULES.md` R4：跨端介面是單一真相、任何修改要先進 `CHANGE_REQUESTS.md`，使用者授權後才動本文。

**Q: 端別很多個怎麼辦？**
A: 端別資料夾從 `05_<SIDE>_SIDE` 起遞增，可用到 `98_<SIDE>_SIDE`（見 `BOOTSTRAP/02_BUILD_TREE.md`）。`99_ARCHIVE/` 保留給封存。

**Q: 沒有 BLE／API 這種「介面」也能用嗎？**
A: 可以。第 4 題（甲）（乙）都答沒有即可；`01_INTERFACE_CONTRACT/` 仍會建立，內文標示目前無多分支共用規格。若只有平面、預算、貸款條件這類，在（乙）用白話說，由 AI 收成短標籤寫進 `INTERFACE_SPEC.md` 摘要。

**Q: 韌體腳位設定圖、軟體 SOP、規範 PDF、流程圖這些放哪？**
A: 全部丟 `_SHARED/`。**只丟這一個地方**，其他資料夾的 md 想用就用相對連結指過去（例 `![pinout](../_SHARED/pinout.png)`）。**不要複製檔案**。索引維護在 `_SHARED/README.md`。

**Q: 這套是給團隊用還是給個人用？**
A: 預設**一人多 AI 協作**。沒有強制 PR、code review、會議紀錄、角色 RACI 表那種團隊用件，AI 也不會主動塞給你。若日後想升級成團隊用，把儲存後端切到 `git`、加上自家的 PR / CI 流程即可。

---

## 設計理念

詳見 [`ARTICLE.md`](./ARTICLE.md)。

---

## 版本與授權

- INIT 包版本：`v1.2.0`（品牌：Control Tree／中控樹；使用者中控樹根預設 `<ProjectName>_ControlTree/`；設定檔 `control-tree.config.yml`；目錄編號：固定區為 `00`–`04` 與 `99`，並含 `_SHARED/`（底線開頭、不參與數字編號）；`05`–`98` 為端別；舊版 `05_INTEGRATION` 等路徑已廢止；若你從舊名 `*_AI_Sync`／`ai-sync.config.yml` 升級，請整包改名或保留舊檔並手動對照本版）
- 你可以自由使用、改造、轉散布這套結構，不需署名。
- 你**用這套結構**產出的中控樹版權歸你所有。
