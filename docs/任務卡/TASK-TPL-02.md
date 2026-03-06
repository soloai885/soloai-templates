# 任務卡：TASK-TPL-02 版型A（美學/美體）完整建置

## 來源
- 任務指令：TASK-TEMPLATE-BUILD-三套版型自建.md
- 對應 PHASE/STEP：Phase 2

## 前置條件
- ✅ TASK-TPL-01（Phase 1）已驗收通過
- ✅ template-a-beauty 基礎架構已就緒

## 目標
將版型A（美學/美體）從骨架建置為完整可瀏覽的商家官網，包含所有 Section 元件、快速需求選單特色模組，並通過 RWD 驗證。

## 執行步驟

### STEP 1：建立 Navbar 元件
檔案：`src/components/Navbar.astro`
- Logo + 店名（從 site.ts 讀取）
- 電話 CTA 按鈕（Mobile 點擊直接撥號 `tel:`）
- LINE 加入按鈕（連結到 `lineUrl`）
- Mobile 漢堡選單（RWD）
- 視覺：珊瑚粉主色調，字體 Noto Serif TC（店名）

### STEP 2：建立 Hero 元件
檔案：`src/components/Hero.astro`
- 大圖背景（使用 `/placeholder/hero.jpg`）
- `bg-cover bg-center` + 深色 overlay 確保文字可讀
- 標語文字（從 site.ts 讀取 tagline）
- 預約按鈕（平滑滾動到 `#location` 區塊）
- 文字居中，字體 Noto Serif TC

### STEP 3：建立快速需求選單元件（特色模組）
檔案：`src/components/QuickMenu.astro`
- 標題：「今天想改善什麼？」
- 選項卡（可橫向滾動）：舒壓按摩 / 美背護理 / 臉部保養 / 纖體療程
- 從 site.ts services 讀取
- 點擊後平滑滾動到 `#services` 對應服務
- Mobile：橫向可捲動，不換行

### STEP 4：建立熱門服務卡元件
檔案：`src/components/Services.astro`
- HTML anchor：`id="services"`
- 3-4 張服務卡片（從 site.ts services 讀取）
- 每張卡片：圖片（`/placeholder/card.jpg`）+ 名稱 + 價格 + 時間 + icon
- 圖片：`aspect-ratio: 4/3`，`object-cover`，`loading="lazy"`
- 卡片：圓角、shadow
- Desktop：3-4 欄並排
- Mobile：1 欄

### STEP 5：建立信任模組元件
檔案：`src/components/TrustSection.astro`
- 3 個信任點（從 site.ts trustPoints 讀取）：icon + label
- 客評引言區塊（可以寫死 2-3 條示範評論）
- 視覺：淺色背景區塊，與主內容區分

### STEP 6：建立位置資訊元件
檔案：`src/components/Location.astro`
- HTML anchor：`id="location"`
- 地址（從 site.ts 讀取）
- 營業時間（從 site.ts 讀取）
- Google Map iframe（使用 googleMapsUrl）
- 電話直撥按鈕 + LINE 按鈕

### STEP 7：建立 Footer 元件
檔案：`src/components/Footer.astro`
- LINE 加入按鈕
- 電話直撥
- 版權聲明（© 2026 {shopName}）
- 簡潔設計

### STEP 8：整合至首頁
檔案：`src/pages/index.astro`
- 引入所有元件，按以下順序排列：
  1. Navbar
  2. Hero
  3. QuickMenu（快速需求選單）
  4. Services（熱門服務卡）
  5. TrustSection（信任模組）
  6. Location（位置資訊）
  7. Footer

### STEP 9：RWD 調整與測試
- Desktop（≥1024px）：確認多欄佈局正確
- Tablet（768~1023px）：確認過渡正常
- Mobile（<768px）：確認單欄、無橫向溢出、漢堡選單正常
- 確認 `npm run build` 無 error

## 驗收標準
- [ ] 7 個 Section 元件全部建立（Navbar / Hero / QuickMenu / Services / TrustSection / Location / Footer）
- [ ] 所有資料從 site.ts 讀取，不 hardcode
- [ ] 快速需求選單可橫向滾動，點擊後平滑跳轉到服務區
- [ ] 服務卡片 Desktop 多欄、Mobile 單欄
- [ ] Hero 背景圖有 overlay，文字清晰可讀
- [ ] 電話直撥按鈕（tel:）存在且可用
- [ ] LINE 按鈕存在且連結正確
- [ ] 預約按鈕平滑滾動到位置區塊
- [ ] Mobile（375px）無橫向溢出
- [ ] 佔位圖正確顯示，無破圖
- [ ] `npm run build` 無 error
- [ ] 整體色系為玫瑰粉/珊瑚粉，符合版型A 規格

## 注意事項
1. **不動 Phase 1 建立的架構檔案**（site.ts、BaseLayout、tailwind.config 維持原樣）
2. **純 Tailwind utility**，不引入 UI component library
3. **圖片用佔位圖**，交付時才替換
4. **平滑滾動**用 CSS `scroll-behavior: smooth` 或簡單 JS
5. **所有 CTA 連結**：電話用 `tel:`、LINE 用 `https://line.me/R/ti/p/`、外部連結 `target="_blank" rel="noopener"`

---

*任務卡由小K產出，派給小碼執行。*
*完成後由小K驗收（含瀏覽器視覺測試），驗收通過後再拆 TASK-TPL-03（Phase 3：版型B）。*
