# 中英文切換 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 讓 MaxCareerPortal 單檔靜態站支援中／英雙語，首次進站依瀏覽器語言自動選擇，並提供手動切換按鈕（記憶於瀏覽器）。

**Architecture:** A 案雙區塊 CSS 顯示切換。`<html>` 掛 `lang-zh` / `lang-en` class（由 `<head>` inline script 在渲染前即設定，避免閃爍）。可翻譯文字提供兩份，中文標 `class="t-zh"`、英文標 `class="t-en"`；CSS 依 `<html>` 的 class 隱藏非當前語言。未加 `t-zh/t-en` 的內容（多數 tag、公司名、職稱）在兩種語言都顯示。

**Tech Stack:** 純 HTML + 內嵌 CSS + 原生 JS（vanilla），無框架、無建置流程。單檔 `index.html`。

## Global Constraints

- 只改 `/Users/mmfamily/Maxcareerportal/index.html`，不新增檔案、不引入函式庫。
- 語言 class 掛在 `<html>`（`document.documentElement`），選擇器一律 `html.lang-zh` / `html.lang-en`。
- 內容語言 class 固定用 `t-zh`（中文）、`t-en`（英文），不要用別的名稱。
- `localStorage` key 固定為 `site-lang`，值只有 `zh` 或 `en`。
- 英文文案：履歷式簡潔專業，**關鍵點不可漏**（數據如 300+ PCR/gen、Amazon 4/5 星、30K 觀看、100+ 跨團隊、10+ 世代 NPI 都要保留）。
- 不翻譯「經驗分享」簡報（lines ~1494–1657）；該功能的 nav 按鈕在中英文模式都隱藏。
- 不動既有配色（未提交的 index.html 視覺變更）；本計畫只疊加雙語。
- 每個 Task 完成後用瀏覽器實測（`cd /Users/mmfamily/Maxcareerportal && python3 -m http.server 8777` → `http://localhost:8777/`），再 commit。
- 注意：`index.html` 目前含未提交的配色改版，第 1 個 commit 會一併帶入這些配色變更（同一檔案無法分離），這是預期且可接受的。

---

### Task 1: i18n 基礎建設（偵測 + CSS + 切換鈕 + 隱藏經驗分享）

**Files:**
- Modify: `index.html`（`<head>` 內、`<style>` 內、nav `<div class="nav-links">`、`</body>` 前的 script 區）

**Interfaces:**
- Produces: `<html>` 上的 `lang-zh`/`lang-en` class；全域 CSS 規則 `html.lang-zh .t-en{display:none}` / `html.lang-en .t-zh{display:none}`；全域 JS 函式 `toggleLang()`；`localStorage['site-lang']`。後續所有翻譯 Task 依賴此 class 與 CSS。

- [ ] **Step 1: 在 `<head>` 最前面（`<meta charset>` 之後）插入偵測 script**

在 `index.html` 的 `<head>` 內，緊接在 charset meta 後加入：

```html
  <script>
    (function () {
      var saved = localStorage.getItem('site-lang');
      var nav = (navigator.language || '').toLowerCase();
      var lang = saved || (nav.indexOf('en') === 0 ? 'en' : 'zh');
      var root = document.documentElement;
      root.classList.add('lang-' + lang);
      root.setAttribute('lang', lang === 'en' ? 'en' : 'zh-TW');
    })();
  </script>
```

（原本 `<html lang="zh-TW">` 的靜態屬性保留無妨，script 會覆寫。）

- [ ] **Step 2: 在 `<style>` 內加入語言顯示規則**

在既有 `<style>` 區塊末端加入：

```css
/* ── i18n 語言切換 ── */
html.lang-zh .t-en { display: none !important; }
html.lang-en .t-zh { display: none !important; }
/* 語言切換按鈕 */
.nav-lang-btn {
  background: transparent;
  border: 1px solid var(--border);
  color: var(--muted);
  font-family: var(--mono);
  font-size: 0.72rem;
  padding: 0.3rem 0.6rem;
  border-radius: 6px;
  cursor: pointer;
  margin-left: 0.5rem;
  transition: color .2s, border-color .2s;
}
.nav-lang-btn:hover { color: var(--accent); border-color: var(--accent); }
```

