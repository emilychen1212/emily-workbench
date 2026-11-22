# emily-workbench 建置交接（給 Claude Code）

## 背景
- GitHub 帳號：emilychen1212，repo：`emily-workbench`（Public，已開 GitHub Pages）
- 網址：https://emilychen1212.github.io/emily-workbench/
- 用途：集中放 Emily 工作中製作的 HTML 工具、資料頁、活動頁、教學頁。之後每次確認「上架」就新增進來，不必再另外整理
- 既有的 `emily-work-system` repo 維持原樣，只在首頁放一張卡片連過去

## 一、資料夾結構
```
emily-workbench/
├── index.html          ← 首頁，讀 catalog.json 動態產生卡片
├── catalog.json        ← 作品清單（唯一資料來源）
├── CLAUDE.md           ← 上架規則（見第五節，任何 Claude 都依此執行）
├── README.md
├── tools/              ← 工具：可操作、會存資料
├── data/               ← 資料頁：整理、呈現資料，主要用來看
├── campaigns/          ← 活動頁：給客戶／使用者參與
├── guides/             ← 教學：操作手冊、講習頁
└── lab/                ← 實驗：草稿、試做
```
- 每個作品一個資料夾，命名 `YYYY-MM-英文短名/index.html`，例如 `tools/2026-11-booth-raffle/index.html`
- 作品引用的圖片等資源放在同一個資料夾內

## 二、catalog.json 格式
```json
{
  "updated": "2026-11-22",
  "items": [
    {
      "id": "emily-work-system",
      "title": "Emily 的工作管理系統",
      "desc": "工作、任務、推廣三套管理系統",
      "type": "tools",
      "tags": ["內部", "使用中"],
      "date": "2026-10",
      "url": "https://emilychen1212.github.io/emily-work-system/"
    }
  ]
}
```
- `type` 只能是：`tools` / `data` / `campaigns` / `guides` / `lab`
- `tags` 包含三種：產品（JoVE、LWW、Ovid…）、對象（內部／客戶）、狀態（使用中／已封存）
- repo 內的作品，`url` 用相對路徑，例如 `tools/2026-11-booth-raffle/`
- `desc` 只寫一句話，15 字以內

## 三、首頁 index.html 規格
- 單一 HTML 檔，不用 build 工具，用 fetch 讀 `catalog.json`
- 版面由上到下：標題列（Emily's workbench＋一句副標＋搜尋框）→ 各類型數量統計（4～5 格）→ 類型篩選按鈕（全部／工具／資料頁／活動頁／教學／實驗）→ 作品卡片 grid
- 卡片內容：類型標示（icon＋文字，每種類型一個顏色）、標題、描述、tags、日期，整張卡片可點擊開啟
- 搜尋範圍：title、desc、tags
- 排序：預設依 date 新到舊；「已封存」的卡片顏色變淡，排在最後
- 視覺：沿用 Emily 的個人風格，扁平、沉穩又帶點可愛，深藍（navy）主色、橘色點綴，與她的「教育訓練管理平台」一致
- 要支援手機版（RWD）

## 四、上架流程
Emily 說「上架」時，依序執行：
1. 判斷類型。依第一節的標準判斷，判斷不了就問 Emily
2. 放進 `類型/YYYY-MM-英文短名/index.html`
3. 在 HTML `<head>` 補上 `<title>`，以及 `<meta name="description">`
4. 在 `catalog.json` 新增一筆，並更新 `updated` 日期
5. 敏感資料檢查（必做）：掃描檔案內容，看有沒有客戶聯絡人姓名、email、電話、報價金額、合約價、內部議價資訊。有的話先停下來列給 Emily 看，經她確認或改成去識別化之後才推
6. Commit 訊息格式：`add(類型): 標題`，例如 `add(tools): 擺攤抽獎系統`
7. Push，並回報 GitHub Pages 網址（Pages 部署約需 1 分鐘）

更新既有作品時，commit 訊息用 `update(類型): 標題`，catalog 只改有變動的欄位。

## 五、請在 repo 建立 CLAUDE.md
內容就是第一、二、四節的規則精簡版。用意是讓 Claude Code、claude.ai 上的 Claude，或任何之後接手的 Claude 都遵守同一套規則。

## 六、第一批任務
1. 建立資料夾結構、`index.html`、`catalog.json`、`CLAUDE.md`、`README.md`，推上去並確認 Pages 正常顯示
2. 盤點 Emily 電腦上今年做過的 HTML 工具，列成清單（名稱、建議類型、是否含敏感資料），讓 Emily 勾選要上架哪些，再分批上架
