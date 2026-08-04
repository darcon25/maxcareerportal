# 中英文切換設計（i18n zh / en）

日期：2026-08-04
狀態：待實作

## 目標
MaxCareerPortal 單檔靜態站（`index.html`）加入中／英雙語：
1. 中英文內容隔離，可切換顯示
2. 首次進站依瀏覽器語言自動選語言
3. 右上角手動切換按鈕，選擇記憶於瀏覽器

英文內容來源：`Position_Product management ChienTsungLiu (Max) July 2026.docx`（July 2026 履歷）。

## 做法：A 案 — 雙區塊 CSS 顯示切換

### 隔離結構
- 每段可翻譯文字提供中、英兩份，並各自標記語言 class：
  - 中文：`<... class="lang-zh">…</...>`
  - 英文：`<... class="lang-en">…</...>`
- `<body>` 掛目前語言 class：`lang-zh` 或 `lang-en`。
- CSS 規則：
  ```css
  body.lang-zh .lang-en { display: none; }
  body.lang-en .lang-zh { display: none; }
  ```
- 行內元素用 `<span class="lang-zh">`／`<span class="lang-en">`；區塊元素用對應標籤加 class。含連結／粗體的段落，整段複製兩份，各自帶完整內嵌 markup。

### 自動偵測（首次進站）
- 讀 `localStorage.getItem('site-lang')`：有值 → 直接用（優先）。
- 無值 → 讀 `navigator.language`：以 `en` 開頭 → `en`，否則 → `zh`。
- 套用：設定 `document.body.className`（含 `lang-xx`）與 `document.documentElement.lang`（`zh-TW` / `en`）。
- 為避免載入閃爍：偵測 script 放 `<head>`，在 body 一渲染即定 class（或 body 預設 `lang-zh`，script 立即覆寫）。

### 手動切換
- nav 右上角加一顆按鈕，顯示「中 / EN」，點擊在 zh／en 間切換。
- 切換時：更新 `body` class、`<html lang>`、`localStorage.setItem('site-lang', …)`。
- 按鈕本身文字也隨語言顯示（中文版顯示「EN」、英文版顯示「中」，代表「點我切到另一種」）。

## 英文文案對應（專業簡潔版，源自履歷）

| 區塊 | 英文內容來源 |
|---|---|
| Hero 姓名／標語 | Chien-Tsung Liu (Max)／Product Manager · Project Manager |
| 職涯故事 4 點 | ODM project experience／Brand-side collaboration model／Applied AI tooling／Problem solving |
| 職涯軌跡 | Dell（Advisory PM, 2021–2026）、LC Futurecenter（Advisory PM／Staff PM）、GSP Tech（Product Manager, Talkimate）、Elite Computer／Qisda（Project Specialist），各帶履歷職責 bullet |
| 能力地圖 SVG 文字 | 英文化群組與節點標籤 |
| 專案卡片 | Talkimate (Kickstarter)／Dell Internal IT Tool／Edge・Healthcare・GPU Platform／Maxcareerportal |
| nav／聯絡／頁尾 | 對應英文 |

英文採履歷式簡潔專業語氣（bullet、精煉），非長篇敘事。**精簡但關鍵點不可漏**：中文版有提到的重點（職責、成果數據如 300 PCR/gen、Amazon 4/5 星、30 萬觀看、跨 30+ POC 協調等）英文版都要涵蓋，只是用更精煉的方式表達。先由 Claude 全部草擬，使用者潤飾。

## 範圍與非目標
- 只動 `index.html`（單檔）與其內嵌 CSS／JS。不引入框架或建置流程。
- 不做第三語言、不做 URL 路由（`/en`）、不做 SEO hreflang（未來可加）。
- 不改既有配色改版（未提交的 index.html 變更）之視覺，只在其上疊加雙語。

## 驗收
- 英文系統瀏覽器首次開站顯示英文；中文系統顯示中文。
- 手動切換即時生效，重新整理後維持上次選擇。
- 兩種語言下版面、動畫、能力地圖 SVG、簡報 overlay 皆正常。
- 未選語言的那份內容完全不顯示（無殘影、無佔位）。