- [ ] **Step 3: 在 nav 加入切換按鈕，並隱藏「經驗分享」按鈕**

在 `index.html` 找到（約 line 959）：

```html
        <button class="nav-share-btn" onclick="openPresentation()">經驗分享 ✦</button>
```

改為（加 `style="display:none"` 隱藏，並在其後新增語言按鈕）：

```html
        <button class="nav-share-btn" onclick="openPresentation()" style="display:none">經驗分享 ✦</button>
        <button class="nav-lang-btn" onclick="toggleLang()" aria-label="Switch language"><span class="t-zh">EN</span><span class="t-en">中</span></button>
```

（按鈕文字：中文模式顯示 `EN`＝點我切英文；英文模式顯示 `中`＝點我切中文。）

- [ ] **Step 4: 在 `</body>` 前的 `<script>` 區加入 `toggleLang()`**

在既有主 script 區塊內（與 `openPresentation` 等函式同層）加入：

```js
    function toggleLang() {
      var root = document.documentElement;
      var next = root.classList.contains('lang-en') ? 'zh' : 'en';
      root.classList.remove('lang-zh', 'lang-en');
      root.classList.add('lang-' + next);
      root.setAttribute('lang', next === 'en' ? 'en' : 'zh-TW');
      localStorage.setItem('site-lang', next);
    }
```

- [ ] **Step 5: 瀏覽器實測**

啟動 `python3 -m http.server 8777`（於專案根目錄），開 `http://localhost:8777/`：
- 預期：頁面正常顯示（此時全站中文，因內容尚未加 `t-zh/t-en`）。
- nav 右側出現 `EN` 按鈕；「經驗分享」按鈕消失。
- 點 `EN`：按鈕變 `中`，`<html lang>` 變 `en`（可在 DevTools Elements 確認），頁面內容此時仍為中文（正常，內容未翻）。
- 重新整理：維持上次語言（localStorage 生效）。
- DevTools Console 執行 `localStorage.setItem('site-lang','en');location.reload()` → 確認記憶優先於瀏覽器語言。

- [ ] **Step 6: Commit**

```bash
cd /Users/mmfamily/Maxcareerportal
git add index.html docs/DESIGN.md
git commit -m "feat(i18n): 語言切換基礎建設（偵測/CSS/切換鈕），隱藏經驗分享按鈕"
```

---

### Task 2: Hero 與 Stats 雙語

**Files:**
- Modify: `index.html`（hero-sub 約 974–977、stats strip 約 1052–1068）

**Interfaces:**
- Consumes: Task 1 的 `t-zh/t-en` CSS 規則。

- [ ] **Step 1: hero-sub 加英文版**

找到（約 974–977）：

```html
      <p class="hero-sub">
        文科法學背景出發，歷經 Qisda、Elite、LC Futurecenter、GSP Tech、Dell，<br>
        橫跨硬體 NPI、產品管理到 AI 自動化。15 年，持續進化中。
      </p>
```

改為兩份：

```html
      <p class="hero-sub t-zh">
        文科法學背景出發，歷經 Qisda、Elite、LC Futurecenter、GSP Tech、Dell，<br>
        橫跨硬體 NPI、產品管理到 AI 自動化。15 年，持續進化中。
      </p>
      <p class="hero-sub t-en">
        From a humanities and law background through Qisda, Elite, LC Futurecenter, GSP Tech and Dell —<br>
        spanning hardware NPI, product management and AI automation. 15 years, still evolving.
      </p>
```

- [ ] **Step 2: 四個 stats 標籤加英文版**

四個標籤分別在 label div 內包中英兩份 span。找到每個（約 1055/1059/1063/1067）：

