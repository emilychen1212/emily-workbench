# emily-workbench 上架規則

所有 Claude（claude.ai 對話、Claude Code）都依本檔執行。完整背景見 `docs/交接給ClaudeCode.md`。

## 分工
- claude.ai 的 Claude：做內容，把檔案直接寫進本資料夾對應位置，並更新 `catalog.json`；不執行 git
- Claude Code：負責 repo 結構與首頁維護、commit、push
- Emily 對 Claude Code 說「推上去」時：`git status` 列出新增或修改的檔案 → 跑敏感資料檢查 → commit → push → 回報網址

## 結構
- 類型資料夾：`tools/`（可操作、會存資料）、`data/`（呈現資料）、`campaigns/`（給客戶參與）、`guides/`（教學）、`lab/`（實驗）
- 每個作品：`類型/YYYY-MM-英文短名/index.html`，資源放在同一個資料夾
- `catalog.json` 是首頁唯一的資料來源；有新作品就必須同步新增一筆

## catalog.json 欄位
`id`、`title`、`desc`（一句話，15 字內）、`type`（tools/data/campaigns/guides/lab）、`tags`（產品／對象：內部或客戶／狀態：使用中或已封存）、`date`（YYYY-MM）、`url`（repo 內作品用相對路徑）
- 選填 `pinned: true`：釘選，卡片排在最前面並顯示「釘選」標記。Emily 說「釘選／取消釘選 X」時加上或刪掉這個欄位，commit 用 `update(類型): 標題`。已封存的作品就算有釘選也照樣排在最後

## 上架前必做：敏感資料檢查
本 repo 為 Public。推送前掃描客戶聯絡人姓名、email、電話、報價金額、合約價、議價資訊。發現任何一項就先停下來列給 Emily，等她確認或改成去識別化之後才推。

## Commit 訊息
- 新增：`add(類型): 標題`
- 更新：`update(類型): 標題`
- 結構或首頁：`chore: 說明`
