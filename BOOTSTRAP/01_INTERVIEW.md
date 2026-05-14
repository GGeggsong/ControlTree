# 01 · Interview Script（訪談腳本）

> 給 AI：你必須**用使用者的語言**（預設繁體中文）**逐題**提問；**每題要等使用者回答後再問下一題**，不要一次問完。**禁止**在單一則訊息裡把 Q1～Q6（或尚未作答的多題）整包貼給使用者——使用者請你「模擬訪談」時也一樣，須與實際建樹**相同節奏**（逐題），否則沒有模擬價值。**例外**：僅當使用者**明文**說「請把六題整份列出來我自己填／列印」時，才可一次貼出全文，且須註明：**正式建樹訪談仍應逐題進行**。回答結束後，把所有答案彙整成 `control-tree.config.yml`（範例見根目錄）。

---

## 訪談規則

- **逐題**問，不要 batching。**每一則**發給使用者的訊息**最多一題**（Q4 的（甲）（乙）視為**同一題**的連續提問，可寫在同一則裡；不要拆成要來回六則才答完一題）。**禁止**把多題或未作答的題目整包貼上。
- 每題要等使用者回答後再問下一題。
- 每題提供**範例答案**，降低使用者卡關機率。
- 若使用者回答模糊，**追問一次**；仍模糊則套用預設值並標 `Need Verify`。
- 訪談結束後**復述彙整**讓使用者確認，再開始建樹。
- **給非工程背景使用者**：不要用「端」「SIDE」「kebab-case」當開場白；先用生活化中文問清楚，再在彙整裡**一行對照**「你說的 ○○ → 建樹用代號 `xxx`」。代號規則仍遵守各題下方的硬性規則（AI 負責翻譯與確認）。
- **Q6 起始版本**：對使用者**只問一句**是否同意起頭版（見 Q6）；術語寫進 yml／md 即可；**不得**要求為建樹查多台電腦。

---

## 6 題訪談

### Q1 · 專案名稱

> 「請給我這個專案的英文短代號（會用在資料夾名稱），例如 `EasyLighting`、`MyHomeBox`、`AcmeRobot`。」

- 規則：英數與底線；建議 4–20 字。
- 用途：中控樹根目錄將命名為 `<ProjectName>_ControlTree/`。
- 預設：若使用者只給中文名稱，AI 自動轉一個英數短代號並請使用者確認。

### Q2 · 中控樹本地路徑

> 「請給中控樹要放在本地的哪個資料夾？我會在這底下建一個 `<ProjectName>_ControlTree/`。例如 `D:\Projects\EasyLighting` 或 `/Users/me/Projects/EasyLighting`。」

- 用途：決定建樹根目錄。
- 預設：若使用者答「就放在這個專案根目錄」，採用使用者當前 IDE workspace 的根。

### Q3 · 協作分支清單（建樹時稱 Side List；**對使用者不必講這個詞**）

**請對使用者這樣問（擇一或合併，口吻自然即可）：**

> 「這個案子裡，你有**幾條要分開追的線**？每一條可以是不同產品、不同平台、不同交付物，或不同機器上的工作——請用**你習慣的說法**列出來就好。例如：沙發、餐桌、椅子；或網站、後台、小冊子。若整案只有一條線，說一個也可以。」

**若使用者明顯是工程背景**，可改用較短版本：

> 「有哪些模組或平台要分開維護狀態？請列舉，例：`firmware, ios, android` 或 `web, cloud, hardware`。」

**AI 接到答案後（硬性）：**

- 把每一條線對應成**一個**小寫英文短代號（單字或 `kebab-case`，逗號分隔、**不要空白**），例如使用者說「沙發、餐桌、椅子」→ `sofa, table, chair`。
- **念給使用者聽一次**：「我會用 `sofa, table, chair` 當資料夾代號，可以嗎？」不同意則改代號再確認。
- 若使用者一開始就用英文代號回答，仍要確認「順序」是否代表優先級（預設：順序只影響 `05→06→07` 編號，不改語意）。

**規則（與 `02_BUILD_TREE.md` 一致）：**

- 用途：清單有幾項，就建幾個 `0X_<SIDE>_SIDE/`（X 從 **05** 起遞增）。
- 範例代號：`firmware`、`ios`、`sofa`、`copy`、`mechanical` 等。
- 預設：若只有一條線，仍建一個 SIDE 資料夾；之後可加。

### Q4 · 多條分支之間「有沒有要共用的一份規格」（建樹時寫入 `interface.types`；**對使用者不必講資料夾名**）