```html
          <div style="font-size:0.72rem;color:var(--dim);margin-top:0.2rem">年工作經驗</div>
```
改為：
```html
          <div style="font-size:0.72rem;color:var(--dim);margin-top:0.2rem"><span class="t-zh">年工作經驗</span><span class="t-en">Years experience</span></div>
```

其餘三個同法，英文對應：
- `間企業歷練` → `Companies`
- `跨越領域` → `Domains`
- `跨團隊協作` → `Cross-team POCs`

- [ ] **Step 3: 瀏覽器實測**

重整 `http://localhost:8777/`，切到 EN：hero 副標與四個數字標籤變英文；切回中：恢復中文。數字（15+/6/3/100+）兩語不變。

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat(i18n): Hero 副標與 stats 標籤雙語"
```

---

### Task 3: About 區塊雙語

**Files:**
- Modify: `index.html`（約 1165–1189）

- [ ] **Step 1: 標題與副標加英文版**

`<h2 class="section-h2">一段持續進化的故事</h2>`（1165）改為：
```html
      <h2 class="section-h2 t-zh">一段持續進化的故事</h2>
      <h2 class="section-h2 t-en">A story of constant evolution</h2>
```

`<p class="section-sub">…</p>`（1166–1168）改為兩份，中文保留原文，英文：
```html
      <p class="section-sub t-en">
        From a Guanghua-Market DIY tinkerer with a tech-law background into one of Taiwan's most demanding industries — building product-engineering instinct in the world of hardware NPI, honing the craft of storytelling across countless conference calls, then reinventing myself for the age of AI automation. Every choice, a cross-disciplinary compounding I never gave up on.
      </p>
```
（原 `<p class="section-sub">` 加上 `t-zh`。）

- [ ] **Step 2: 四張 about-card 的 h3 與 p 加英文版**

每張卡的 `<h3>` 與 `<p>` 各複製為 t-zh / t-en 兩份（原元素加 `t-zh`，新增 `t-en`）。英文對應：

- 01 `豐富的 ODM 專案經驗` → `Deep ODM project experience`
  p `NB、Server、Display、Workstation 跨多產品線，主導超過 10 世代 NPI 全流程，從 RFQ 到 MP 無斷點交付。`
  → `Across NB, Server, Display and Workstation lines — led 10+ generations of full-cycle NPI, delivering seamlessly from RFQ to MP.`
- 02 `品牌廠工作模式理解` → `Brand-side operating fluency`
  p → `Working directly with the brand side at Dell Taiwan — fluent in brand procurement decisions, translating engineering requirements, and cross-timezone cadence.`
- 03 `AI 工具應用實作` → `Hands-on AI tooling`
  p → `n8n automation, Claude Code vibe coding and LLM prompt engineering — bringing AI tools genuinely into daily work.`
- 04 `問題解決能力` → `Problem solving`
  p → `300+ PCRs handled, cross-department conflict resolution, and a knack for making complex technical and business problems clear to everyone.`

範例（01 卡）：
```html
          <h3 class="t-zh">豐富的 ODM 專案經驗</h3>
          <h3 class="t-en">Deep ODM project experience</h3>
          <p class="t-zh">NB、Server、Display、Workstation 跨多產品線，主導超過 10 世代 NPI 全流程，從 RFQ 到 MP 無斷點交付。</p>
          <p class="t-en">Across NB, Server, Display and Workstation lines — led 10+ generations of full-cycle NPI, delivering seamlessly from RFQ to MP.</p>
```

- [ ] **Step 3: 瀏覽器實測**

切 EN：About 標題、副標、四卡標題與內文全部英文；切中恢復。`card-num`（01 · ODM 等）兩語不變。

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat(i18n): About 區塊雙語"
```

---

### Task 4: Experience 區塊雙語

**Files:**
- Modify: `index.html`（h2 1201；五個 `exp-desc` 1208/1224/1239/1254/1268）

- [ ] **Step 1: 標題加英文版**

