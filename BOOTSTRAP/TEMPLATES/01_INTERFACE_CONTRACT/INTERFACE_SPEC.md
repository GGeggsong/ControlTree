# Interface Spec — {{INTERFACE_TYPE}}

CONTRACT_VERSION: **{{CONTRACT_VERSION}}**
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}
Interface Type: **{{INTERFACE_TYPE}}**

> 本檔為跨端介面的**單一真相**。任何端的實作若與本文不一致，**不要單方面改本文**；先進 `CHANGE_REQUESTS.md` 與 `ISSUES_BLOCKERS.md`。
>
> **註：** 若專案**沒有** BLE／REST 等通訊協定，請把「介面」理解成「幾條協作分支**必須對齊的同一份規格／承諾**」；下方各節可改寫為平面基準、財務門檻、業主需求等實際內容，不適用的節標 **N/A**。

---

## 1. 範疇

- 本檔用於：**{{SIDE_LIST_CSV}}** 之間須對齊的依據（通訊協定、空間／工法基準、對外合約要點等）。
- 本檔**不**包含：不必跨線對帳的單線細節、純單線流程（見各 `_SIDE/` 與 `04_PRODUCT_SPEC/`）。

## 2. 物理／傳輸層

> 例：BLE Advertising / GATT / RS-485 9600 8N1 / HTTPS REST / gRPC over HTTP/2 …

- TODO（請使用者或介面主導端補完）

## 3. 角色（Roles）

> 哪一端是 Central / Peripheral、Client / Server、Master / Slave、Producer / Consumer？

- TODO

## 4. 連線／會話（如適用）

- TODO

## 5. 主要指令／訊息類型

> 詳細指令表見 `COMMAND_TABLE.md`，本節僅列大類。

- TODO

## 6. 安全／鑑權

- TODO

## 7. 錯誤處理

> 詳細錯誤碼見 `ERROR_CODE.md`。

- TODO

## 8. 版本相容性

| Contract Version | 相容端 | 備註 |
|---|---|---|
| {{CONTRACT_VERSION}} | {{SIDE_LIST_CSV}} | 初始版本 |

## 9. 未決議題 / Need Verify

> 本節列出尚需驗證或決策的條目，並連結至 `ISSUES_BLOCKERS.md`。

- TODO
