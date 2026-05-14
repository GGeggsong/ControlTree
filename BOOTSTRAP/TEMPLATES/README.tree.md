# {{PROJECT_NAME}}_ControlTree — Control Tree（中控樹）

> 本資料夾由 [Control Tree（中控樹）](https://github.com/) INIT v1.2.0 建立。

---

## 本機路徑

```
{{LOCAL_ROOT}}
```

儲存後端：**{{STORAGE_BACKEND}}** — 同步 SOP 見 `00_PROJECT_CONTROL/STORAGE_AND_SYNC.md`。

---

## 目錄架構

| 編號 | 資料夾 | 用途 | 維護者 |
|---|---|---|---|
| **00** | `00_PROJECT_CONTROL/` | 總狀態、任務、議題、版本、決策、儲存約定 | 輪值 |
| **01** | `01_INTERFACE_CONTRACT/` | 跨端介面單一真相（{{INTERFACE_TYPE}}） | 介面主導端 |
| **02** | `02_INTEGRATION_TEST/` | Feature Matrix、跨端 bug、整合測試計畫／log | Cross |
| **03** | `03_SKILLS_EXTRACTION/` | 可抽成通用 AI skill 的長文 | 維運 |
| **04** | `04_PRODUCT_SPEC/` | 非介面之產品／流程／商業規則 | 產品 |
| — | `_SHARED/` | **共用文件中心**：SOP、腳位圖、流程圖、規範、外部 datasheet、品牌素材；他處用相對連結引用，不複製 | 全體 |
| **05..98** | `0X_<SIDE>_SIDE/` | 各端現況、交接、測試、changelog、skill notes（第 1 個端 = `05_…`，第 2 個 = `06_…`，以此類推） | 該端 AI／開發者 |
| **99** | `99_ARCHIVE/` | 封存舊內容 | — |

本專案的端別清單：**{{SIDE_LIST_CSV}}**

---

## 建議閱讀順序（新視窗／新 AI／新成員）

1. `00_PROJECT_CONTROL/MASTER_STATUS.md`
2. `00_PROJECT_CONTROL/CURRENT_TASKS.md`
3. `00_PROJECT_CONTROL/SYNC_RULES.md`
4. `00_PROJECT_CONTROL/STORAGE_AND_SYNC.md`
5. `_SHARED/README.md`（共用 SOP／腳位／流程圖索引）
6. `01_INTERFACE_CONTRACT/INTERFACE_SPEC.md`（若任務涉及）
7. 對應 `0X_<SIDE>_SIDE/<SIDE>_STATUS.md`
8. `02_INTEGRATION_TEST/FEATURE_MATRIX.md`

---

## 版本

- `SYNC_REV`：見 `00_PROJECT_CONTROL/SYNC_HISTORY.md`
- `CONTRACT_VERSION`：見 `00_PROJECT_CONTROL/MASTER_STATUS.md`
- `<SIDE>_VERSION`：見各 `<SIDE>_STATUS.md`
- `PRODUCT_SPEC_VERSION`：見 `04_PRODUCT_SPEC/README.md`

---

## 怎麼換一隻 AI 接手

把這段話貼給新 AI：

```
請依 {{LOCAL_ROOT}}/README.md 與 00_PROJECT_CONTROL/MASTER_STATUS.md 接續協作。
任務是 <一句話描述>。動手前讀 SYNC_RULES.md。
```

AI 會自動掃完讀順序、執行任務、最後更新中控樹（含 SYNC_REV 遞增）。

---

*由 Control Tree（中控樹）INIT 建立於 {{TODAY}}，by {{AI_AGENT}}*