> 說明給 AI：`01_INTERFACE_CONTRACT/` 放的是「**不只一條分支會用到、不能各寫各的**」那份規格。可能是藍牙／API，也可能是平面圖、合約條件；**沒有就記 `none`**。各分支自己的筆記仍在各自的 `_SIDE/`。

**請對使用者這樣問（建議照順序；口吻白話）：**

> 「前面你列的那幾條，有沒有**兩條以上會一起依賴同一份東西**？我分兩種問，你想到哪種就答哪種；**兩種都沒有就說都沒有**。」
>
> 「**（甲）電子或軟體**：模組之間要不要靠**同一套連線或傳輸規格**溝通？有的話**直接講技術名**就好，例如：**藍牙 BLE**、**Wi‑Fi**、**HTTP／REST**、**WebSocket**、**gRPC**、**MQTT**、**RS‑485**、**CAN**、**I2C**、或你自己取的協定名稱。**完全沒有、各跑各的**，就說**沒有**。」
>
> 「**（乙）不是寫程式這類**：有沒有**同一份檔案或同一組規則**大家都要照？例如同一張平面圖、同一份業主簽過的需求、貸款核准前不能超出的預算。**有就形容一下**；**沒有就說沒有**。」

**若對話已經很清楚是純軟硬體通訊專案**，可只問（甲），（乙）一句帶過：「若還有非程式的共同文件要當準則，也可以補充；沒有就跳過。」

**AI 接到答案後（硬性）：**

- （甲）有具體通訊／API → `interface.types` 用慣例標籤：`BLE`、`Wi-Fi`、`REST`、`WebSocket`、`gRPC`、`MQTT`、`RS-485`、`CAN`、`I2C`、`custom-<slug>` 等（與使用者用語對齊即可）。
- （乙）有白話描述、無通訊 → 濃縮成 kebab-case 短標籤寫入 `interface.types`（例：`floor-plan`、`financing-cap`）；**不要**硬塞 BLE。
- 兩邊都沒有 → `interface.types` 填 `none`，`INTERFACE_SPEC.md` 首段寫明「目前無須多分支共用的固定規格」。
- 答得模糊 → **追問一次**；可舉反例：「例如只有 iOS 跟雲端用 REST 對接、韌體不管，那 REST 就算有」。
- 複選允許；復述時用使用者聽得懂的話：「我會把你說的 BLE、還有那張平面圖，記成『多分支共用規格』，可以嗎？」（不要說「單一真相區」除非使用者自己用這詞。）

**用途（不變）：** 決定 `01_INTERFACE_CONTRACT/` 初稿寫什麼；無則依 `02_BUILD_TREE.md` 標 N/A，不硬填假協定。

**預設：** 仍模糊 → `none` 並標 `Need Verify`。

#### Q4 答題範例（給 AI 對齊語意；工程與非工程各保留一則）

**範例 A · 工程（甲有、乙無）**

- 使用者答：「韌體跟 App 靠 **BLE** 對接；沒有大家共用一份平面圖或合約檔那種。」
- `interface.types`：`BLE`（可複選，如再加 `REST` 則一併列出）。
- `INTERFACE_SPEC.md`：依協定填寫；（乙）相關節標 **N/A** 或一句帶過「無」。

**範例 B · 非工程（甲無、乙有：多份共用規格／企劃書）**

- 使用者答：「**（甲）沒有**，沒有 BLE／Wi‑Fi／API 那些。**（乙）有**——我們有 **專案共用規格書**、**範疇管理企劃書**、**品質管理計畫書**、**採購管理企劃書**、**風險管理企劃書**，各分支都要照這幾份。」
- `interface.types`（建議標籤，經使用者 OK 後寫入 yml）：
  - `shared-project-spec` ← 專案共用規格書
  - `scope-management-plan` ← 範疇管理企劃書
  - `quality-management-plan` ← 品質管理計畫書
  - `procurement-management-plan` ← 採購管理企劃書
  - `risk-management-plan` ← 風險管理企劃書
- **實體檔**放 `_SHARED/`（或子資料夾），`_SHARED/README.md` 建索引；`INTERFACE_SPEC.md` **§1** 用白話摘要這五份的角色與「變更時誰拍板」，**不要**把 PDF 全文貼進 md。

### Q5 · 儲存後端（Storage Backend）

> 「中控樹要怎麼跟其他人／其他電腦同步？三選一：
>
> - `local`：純本地，自己管，不同步（最簡單）
> - `git`：放進 Git，靠 commit／push／pull 同步
> - `cloud-drive`：放在 Google Drive / OneDrive / iCloud / Dropbox / NAS 等雲端硬碟自動同步」

