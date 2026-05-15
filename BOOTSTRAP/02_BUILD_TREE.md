# 02 · Build Tree Rules（建樹規則）

> 給 AI：依訪談結果建立中控樹。本檔定義**命名、編號、檔案清單**與**從 TEMPLATES 拷貝的流程**。

---

## 1. 中控樹根目錄

- 名稱：`<ProjectName>_ControlTree/`
- 位置：使用者在 Q2 指定的路徑底下
- 範例：`D:\Projects\EasyLighting\EasyLighting_ControlTree\`

## 2. 一級資料夾清單

### 編號原則（給 AI，不給人「故事線」）

- **固定區**用連號 `00`–`01`、`02`–`04`、`99`，路徑穩定、語意不飄。
- **動態端別**從 `05` 起遞增，**不**與固定區撞號；最多可用 `05`–`98`（共 94 個端別槽位，實務足夠）。
- **AI 讀檔順序**一律依 `SYNC_RULES.md` / `04_SYNC_PROTOCOL.md`，**不依賴**檔案總管依編號排序。

### 核心固定（每個專案都要有）

| 編號 | 資料夾 | 是否動態 |
|---|---|---|
| 00 | `00_PROJECT_CONTROL/` | 固定 |
| 01 | `01_INTERFACE_CONTRACT/` | 固定 |
| 02 | `02_INTEGRATION_TEST/` | 固定 |
| 03 | `03_SKILLS_EXTRACTION/` | 固定 |
| 04 | `04_PRODUCT_SPEC/` | 固定 |
| — | `_SHARED/` | 固定（共用文件中心；底線開頭，不參與編號） |
| 99 | `99_ARCHIVE/` | 固定 |

### 端別動態（依 Q3 清單展開）

| 編號 | 資料夾 | 規則 |
|---|---|---|
| 05 | `05_<SIDE1>_SIDE/` | 第一個端 |
| 06 | `06_<SIDE2>_SIDE/` | 第二個端 |
| 07 | `07_<SIDE3>_SIDE/` | 第三個端 |
| … | … | 依 Q3 順序遞增 |
| 98 | `98_<SIDE94>_SIDE/` | 第 94 個端（上限） |

**命名規則**：`<SIDE>` 一律大寫底線，例 `05_FIRMWARE_SIDE/`、`06_IOS_SIDE/`。

**端別數量**：第 N 個端使用編號 `04 + N`（即從 `05` 起）。不得使用 `99`（保留給封存區）。

## 3. 每個資料夾要建的檔案

### `00_PROJECT_CONTROL/`（8 檔）

從 `TEMPLATES/00_PROJECT_CONTROL/` 拷出：

- `MASTER_STATUS.md`
- `CURRENT_TASKS.md`
- `ISSUES_BLOCKERS.md`
- `SYNC_HISTORY.md`
- `VERSION_POLICY.md`
- `DECISION_LOG.md`
- `STORAGE_AND_SYNC.md`
- `SYNC_RULES.md`

### `01_INTERFACE_CONTRACT/`（5 檔，依介面類型調整檔名）

從 `TEMPLATES/01_INTERFACE_CONTRACT/` 拷出並依 Q4 選擇調整：

- `INTERFACE_SPEC.md`（一般通用名稱，建議保留）
- `COMMAND_TABLE.md`（如為 BLE / RS-485 等指令式介面）
- `DATA_FORMAT.md`
- `ERROR_CODE.md`
- `CHANGE_REQUESTS.md`

**檔名變體（選用）**：若使用者堅持要在檔名前加介面前綴（例 `BLE_INTERFACE_SPEC.md`），可加，但保留 `INTERFACE_SPEC.md` 為主檔名以維持跨專案一致。**預設不加前綴**。

**Q4 非通訊類或 `none` 時**：仍拷貝本區五檔。`INTERFACE_SPEC.md` 由 AI 依訪談白話改寫 **§1 範疇**（寫清「多分支共用什麼規格／檔案」或明確寫「目前無」）；§2 起若無傳輸層／指令表可寫，標 **N/A** 或改寫成該專案實際條款（空間基準、財務門檻、業主需求摘要等），**不要**留一堆 BLE 範例 TODO 假裝有協定。

### `02_INTEGRATION_TEST/`（4 檔）

從 `TEMPLATES/02_INTEGRATION_TEST/` 拷出：

- `FEATURE_MATRIX.md`
- `INTEGRATION_TEST_PLAN.md`
- `INTEGRATION_TEST_LOG.md`
- `BUG_CROSS_SIDE.md`

### `03_SKILLS_EXTRACTION/`（1 檔起）

從 `TEMPLATES/03_SKILLS_EXTRACTION/` 拷出：

- `README.md`（規範這個資料夾用法）

### `04_PRODUCT_SPEC/`（2 檔起）

從 `TEMPLATES/04_PRODUCT_SPEC/` 拷出：

- `README.md`
- `TOPIC_TEMPLATE.md`（未來各主題複製此模板再改名）

### `05_<SIDE>_SIDE/` 起（每個端 5 檔）

從 `TEMPLATES/_SIDE/` 拷出，**檔名前綴替換**為該端的大寫名稱：

- `<SIDE_UPPER>_STATUS.md`
- `<SIDE_UPPER>_AI_HANDOFF.md`
- `<SIDE_UPPER>_CHANGELOG.md`
- `<SIDE_UPPER>_TEST_LOG.md`
- `<SIDE_UPPER>_SKILL_NOTES.md`

範例：`05_FIRMWARE_SIDE/FIRMWARE_STATUS.md`、`06_IOS_SIDE/IOS_AI_HANDOFF.md`。

### `_SHARED/`（1 檔起；使用者後續自由新增）

從 `TEMPLATES/_SHARED/` 拷出：

- `README.md`（索引兼放置規則；**這份必建**）

> 其他內容由使用者自行新增（SOP、腳位圖、流程圖、PDF、規範等）。AI 建樹時**不主動**填內容；只建空索引。

### `99_ARCHIVE/`（1 檔）

從 `TEMPLATES/99_ARCHIVE/` 拷出：

- `README.md`

### 中控樹根目錄（2 檔）

- `README.md`（從 `TEMPLATES/README.tree.md` 拷出，**注意是 `README.tree.md`**，避免和 INIT 包根的 README 衝突）
- `control-tree.config.yml`（從 `control-tree.config.example.yml` 拷出並依訪談填值）

## 4. 占位符表（必須全部替換）

| 占位符 | 來源 |
|---|---|
| `{{PROJECT_NAME}}` | Q1 |
| `{{PROJECT_NAME_LOWER}}` | Q1 全小寫 |
| `{{LOCAL_ROOT}}` | Q2（中控樹絕對路徑） |
| `{{SIDE_LIST_CSV}}` | Q3（逗號分隔） |
| `{{INTERFACE_TYPE}}` | Q4（例 `BLE`、`REST`、或 `None`） |
| `{{STORAGE_BACKEND}}` | Q5（`local` / `git` / `cloud-drive`） |
| `{{STORAGE_DETAIL}}` | Q5 追問結果（repo URL 或雲端服務 + 本地路徑） |
| `{{CONTRACT_VERSION}}` | Q6；使用者未提供時 **v0.0.0** 並標 `Need Verify` |
| `{{SIDE_VERSION:<side>}}` | Q6 對應；未提供時 **`<SIDE_UPPER>-0.0.0`** 並標 `Need Verify` |
| `{{PRODUCT_SPEC_VERSION}}` | 預設 `v0.1.0` |
| `{{SYNC_REV}}` | 建樹當下日期 + `-001`，例 `2026.05.14-001` |
| `{{TODAY}}` | 建樹當天（使用者時區，例 `2026-05-14`） |
| `{{AI_AGENT}}` | 你自己的標識，例 `Cursor (Claude Opus 4.7)` |
| `{{SIDE_LOWER}}` / `{{SIDE_UPPER}}` | 端別模板專用 |

## 5. 建樹後的初始填值

- `MASTER_STATUS.md` 中各端 `SIDE_VERSION` 與 `CONTRACT_VERSION` 依 Q6 填；**訪談時使用者未給版號**則 AI 填 **v0.0.0**／**`<SIDE_UPPER>-0.0.0`** 並標 `Need Verify`，其餘留空或標 `Need Verify`。
- `SYNC_HISTORY.md` 寫第一筆紀錄：`{{SYNC_REV}}：Control Tree（中控樹）初始化（by {{AI_AGENT}}）`。
- `DECISION_LOG.md` 寫第一筆決策：採用 Control Tree（中控樹）INIT v1.2.0 結構、儲存後端為 `{{STORAGE_BACKEND}}`。
- `CURRENT_TASKS.md` 預埋一條：**填寫 `01_INTERFACE_CONTRACT/INTERFACE_SPEC.md` 與各端 `STATUS.md`**。
- `control-tree.config.yml` 依訪談寫滿（見 `control-tree.config.example.yml`），**必含** `user_preferences`（見 `01_INTERVIEW.md`）。

## 6. 完成判定

中控樹建好的判定：

- [ ] 所有一級資料夾都已建立（含 `_SHARED/`）
- [ ] 所有模板檔已拷貝且**沒有殘留 `{{...}}` 占位符**（除了範例與註解中刻意保留的）
- [ ] `control-tree.config.yml` 已寫入
- [ ] `MASTER_STATUS.md` 顯示正確的 `SYNC_REV`
- [ ] `_SHARED/README.md` 存在（供使用者開始往裡丟東西）
- [ ] 已對使用者復述摘要（見 INIT.md §4），含「共用文件請丟 `_SHARED/`」的提示

---

*02_BUILD_TREE.md · part of Control Tree INIT v1.2.0*
