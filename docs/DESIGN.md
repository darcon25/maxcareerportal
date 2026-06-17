# Maxcareerportal — DESIGN.md
> Open Design 規格文件。定義品牌語言與個人定位。最後更新：2026-06-10

---

## 身份定位

| 欄位 | 內容 |
|------|------|
| **顯示名稱** | Max.CT.Liu |
| **全名** | Chien-Tsung Liu (Max) |
| **職稱** | Advisory Project Manager → Legal-Tech PM |
| **Hero 標題** | Curious by Design |
| **About 副標** | 從科技法律出發的光華商場 DIY 玩家踏入台灣最肝苦產業，在硬體 NPI 的世界裡磨出產品研發的技術直覺，在無數的電話會議中淬鍊出說故事的藝術，再到 AI 自動化時代的自我重塑。每一次選擇的結果，是從來沒有放棄的跨界累積。 |
| **所在地** | 新北市汐止，Taiwan |
| **Email** | chientsungliu@gmail.com |
| **GitHub** | https://github.com/darcon25 |
| **LinkedIn** | https://www.linkedin.com/in/max-chien-tsung-liu-4b7042103/ |
| **目標受眾** | 業界社群、LegalTech / HardTech 合作夥伴 |

---

## 職涯時間軸

| 期間 | 職稱 | 公司 | Tags |
|------|------|------|------|
| 2021 Nov – 2026 Jan | Advisory Project Manager | Dell Technology (Taiwan) | PowerEdge Server、Edge Solution、Healthcare Platform |
| 2018 Nov – 2021 Nov | Advisory Project Manager | Lenovo (LC Futurecenter) | ThinkPad T Series、Mobile Workstation P、Technical PM、Development PM、Product Core Team |
| 2015 Nov – 2018 Nov | Product Manager | GSP Tech Co., Ltd *(Taiwan Startup)* | Talkimate SPK Mic、Kickstarter Crowdfunding、Amazon Selling Channel |
| 2012 Nov – 2015 Nov | Staff Project Manager | Lenovo (LC Futurecenter) | ThinkPad X1、IdeaPad、Commercial NB |
| 2011 Jun – 2012 Nov | Project Specialist | Elite Computer | — |
| 2010 Nov – 2011 May | Project Specialist | Qisda Corporation | — |

---

## 學歷

| 期間 | 學校 | 學位 |
|------|------|------|
| 2009 – 2010 | University of Wollongong, AUS | Master in Project Management |
| 2000 – 2005 | Chung Yuan University, TW | Financial Law |

---

## 四大 Highlight（About 區塊）

| # | 標題 | 說明 |
|---|------|------|
| 01 · ODM | 豐富的 ODM 專案經驗 | NB、Server、Display、Workstation 跨多產品線，主導超過 10 世代 NPI 全流程，從 RFQ 到 MP 無斷點交付。 |
| 02 · Brand | 品牌廠工作模式理解 | 在 Dell 台灣直接對接品牌端，熟悉品牌採購決策、工程需求轉譯與跨時區溝通節奏。 |
| 03 · AI | AI 工具應用實作 | n8n 自動化流程、Claude Code Vibe Coding、LLM prompt 工程，將 AI 工具真正落地進日常工作。 |
| 04 · Problem | 問題解決能力 | 300+ PCR 處理經驗，跨部門衝突解決，擅長把複雜的技術與商業問題說得讓所有人聽懂。 |

---

## 技能地圖

### Technical
- Dell Server Platform HW Development
- Edge SW Solution Development
- ODM Management & NRE Budget Audit
- NPI Program Budget Planning
- Internal IT Tool Development (SW Spec / UI)

### Product
- Product Lifecycle Management (end-to-end)
- Crowdfunding & Go-to-Market (Kickstarter)
- PCR / Scope Change Management (~300/generation)
- Cross-functional Issue Resolution
- Global Offering Matrix Management

