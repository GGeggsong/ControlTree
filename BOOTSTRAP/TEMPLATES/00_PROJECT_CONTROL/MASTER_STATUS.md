# MASTER STATUS

SYNC_REV: **{{SYNC_REV}}**
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}
Current Phase: **Initialized**

## AI_SYNC_ROOT（本機）

| 環境 | 路徑 | 備註 |
|---|---|---|
| {{OS}} | `{{LOCAL_ROOT}}` | 由 Control Tree（中控樹）INIT 建立 |

> 若有多台機器使用同一棵樹（例如雲端硬碟同步），每台都加一列。

## Current Contract Version

`{{INTERFACE_TYPE}}_CONTRACT_VERSION`: **{{CONTRACT_VERSION}}**

## Current Side Versions

{{SIDE_VERSIONS_BLOCK}}

> 範例：
>
> - `FW_VERSION`: `FW-0.0.0`（Need Verify）
> - `IOS_VERSION`: `IOS-1.0.0`
> - `ANDROID_VERSION`: `ANDROID-0.0.0`（Need Verify）

## Product Spec Version

`PRODUCT_SPEC_VERSION`: **{{PRODUCT_SPEC_VERSION}}**

## Latest Change

**{{SYNC_REV}}**：Control Tree（中控樹）初始化（by {{AI_AGENT}}）。建立核心 6 個資料夾與 {{SIDE_COUNT}} 個 SIDE 資料夾；儲存後端為 **{{STORAGE_BACKEND}}**。

## Action Required

1. **User**：補齊 `01_INTERFACE_CONTRACT/INTERFACE_SPEC.md` 的「現有規格」段落。
2. **各端 AI**：填 `0X_<SIDE>_SIDE/<SIDE>_STATUS.md` 之 `Based On Contract Version` 與目前實作摘要。
3. **All**：審視 `CURRENT_TASKS.md` 並認領。

## Current Next Owner

**User**（決定首批 contract 內容與端別現況）。

## Current Blockers（摘要）

無；待 `01_INTERFACE_CONTRACT/` 與各端 `STATUS.md` 補完後重評。

## Notes

- 本檔為**整棵中控樹的儀表板**。任何更新都應同步反映此處的 `SYNC_REV` 與 `Latest Change`。
- 儲存後端與同步 SOP 見 `STORAGE_AND_SYNC.md`。
