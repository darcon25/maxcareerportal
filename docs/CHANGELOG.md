# Maxcareerportal — 更新日誌

## v0.7 — 部署遷移至 Cloudflare Pages
**日期：** 2026-10-20

### 背景
- Zeabur 宣布 2026 年底停止營運，網站由 Zeabur 遷移至 Cloudflare Pages。

### 部署
- **平台：** Cloudflare Pages（專案名稱 `maxliucareer`），連接 GitHub repo，`main` push 後自動部署，不再使用 ghcr.io image。
- **建置：** build command 將網站檔案複製到 `dist/`，排除 `docs/`、隱藏檔與 `Dockerfile`。
- **線上網址：** https://maxliucareer.pages.dev/

### 內容修正
- `index.html` 的 `canonical` 與 `og:url` 由 `maxliucareer.zeabur.app` 改為 `maxliucareer.pages.dev`。

---

## v0.6 — 中英雙語切換 + 對外上線
**日期：** 2026-08-05
**來源履歷：** `Position_Product management ChienTsungLiu (Max) July 2026.docx`

### 雙語功能（i18n）
- **隔離方式**：雙區塊 CSS 顯示切換。可翻譯文字包中／英兩份（`t-zh`/`t-en`），`<html>` 掛 `lang-zh`/`lang-en`，CSS 只顯示對應語言。
- **自動偵測**：首次進站讀 `navigator.language`。**預設邏輯：`zh` 開頭 → 中文；其餘全部（英文、日文、德文…）→ 英文**（適合對外分享，非中文語系一律英文）。
- **手動切換**：nav 右上角「中／EN」按鈕（`toggleLang()`），選擇存 `localStorage['site-lang']`，重整後記憶。
- **防護**：`localStorage` 讀寫加 `try/catch`，並驗證存值只接受 `zh`/`en`（避免極端瀏覽器出現中英並存）。
- **經驗分享簡報**：中英文版皆隱藏 nav 按鈕，簡報內容不翻譯（在地化演講，短期用不到）。

### 英文文案
- 全站英文改寫為道地 portfolio 語感，去除翻譯腔（hero「Law by training, product by trade.」、About 開場、GSP 條目等），關鍵數據保留（15 年、100+ 團隊、300+ PCR/gen、30K 觀看、4/5 星、10+ 世代 NPI）。

### 內容修正
- **Pioneer 專案卡**：從 Dell 改為 **LC Futurecenter**，三亮點 **Wave 1 / Healthcare Platform / GPU Raw Card**，移除 Edge 與「跨部門緊急修復排程機制」句。
- **Hero 數據**：企業數 6 → **5**（Qisda、Elite、LC Futurecenter、GSP Tech、Dell）。
- **Dell 時間軸標籤**：改為 PowerEdge Server / Storage Server / NativeEdge / IT Tool Development。

### 部署
- 走 ghcr.io 預建 image（`ghcr.io/darcon25/maxcareerportal:latest`，amd64）+ Zeabur 重啟，非 git push。
- **線上網址：** https://max-career-portal.zeabur.app/

---

## v0.5 — 配色改版 方案C 書布褐（暖亮色）
**日期：** 2026-08-04

- 整站深色 Linear 風 → 亮色暖書布褐（參考 Claude 官網）。
- Token：bg `#EDE8DC`、fg `#26231D`、muted `#56534B`、dim `#7A7466`、accent 深赤陶 `#C15F3C`、accent-2 橄欖 `#7C7A52`。
- 一併調整：hero 漸層（赤陶→brass）、時間軸打燈動畫、能力地圖 SVG 三群配色、nav 毛玻璃、標籤與內文加深提升可讀性。
- 簡報 overlay（經驗分享）維持深色劇場、只覆寫 token。

---

## v0.4 — 真實履歷資料填入
**日期：** 2026-06-09  
**來源：** `LATEST Position_Product_Project management ChienTsungLiu (Max) 2026.docx`

