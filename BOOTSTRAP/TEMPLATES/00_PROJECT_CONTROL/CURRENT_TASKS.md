# Current Tasks

Last Updated At: **{{TODAY}}**
Last Updated By: {{AI_AGENT}}

## Done

- [x] Control Tree（中控樹）初始化（`SYNC_REV {{SYNC_REV}}`）。

## Open — Contract & Spec

- [ ] **User**：補完 `01_INTERFACE_CONTRACT/INTERFACE_SPEC.md` 的「現有規格」與「主要指令／訊息」段落。
- [ ] **User**：若無正式介面，於 `INTERFACE_SPEC.md` 寫明「本專案目前無跨端介面」並標 `CONTRACT_VERSION` 永久 `v0.0.0`。

## Open — 各端 SIDE Status

{{SIDE_OPEN_TASKS_BLOCK}}

> 範例：
>
> - [ ] **Firmware AI**：填 `05_FIRMWARE_SIDE/FIRMWARE_STATUS.md` 之 Based On / 實作摘要 / Known Issues。
> - [ ] **iOS AI**：填 `06_IOS_SIDE/IOS_STATUS.md` 之 Based On / 實作摘要 / Known Issues。

## Open — Integration

- [ ] **All**：依端別填 `02_INTEGRATION_TEST/FEATURE_MATRIX.md` 初版（每列功能 + 各端狀態）。
- [ ] **User**：排第一次跨端整合測（時程、人員、目標）。

## User Decision Needed

- [ ] 是否啟用 `git` / `cloud-drive` 儲存後端？（目前：**{{STORAGE_BACKEND}}**）
- [ ] 是否新增其他端別？（目前：**{{SIDE_LIST_CSV}}**）

## Drive／協作

- [ ] 視儲存後端執行同步動作（見 `STORAGE_AND_SYNC.md`）。