`<h2 class="section-h2">職涯軌跡</h2>`（1201）→
```html
      <h2 class="section-h2 t-zh">職涯軌跡</h2>
      <h2 class="section-h2 t-en">Career path</h2>
```

- [ ] **Step 2: 五段 `exp-desc` 各加英文版**

每段原 `<p class="exp-desc">` 加 `t-zh`，並在其後新增 `<p class="exp-desc t-en">…</p>`。英文對應：

- Dell（1208）→ `End-to-end project management for Dell Server Platform HW/SW NPI, coordinating 100+ cross-functional engineering teams. Led ODM management, NRE budget audits and Statement-of-Work consolidation, and drove internal IT-tool development (SW spec + UI/UX).`
- LC 2018–2021（1224）→ `As Lenovo Technical PM and Development PM, managed 300+ PCRs per generation of scope changes, built end-to-end product-lifecycle solutions, and owned global offering-matrix management.`
- GSP 2015–2018（1239）→ `Took the Talkimate SPK mic from zero to one — launched on Kickstarter, 30K views on the brand video, 4/5-star Amazon reviews, executing the full go-to-market strategy.`
- LC 2012–2015（1254）→ `Engineering development management for ThinkPad commercial NB and Mobile Workstation lines — cross-functional problem solving and process-improvement proposals.`
- Elite/Qisda 2010–2012（1268）→ `Executed engineering-development projects for Display Monitors and X86 Pad/Netbook — building the early-career foundation in hardware product development.`

範例（Dell）：
```html
          <p class="exp-desc t-zh">負責 Dell Server Platform HW/SW NPI 全程專案管理，協調逾 100 個跨部門工程團隊。主導 ODM 管理、NRE 預算審計、Statement of Work 整合，並推動內部 IT 工具開發（SW Spec + UI/UX 優化）。</p>
          <p class="exp-desc t-en">End-to-end project management for Dell Server Platform HW/SW NPI, coordinating 100+ cross-functional engineering teams. Led ODM management, NRE budget audits and Statement-of-Work consolidation, and drove internal IT-tool development (SW spec + UI/UX).</p>
```

- [ ] **Step 3: 瀏覽器實測**

切 EN：標題與五段描述英文；`exp-period`、職稱 `<h3>`、`exp-co`、tag 兩語不變。

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat(i18n): Experience 區塊雙語"
```

---

### Task 5: Skills 標題 + Projects + Contact 雙語

**Files:**
- Modify: `index.html`（Skills h2 1286 與 SVG aria-label 1288；Projects h2 1411 與各卡 1415/1416/1427/1438/1448/1449；Contact 1462）

- [ ] **Step 1: Skills 標題與 aria-label**

`<h2 class="section-h2">能力地圖</h2>`（1286）→
```html
      <h2 class="section-h2 t-zh">能力地圖</h2>
      <h2 class="section-h2 t-en">Capability map</h2>
```
SVG（1288）`aria-label="能力星座圖：Technical PM、Product、AI & Domain 三個核心技能群"` 改為英文：
`aria-label="Capability constellation: Technical PM, Product, AI & Domain"`。
（SVG 內節點文字已是英文，無需處理。）

- [ ] **Step 2: Projects 標題與四卡文字**

`<h2 class="section-h2">親手建造的東西</h2>`（1411）→
```html
      <h2 class="section-h2 t-zh">親手建造的東西</h2>
      <h2 class="section-h2 t-en">Things I've built</h2>
