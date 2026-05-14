# Version Policy

> 本中控樹有 **四軸版本**，互不混用。

## 1. SYNC_REV

- Format: `YYYY.MM.DD-NNN`
- Example: `2026.05.14-001`
- 規則：中控樹任一檔案有實質更新就遞增；同一天 NNN 從 `001` 起。

## 2. CONTRACT_VERSION（跨端介面）

- Format: `vMajor.Feature.Patch`
- Example: `v0.1.0`
- 規則：
  - **Patch**：僅文件修正、不影響行為。
  - **Feature**：新增／修改指令、欄位、payload、回應、notify、UUID、行為。
  - **Major**：合約穩定後的破壞性架構變更。
- 介面類型本專案為：**{{INTERFACE_TYPE}}**。

## 3. SIDE_VERSION（各端實作）

- Format: `<SIDE_UPPER>-x.y.z`
- 範例：`FW-1.2.3`、`IOS-1.0.0`、`ANDROID-0.4.1`
- 規則：各端維護；於 `<SIDE>_STATUS.md` 表頭宣告**目前支援的 `CONTRACT_VERSION`**。

## 4. PRODUCT_SPEC_VERSION（非介面之產品規格）

- Format: `vMajor.Feature.Patch`
- 範例：`v0.1.0`
- 規則：產品流程、商業規則、UI 行為等非封包層規格。

## 一致性檢查

每次更新時 AI 應自問：

- [ ] 這次改動有沒有牽動 `CONTRACT_VERSION`？
- [ ] 有沒有牽動某個 `SIDE_VERSION`？
- [ ] 有沒有牽動 `PRODUCT_SPEC_VERSION`？
- [ ] `SYNC_REV` 一定要加一。
