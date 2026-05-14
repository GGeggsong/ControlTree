# Data Format — {{INTERFACE_TYPE}}

CONTRACT_VERSION: **{{CONTRACT_VERSION}}**
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

> 各指令的**逐欄位**／**逐 byte** 格式定義。每變更一次格式都要遞增 `CONTRACT_VERSION`（至少 Feature）。

---

## 通用約定

- Byte Order: TODO（Big Endian / Little Endian）
- 字串編碼: TODO（UTF-8 / ASCII）
- Padding: TODO

## Per-Command Layout

### `<Command Name>` — `<Code>`

| Offset | Length | Field | Type | 說明 |
|---|---|---|---|---|
| 0 | 1 | `header` | u8 | TODO |
| 1 | … | … | … | TODO |

> 每加一個指令就新增一節，順序與 `COMMAND_TABLE.md` 對應。

---

## 變更記錄

- {{CONTRACT_VERSION}} ({{TODAY}})：初始版本。