### 內容更新
- **頁面標題**：`Max.CT.Liu — Legal-Tech PM · Curious by Design`
- **Nav Logo**：`Max.CT.Liu.`
- **Hero 標題**：從法律出發與科技交叉的 **Curious by Design**
- **Hero 副標**：補入真實職涯軌跡一句話說明
- **Hero 數據**：15+ 年 / 6 間企業 / 3 跨越領域 / 100+ 跨團隊協作
- **About 卡片**：填入 n8n、Vibe Coding、汐止、Legal-Tech PM 等真實內容
- **Experience**：完整 5 段職涯（Dell / LC Futurecenter×2 / GSP Tech / Elite+Qisda）
- **Skills**：Technical PM / Product / AI & Domain 三欄真實技能
- **Projects**：Talkimate、Dell IT Tool、Edge Platform、Maxcareerportal 本站
- **Contact Email**：`Chientsungliu@gmail.com`
- **Footer**：加入 Pexels 圖片出處標示

### DESIGN.md 同步更新
- 完整填入個人身份、職涯時間軸、學歷、技能地圖、核心專案
- 列出待補項目：LinkedIn、GitHub、Twitter、社群人數、Writing 文章

---

> 紀錄每次重要迭代的內容與決策原因

---

## v0.3 — Pexels 真實照片整合
**日期：** 2026-06-09

- 替換 Hero 區塊圖像：移除 Python 繪製的示意圖，改用 Pexels 真實會議照片
- 圖片來源：[Photo by Thirdman on Pexels](https://www.pexels.com/photo/a-group-of-people-having-a-meeting-in-the-office-7652049/)（Free License）
- 圖片透過 Pexels CDN 直接載入，不需下載本地檔案

---

## v0.2 — Linear 設計語言 + 標題更新
**日期：** 2026-06-09

**設計參考：** [linear.app](https://linear.app) hero section（via saaspo.com）

### 視覺改動
- 背景改為 Linear 官方 theme-color `#08090a`
- Hero 加入徑向光暈（violet `rgba(139,92,246,0.18)` + blue `rgba(59,130,246,0.10)`）
- 加入點陣紋理背景（dot grid + mask 漸隱）
- Announcement chip：膠囊型 badge，帶 monospace label
- 標題漸層字：`linear-gradient(90deg, #c4b5fd, #93c5fd)`
- 章節編號系統：`1.0 About` / `2.0 Experience` 等

### 內容改動
- Hero 標題改為「從法律出發與科技交叉的**專案經理**」
- Hero 副標更新呼應法律 × 科技背景

### 套用 Open Design color.md 規範
- 邊框：`rgba(255,255,255,0.08)` 半透明白邊
- Accent 限制：最多 2 個明顯使用點（nav logo + CTA 按鈕）
- 字體顏色命名以用途命名（`--fg`, `--muted`, `--dim`）

---

## v0.1 — 初始原型
**日期：** 2026-06-09

### 架構
- 單頁 HTML，無外部依賴（除 Google Fonts）
- 頁面結構：Nav → Hero → About → Experience → Skills → Projects → Writing → Contact → Footer

### 設計決策
- 極簡技術感（Vercel / Linear 風格）
- 跨領域背景展示（Technical / Product / Domain 三欄技能區）
- 社群品牌導向（Writing 區塊展示思考深度）
- 字型：Inter（內文）+ JetBrains Mono（程式碼、標籤）

---

## 待辦 / 下一步

- [x] 填入真實個人資料（姓名、職涯內容、專案）— v0.4
- [x] 補充 About 卡片內容 — v0.4
- [x] 部署上線 — v0.6（Zeabur + ghcr.io image，非 Vercel）
- [x] 中英雙語切換 — v0.6
- [x] 部署遷移至 Cloudflare Pages — v0.7
- [ ] `main` push 到 GitHub 同步 GitHub Pages 備份（目前領先 origin/main）
- [ ] 新增真實文章連結至 Writing 區塊
- [ ] 加入 OG meta tags（社群分享預覽）
- [ ] 手機版微調（Experience 格線）