```

各卡 `<h3>`／`<p>`（僅含中文者）加 t-zh 並新增 t-en：

- Talkimate h3 `Talkimate — Kickstarter 群眾募資產品` → `Talkimate — Kickstarter crowdfunded product`
  p → `Planned an SPK mic hardware product from scratch — crowdfunding, brand building and Amazon channel management, with 30K views on the brand video.`
- Dell IT Tool p（h3 已英文，只翻 p）→ `Led internal-tool SW-spec consolidation and user-story writing, coordinated the dev team, and drove UI/UX enhancements to improve engineering efficiency.`
- Edge/Healthcare/GPU p（h3 已英文，只翻 p）→ `Led pioneer feature development at Dell across Healthcare solutions, GPU-card integration and the Edge Solution Platform — establishing a cross-department critical-fix scheduling mechanism.`
- Maxcareerportal h3 `Maxcareerportal — 本網站` → `Maxcareerportal — this site`
  p → `A personal career portal built with Open Design, the Linear design language and vibe coding — from DESIGN.md to deployment, entirely self-driven.`

範例（Talkimate 卡）：
```html
          <h3 class="t-zh">Talkimate — Kickstarter 群眾募資產品</h3>
          <h3 class="t-en">Talkimate — Kickstarter crowdfunded product</h3>
          <p class="t-zh">從零規劃 SPK Mic 硬體產品，完成群眾募資、品牌建立與 Amazon 銷售通路管理，YT 品牌影片 3 萬觀看。</p>
          <p class="t-en">Planned an SPK mic hardware product from scratch — crowdfunding, brand building and Amazon channel management, with 30K views on the brand video.</p>
```

- [ ] **Step 3: Contact 副標**

`<p class="contact-sub">歡迎聊聊合作機會、技術交流，或純粹打聲招呼</p>`（1462）→
```html
    <p class="contact-sub t-zh">歡迎聊聊合作機會、技術交流，或純粹打聲招呼</p>
    <p class="contact-sub t-en">Happy to chat about collaboration, tech, or just to say hi.</p>
```

- [ ] **Step 4: 瀏覽器實測**

切 EN：Skills/Projects/Contact 標題與內文英文；能力地圖節點與圖例兩語不變；Email/GitHub/LinkedIn 按鈕不變。

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat(i18n): Skills/Projects/Contact 雙語"
```

---

### Task 6: 全站雙語 QA + 收尾

**Files:**
- Verify only（必要時 Modify `index.html` 修 bug）

- [ ] **Step 1: 殘留中文掃描**

```bash
cd /Users/mmfamily/Maxcareerportal
python3 -c "
import re
for i,l in enumerate(open('index.html',encoding='utf-8'),1):
    s=l.strip()
    if re.search(r'[一-鿿]',s) and '<!--' not in s and 't-zh' not in s and '/*' not in s and '簡報' not in s:
        print(i, s[:90])
"
```
預期：輸出只剩「經驗分享」相關（已隱藏、不翻）與 CSS 註解、簡報區塊內文（不翻）。若有其他可見內容中文未包 `t-zh`，補上對應 `t-en`。

- [ ] **Step 2: 兩語言完整走查（瀏覽器）**

`http://localhost:8777/`，分別在 zh / en：
- 逐區捲動：Hero、About、Experience、Skills、Projects、Contact、Footer 文字語言正確、無中英並存殘影。
- 動畫正常：時間軸打燈、能力地圖脈衝環。
- 切換即時生效；重整維持選擇。
- `<html lang>` 隨語言為 `zh-TW` / `en`。
- nav 無「經驗分享」按鈕；語言鈕文字對應（zh 顯示 EN、en 顯示 中）。

- [ ] **Step 3: 模擬英文瀏覽器首次進站**

DevTools Console：`localStorage.removeItem('site-lang'); location.reload();`（瀏覽器語言為 en 時應顯示英文；為中文時顯示中文）。若無法改瀏覽器語言，改用 `localStorage.setItem('site-lang','en')` 驗證英文全站。

- [ ] **Step 4: 最終 Commit（若 Step 1/2 有修正）**

```bash
git add index.html
git commit -m "fix(i18n): 補漏並通過雙語 QA"
```

---

## 完成後

雙語功能完成且本機驗證通過後，回到既有部署待辦（見 memory `project-maxcareerportal`）：`git push` → build/push amd64 image 到 ghcr.io → 重啟 Zeabur。此步驟不在本計畫內，實作完成後另行執行。
