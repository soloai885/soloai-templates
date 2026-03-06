# 任務卡：TASK-TPL-01 Repo 初始化 + 共用架構建立

## 來源
- 任務指令：TASK-TEMPLATE-BUILD-三套版型自建.md
- 對應 PHASE/STEP：Phase 1

## 目標
建立三套商家版型的 Astro 專案架構，確保每套版型都能獨立 `npm run dev` 啟動，為後續 Phase 2-4 的版型實作打好基礎。

## 前置條件
- ✅ GitHub Repo `soloai885/soloai-templates` 已建立
- ✅ 初始 commit 已 push 至 main

## 執行步驟

### STEP 1：建立三個版型子資料夾
在 `soloai-templates/` 根目錄下建立：
- `template-a-beauty/`（美學/美體）
- `template-b-nail/`（美甲）
- `template-c-hair/`（美髮）

### STEP 2：各子資料夾初始化 Astro + Tailwind
每個資料夾內執行：
1. 初始化 Astro 4.x 專案
2. 安裝 Tailwind CSS 整合
3. 確認 `package.json` 正確
4. 確認 `astro.config.mjs` 正確
5. 確認 `tailwind.config.cjs` 正確

### STEP 3：建立共用資料結構 `site.ts`
每個版型在 `src/data/site.ts` 建立資料結構：
```typescript
export const siteData = {
  shopName: "店家名稱",
  tagline: "一句話描述",
  phone: "0912-345-678",
  address: "高雄市OO區OO路X號",
  lineId: "@xxxxxxxx",
  googleMapsUrl: "https://maps.google.com/...",
  businessHours: "週一至週日 10:00–20:00",
  services: [
    { name: "服務名稱", price: "NT$XXX起", duration: "60分鐘", icon: "✨" },
  ],
  gallery: [
    { src: "/images/work-01.jpg", alt: "作品說明" },
  ],
  trustPoints: [
    { icon: "⭐", label: "Google 評分 4.9" },
    { icon: "👥", label: "服務超過 500 位顧客" },
  ],
}
```

### STEP 4：建立 BaseLayout.astro
每個版型在 `src/layouts/BaseLayout.astro` 建立基礎佈局：
- `<head>` 包含 meta、SEO tags（從 site.ts 讀取）
- OG tags（og:title, og:description, og:image）
- Google Fonts 引入（用 `<link>` 不用 `@import`）
  - 版型A：Noto Serif TC + Noto Sans TC
  - 版型B：Playfair Display + Noto Sans TC
  - 版型C：Cormorant Garamond + Noto Sans TC

### STEP 5：Tailwind 主色設定
各版型 `tailwind.config.cjs` 使用 CSS variables 定義主色（不要 hardcode）：

**版型A（美學/美體）：**
- primary: `#E8A598`（珊瑚粉）
- secondary: `#F5E6D8`（奶油白）
- text: `#3D2B1F`（深棕）

**版型B（美甲）：**
- primary: `#9B59B6`（深紫）
- accent: `#D98EF0`（霓虹紫）
- background: `#1A1A2E`（黑冷灰）
- text: `#F0F0F0`（近白）

**版型C（美髮）：**
- primary: `#2D3A2E`（深墨綠）
- secondary: `#1C1C1C`（炭黑）
- accent: `#C9A96E`（香檳金）
- background: `#F5F0E8`（米白）

### STEP 6：建立佔位圖
每個版型 `public/placeholder/` 放入佔位圖：
- `hero.jpg`：1440×900px（灰色系）
- `card.jpg`：800×600px（灰色系）
- `avatar.jpg`：400×400px（灰色系）

### STEP 7：建立首頁骨架
每個版型 `src/pages/index.astro`：
- 引入 BaseLayout
- 顯示一個簡單的 `<h1>` 標題（如「版型A - 美學/美體」）
- 確認頁面可正常載入

### STEP 8：本機測試
每個版型分別執行：
```bash
npm run dev    # 確認 dev server 啟動無 error
npm run build  # 確認 build 成功
```

### STEP 9：Push 至 GitHub
```bash
git add .
git commit -m "feat: Phase 1 - 三套版型架構初始化"
git push origin main
```

## 驗收標準
- [ ] 三個子資料夾結構正確（template-a-beauty / template-b-nail / template-c-hair）
- [ ] 每套版型有獨立的 `package.json`、`astro.config.mjs`、`tailwind.config.cjs`
- [ ] 每套版型有 `src/data/site.ts`，格式一致
- [ ] 每套版型有 `src/layouts/BaseLayout.astro`，含正確字體引入
- [ ] Tailwind 主色使用 CSS variables，非 hardcode
- [ ] 佔位圖存在於 `public/placeholder/`（三種尺寸）
- [ ] 三套版型 `npm run dev` 啟動正常，頁面可載入
- [ ] 三套版型 `npm run build` 無 error
- [ ] 程式碼已 push 至 GitHub `main` branch

## 注意事項（小C 特別提醒）
1. **Phase 1 是關鍵** — 架構不對後面三套都要重做，務必仔細驗收
2. **Tailwind 主色用 CSS variables**（`--color-primary`），在 `tailwind.config.cjs` 中定義
3. **字體用 `<link>` 引入** Google Fonts，不用 `@import`（速度更快）
4. **不引入 UI component library**（如 DaisyUI、Flowbite），純 Tailwind utility
5. **三套版型共用一個 Repo，分資料夾**，不是三個 Repo

---

*任務卡由小K產出，派給小碼執行。*
*完成後由小K驗收，驗收通過後再拆 TASK-TPL-02（Phase 2：版型A）。*