- 用途：決定 `STORAGE_AND_SYNC.md` 套用哪一份 SOP（見 `03_STORAGE_PRESETS.md`）。
- 預設：`local`。
- 若選 `git`：追問 repo URL（可填 `TBD`）。
- 若選 `cloud-drive`：追問雲端服務名稱與本地對應路徑。

### Q6 · 起始版本（Initial Versions；**預設帶入，不追問查機**）

> 說明給 AI：**禁止**叫使用者為建樹去各台電腦查板號、翻 repo。畫面上只問**一句**是否同意預設；同意就寫入模板與 `control-tree.config.yml` 並標 `Need Verify`；使用者有貼版號／板號再覆寫。

**請對使用者這樣問（一句話；不要用 CONTRACT_VERSION、Need Verify 等術語轟使用者）：**

> 「各條線跟共用規格（前面第 4 題若有）的版本，我**先全部幫您用起頭版**（合約 **v0.0.0**、各條線 **0.0.0**），**可以嗎？** 您手邊若有**現成的板號或版號**，也可以現在貼上來。」

**AI 接到答案後（硬性）：**

- 使用者答「好／可以／OK／用預設」→ 依預設寫入，**不要**再問第二遍要不要查機。
- 使用者貼了版號／板號 → **AI 代轉**成 `CONTRACT_VERSION`（`v*.*.*`）與各線 `SIDE_VERSION`（`<SIDE_UPPER>-*.*.*`），復述一行請確認；格式怪也**由 AI 修**，別叫使用者背規則。
- 使用者完全沒提、只說好 → `CONTRACT_VERSION`：**`v0.0.0`**；各線：**`<SIDE_UPPER>-0.0.0`**；`PRODUCT_SPEC_VERSION` 與 `VERSION_POLICY.md` 一致採 **`v0.0.0`** 起跳並標 `Need Verify`（擇一貫即可）。
- **不要追問**「要不要去查」。
- 規則（寫進檔案時仍遵守）：`CONTRACT_VERSION` 為 `vMajor.Feature.Patch`；`SIDE_VERSION` 為 `<SIDE_UPPER>-x.y.z`。

---

## 訪談結束後 AI 要做的事

1. **復述彙整**：把 6 題答案以一份條列清單復述，讓使用者確認。
2. **確認後**才開始執行 `02_BUILD_TREE.md`。
3. **同步寫入** `control-tree.config.yml`（建在中控樹根目錄）。

範例復述（給 AI 參考輸出格式；**兩種專案各保留一則**）。

**範例 1 · 工程專案（通訊協定）**

```
我會用以下參數建立中控樹，請確認：
- 專案名稱：EasyLighting
- 中控樹路徑：D:\Projects\EasyLighting\EasyLighting_ControlTree
- 協作分支（代號）：firmware, ios, android（將建 `05_FIRMWARE_SIDE`、`06_IOS_SIDE`、`07_ANDROID_SIDE`）
- 第 4 題：（甲）BLE；（乙）無 → interface.types: BLE
- 儲存後端：cloud-drive（Google Drive，本地路徑 D:\Drive\EasyLighting\）
- 起始版本：依預設 CONTRACT **v0.0.0**、FW-0.0.0、IOS-0.0.0、ANDROID-0.0.0（Need Verify；若使用者訪談時已給明確版號則改填）
請回覆「OK」或要修改的項目。
```

**範例 2 · 非工程專案（共用規格書／企劃書；無 BLE／API）**

```
我會用以下參數建立中控樹，請確認：
- 專案名稱：FurnitureProgram（範例代號，實際以 Q1 為準）
- 中控樹路徑：<Q2 使用者指定>/FurnitureProgram_ControlTree
- 協作分支（代號）：sofa, mep-plan, financing（將建 `05_SOFA_SIDE`、`06_MEP_PLAN_SIDE`、`07_FINANCING_SIDE`）
- 第 4 題：（甲）無；（乙）五份共用文件 → interface.types:
  shared-project-spec, scope-management-plan, quality-management-plan,
  procurement-management-plan, risk-management-plan
  （對應：專案共用規格書、範疇管理企劃書、品質管理計畫書、採購管理企劃書、風險管理企劃書；正本請放 _SHARED/ 並建索引）
- 儲存後端：<Q5 使用者選擇>
- 起始版本：依預設（CONTRACT v0.0.0、SOFA-0.0.0、MEP_PLAN-0.0.0、FINANCING-0.0.0，Need Verify；使用者有提供則覆寫）
請回覆「OK」或要修改的項目。
```

---

*01_INTERVIEW.md · part of Control Tree INIT v1.2.0*
