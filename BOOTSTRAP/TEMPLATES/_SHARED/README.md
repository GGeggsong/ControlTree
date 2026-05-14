# _SHARED · 全專案共用文件中心

Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

> **唯一原則**：任何「全專案 AI／開發者都需要知道」的非 md 規則／圖／PDF／流程，**都丟這裡**。
> 其他資料夾的 md 想用就**用相對連結指過來**，**絕不複製檔案**。
> 一份資產 = 一個檔 = 一個位置。

---

## 1. 適合放在這裡的東西

- **SOP 與流程**：軟體 release SOP、韌體燒錄 SOP、測試流程圖、issue 處理流程
- **硬體規格圖**：腳位設定圖（pinout）、PCB layout 截圖、接線示意、感測器配置
- **規範文件**：命名規則、Coding Style、Commit 慣例、品牌色卡、Logo
- **外部參考**：IC datasheet、認證 PDF、外部 standard、競品規格 PDF
- **跨模組流程圖**：系統架構圖、訊號流向、狀態機、時序圖（PNG / SVG / mermaid 原檔）
- **大型表格**：腳位分配 CSV、註冊表 Excel
- **任何「在多個 md 都會引用」的素材**

## 2. 不適合放這裡的東西

- 規格本文 → 放 `01_INTERFACE_CONTRACT/` 或 `04_PRODUCT_SPEC/`
- 某一端的私房筆記 → 放對應 `0X_<SIDE>_SIDE/<SIDE>_SKILL_NOTES.md`
- 議題追蹤 → 放 `00_PROJECT_CONTROL/ISSUES_BLOCKERS.md`
- 已淘汰的舊版資產 → 搬到 `99_ARCHIVE/`

## 3. 放置規則（簡單版，一人專案優化）

- **要不要分子資料夾，由你自己決定。** 預設可以全部平鋪在 `_SHARED/` 根。
- 若數量超過 ~20 個檔，再考慮分子資料夾（建議命名見 §5）。
- 檔名請有「主題前綴」，讓排序時相關檔聚在一起：
  - `pinout_main_mcu.png`
  - `pinout_dimmer_board.png`
  - `sop_release_firmware.md`
  - `sop_release_ios.md`

## 4. 怎麼從別的 md 引用 `_SHARED/`

一律用**相對路徑**。從中控樹的不同層級指過來：

- 從 `01_INTERFACE_CONTRACT/INTERFACE_SPEC.md`：
  ```markdown
  ![pinout](../_SHARED/pinout_main_mcu.png)
  [燒錄 SOP](../_SHARED/sop_firmware_flash.md)
  ```
- 從 `05_FIRMWARE_SIDE/FIRMWARE_STATUS.md`：
  ```markdown
  ![timing](../_SHARED/timing_ble_adv.svg)
  ```
- 從根目錄 `README.md`：
  ```markdown
  [品牌色卡](./_SHARED/brand_palette.pdf)
  ```

**不要複製檔案到別的資料夾**，否則一份資產有兩個來源，永遠會漂移。

## 5. （可選）子資料夾建議

當數量大了再分。建議命名以**用途**為主，不要以「給哪個端用」為主（因為共用就是共用）：

```
_SHARED/
├── README.md           ← 本檔（索引）
├── sop/                ← 標準作業流程
├── pinout/             ← 腳位／接線圖
├── flow/               ← 系統流程圖、狀態機、時序圖
├── reference/          ← 外部 datasheet、PDF
├── brand/              ← Logo、品牌素材
└── data/               ← 大型表格、CSV
```

但**完全可以省略**，全部平鋪也行。

## 6. 索引（請列出 _SHARED/ 內現有檔案，方便 AI 動手前掃一眼）

> AI 每次新增／更新檔案後，請在本表加一行。表是給「動手前 30 秒掃一眼」的，不必鉅細靡遺。

| 檔名 | 主題 | 誰會用 | 最近更新 |
|---|---|---|---|
| — | （尚無） | — | — |

> 範例：
>
> | `pinout_main_mcu.png` | 主 MCU 腳位 | firmware, hardware | {{TODAY}} |
> | `sop_release_firmware.md` | 韌體 release SOP | firmware, user | {{TODAY}} |
> | `flow_ble_pairing.svg` | BLE 配對流程 | firmware, ios, android | {{TODAY}} |

## 7. 同步行為

- **`_SHARED/` 不另管儲存**：與整棵中控樹相同，預設就是**本機磁碟上的檔案**；不必為共用資料夾再選一套 Git／雲端規則。
- **換機／換環境**：請**整包**備份或複製整棵 `<ProjectName>_ControlTree/`（務必含 `_SHARED/`）。若你希望省力，改由 `00_PROJECT_CONTROL/STORAGE_AND_SYNC.md` 所述，對**整棵樹**啟用 `git` 或 `cloud-drive` 即可。
- **一人本機**：直接丟、直接改；動手後更新本檔 §6 索引。

## 8. 大檔案 / 二進位

- Git 後端：建議用 Git LFS（`.gitattributes` 加 `_SHARED/**/*.{pdf,png,jpg,svg,mp4} filter=lfs diff=lfs merge=lfs -text`）。
- 雲端硬碟後端：不必特別處理。
- 本地後端：注意週期備份。
