# 06 Skills Extraction

> 把長對話、長解說、長 debug 過程**萃取**成可重用的 AI skill 知識；不混入日常 STATUS 或 CHANGELOG。

---

## 何時新增一份 Skill 檔

- AI 解了一個費時的 bug，過程涵蓋多 layer → 萃取一份 `BUG_FIX_<topic>.md`。
- 某個 domain（如 BLE 廣播解析、Auth 流程）反覆出現 → 萃取一份 `DOMAIN_<topic>.md`。
- 新加入的 AI 經常問同樣的問題 → 萃取一份 `ONBOARDING_<topic>.md`。

## 命名建議

- `BUG_FIX_<topic>.md`
- `DOMAIN_<topic>.md`
- `ONBOARDING_<topic>.md`
- `RECIPE_<topic>.md`

## 內容格式

```markdown
# <Topic>

## 背景／問題
## 關鍵知識
## 步驟
## 易犯錯誤
## 參考
```

## 與其他資料夾的分工

- **`05_<SIDE>_SIDE`～`98_<SIDE>_SIDE/<SIDE>_SKILL_NOTES.md`**：該端的私房知識。
- **本資料夾**：跨端／通用、可被打包成 AI skill 給多個專案重用的長文。
