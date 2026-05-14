# Command Table — {{INTERFACE_TYPE}}

CONTRACT_VERSION: **{{CONTRACT_VERSION}}**
Last Updated By: {{AI_AGENT}}
Last Updated At: {{TODAY}}

> 跨端互通的指令／訊息類型清單。**byte-level / field-level** 細節在 `DATA_FORMAT.md`。

---

## 指令清單

| Code / Name | 方向 | 簡述 | Payload 概要 | 回應 | Since | Notes |
|---|---|---|---|---|---|---|
| — | — | （尚無，待補） | — | — | {{CONTRACT_VERSION}} | — |

> 範例（BLE）：
>
> | `0x10` BrightnessControl | App → Light | 設定亮度／色溫 | brightness(1) + cct(1) + dstId(2) + password(4) | broadcast ack | v0.1.0 | — |

> 範例（REST）：
>
> | `POST /v1/devices/{id}/state` | Client → Server | 修改裝置狀態 | JSON `{ state: on/off }` | 200 / 4xx | v0.1.0 | 需 Bearer token |

## 變更記錄

- {{CONTRACT_VERSION}} ({{TODAY}})：初始版本。
