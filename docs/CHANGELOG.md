# Maxcareerportal — 更新日誌

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

- [ ] 填入真實個人資料（姓名、職涯內容、專案）
- [ ] 補充 About 卡片內容
- [ ] 新增真實文章連結至 Writing 區塊
- [ ] 部署至 Vercel / Cloudflare Pages
- [ ] 加入 OG meta tags（社群分享預覽）
- [ ] 手機版微調（Experience 格線）