### AI & Emerging
- Automation tool: **n8n** deployment
- Vibe Coding via LLM (**Claude Code**, Codex)
- AI tool adoption & self-learning capability

### Domain Knowledge
- Financial Law (Chung Yuan University)
- HardTech: NB / Server / Display / Workstation
- LegalTech × PM cross-domain positioning

---

## Hero 數據統計

| 數字 | 標籤 |
|------|------|
| 15+ | 年工作經驗 |
| 6 | 間企業歷練 |
| 3 | 跨越領域（法律 / 科技 / 產品） |

---

## 核心專案

| 專案 | 說明 | 連結 |
|------|------|------|
| Talkimate | Kickstarter 群眾募資 SPK Mic，Amazon 4/5 顆星，YT 3萬觀看 | [Kickstarter](https://www.kickstarter.com/projects/595987921/talkimate-the-stylish-accessory-for-smartphone-wal/rewards?lang=zh) |
| Dell Internal IT Tool | SW spec 整合、UI/UX 優化、內部開發團隊溝通 | — |
| Edge / Healthcare Platform | Pioneer feature dev：Healthcare、GPU Card、Edge Solution | — |

---

## 色彩系統（Open Design color.md 規範）

| Token | 值 | 說明 |
|-------|----|------|
| `--bg` | `#08090a` | Linear 官方 bg |
| `--surface` | `#111214` | 卡片 / Nav |
| `--border` | `rgba(255,255,255,0.06)` | 半透明白邊 |
| `--border-hi` | `rgba(255,255,255,0.12)` | hover 邊框 |
| `--fg` | `#ededed` | 主文字 |
| `--muted` | `#888888` | 次要文字 |
| `--accent` | `#6ee7b7` | 薄荷綠，每頁最多 2 個明顯使用點 |

### Anti-patterns
- ❌ `#6366f1` indigo — OD AI-slop 告示色
- ❌ Accent 超過 2 個明顯使用點
- ❌ 純黑 `#000` / 純白 `#fff`

---

## 動畫規格（Timeline Spotlight）

- **模式**：Spotlight — 依序打燈，每個節點爆發 `box-shadow` 光暈 + 2 環擴散
- **Cycle**：12.5s（5 節點 × 2.5s offset）
- **觸發區間**：前 22% 發生脈衝，其餘 idle
- **Delay 順序**：

| 節點 | `--pd` |
|------|--------|
| Qisda / Elite | 0s |
| LCFC 2012–2015 | 2.5s |
| GSP Tech | 5s |
| Lenovo 2018–2021 | 7.5s |
| Dell | 10s |

- **Dell 差異**：使用 `tl-dot-spotlight-accent`，綠色光暈 `rgba(110,231,183,0.65)`，強度 2×

---

## 部署計畫

| 項目 | 內容 |
|------|------|
| **平台** | [Zeabur](https://zeabur.com) |
| **類型** | 靜態網站（Static Site） |
| **來源** | 單一 `index.html` 檔案 + `zbpack.json` |
| **狀態** | ✅ 已上線 |
| **正式網址** | https://maxliucareer.zeabur.app/ |

### 部署步驟（備忘）
1. 在 Zeabur 建立新 Project
2. 選擇 Static 服務類型
3. 上傳 `Maxcareerportal/` 資料夾或連結 GitHub repo
4. 設定自訂 Domain（如有）

---

## 已完成項目

- [x] Linear.app 設計語言套用（bg、typography、glow）
- [x] 公司 Logo 帶（Qisda、Elite、Lenovo、GSP Tech、Dell — 全部 inline SVG / base64）
- [x] 職涯時間軸 Spotlight 動畫（12.5s 循環，5 節點依序打燈）
- [x] About 四大 Highlight 卡片（數字柱 A 方案）
- [x] 連絡方式：Email / GitHub / LinkedIn 連結完整
- [x] Writing 區塊已移除
- [x] Zeabur 部署上線

## 待補資訊

- [ ] 個人照片（Hero 圓形頭像）
- [ ] 社群追蹤人數（選填）

---

## 開發歷程紀錄

### 階段一：骨架建立
從零建立單一 `index.html` 靜態網頁，套用 Linear.app 設計語言：`#08090a` 深黑背景、Inter 字型、Violet + Blue hero glow、dot grid 底紋。建立 `DESIGN.md` 規格文件與 `zbpack.json` 部署設定，部署至 Zeabur 上線。

### 階段二：Logo 帶
原用 Clearbit CDN → 失效 → 改 Simple Icons CDN → 也失效。最終全部改為 inline SVG 手刻 + Dell logo 用 base64 PNG 嵌入，零外部依賴。

| 公司 | 實作方式 |
|------|---------|
| Qisda | Nunito 字型，`fill="#1078C8"` |
| Elite | 橘色 swoosh SVG path + 藍字 `#1A3A8F` |
| Lenovo | Inter 字型，`fill="#E2231A"` |
| GSP Tech | 幾何方框 SVG |
| Dell | base64 PNG 嵌入（`dell--600.png`） |

### 階段三：時間軸動畫演進
三輪迭代：靜態節點 → 三層漣漪擴散環 → 最終 Spotlight 架構。

核心技術：CSS custom property `--pd` 掛在 `.tl-row`，cascade 給所有子元素與 pseudo-element，5 節點 × 2.5s offset，12.5s 一輪循環。Dell 起初獨立 2.2s 持續跳動，後改為加入共用節奏（`--pd: 10s`）。

```css
.career-timeline > .tl-row:nth-child(2) { --pd: 0s; }
.career-timeline > .tl-row:nth-child(3) { --pd: 2.5s; }
.career-timeline > .tl-row:nth-child(4) { --pd: 5s; }
.career-timeline > .tl-row:nth-child(5) { --pd: 7.5s; }
.career-timeline > .tl-row:nth-child(6) { --pd: 10s; } /* Dell */
```

### 階段四：Spotlight 動畫
提供 5 種互動 demo，使用者選擇 B — 光暈掃過（Glow Sweep / Spotlight）。

實作：`box-shadow` 為主視覺，2 環擴散為輔（第 3 環停用），idle 時文字 `opacity: 0.72`，打燈提亮至 1。Dell 使用 `tl-dot-spotlight-accent`，綠光強度 2×。

| Keyframe 名稱 | 用途 |
|--------------|------|
| `tl-dot-spotlight` | 一般節點本體 |
| `tl-dot-spotlight-accent` | Dell 節點（綠光加強） |
| `tl-ring-1` | 第 1 環（快速射出） |
| `tl-ring-2` | 第 2 環（餘暉散去） |
| `tl-text-spotlight` | 文字依序提亮 |

### 階段五：內容調整
- About 區塊：從「正在建造 / 所在地 / 專注領域 / 側邊能量」→ 四大 Highlight 數字柱（A 方案，3 種版型 demo 後採用）
- Hero 副標：改為「從科技法律出發的光華商場 DIY 玩家踏入台灣最肝苦產業…」
- GSP Tech 公司名加 `· Taiwan Startup` monospace 小字
- LCFC 2018–2021 tag：ODM Management → Technical PM / Development PM / Product Core Team
- GSP Tech tag：Kickstarter → Kickstarter Crowdfunding、Amazon → Amazon Selling Channel
- Writing 區塊整個移除
- 聯絡資訊：Email `chientsungliu@gmail.com`、GitHub https://github.com/darcon25、LinkedIn https://www.linkedin.com/in/max-chien-tsung-liu-4b7042103/、Twitter/X 移除

### 當前狀態（2026-06-10）
- 單一 `index.html`，零外部 CDN（僅 Google Fonts）
- 部署：https://maxliucareer.zeabur.app/（Zeabur Static Site）
- 本機路徑：`/Users/mmfamily/Downloads/Maxcareerportal/`
- 主要檔案：`index.html`、`docs/DESIGN.md`、`zbpack.json`
- 唯一待補：個人頭像照片
