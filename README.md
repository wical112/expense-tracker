# 💸 極簡記支出 — 免費 dogfood（主公自用）

極簡、盡可能少輸入、logic 補強嘅每日支出記帳 PWA。
核心循環：**開 app → 一個輸入框 → 打「lunch 65」→ 入帳 → 收工**。

> **狀態：v1 免費 dogfood** — 業務邏輯已實作：
> 自然語言 mini-parse（金額+關鍵字）· rule-based 自動分類（8 類，撳分類可改、會學）· recurring 偵測（同筆 ≥3 次提示）· 月預算 + 超支/異常大額即時提醒。
> 資料純 localStorage、無帳號、無後端、無收款。
> **定位**：曾為微應用工廠注#1，因紅海+無付費 wedge 經 Philips/Jordan gate 判 KILLED 作付費注；主公 explicit 復活作個人自用工具（非付費注、不入 9 站閘）。

## Stack

- 純 client-side **單檔 PWA**，**無 build、無後端**
- `index.html`（畫面 + 樣式 + 一段 minimal JS）
- `manifest.webmanifest`（可裝主畫面）
- `sw.js`（app-shell precache，第二次起離線可開）
- `icon.svg`（PWA / apple-touch-icon）
- 沿用 wical112 GitHub Pages 慣例（同台灣卡店地圖 / 福岡旅遊手帳同一套 arch）
- 資料層日後用 **localStorage**（Firebase 為將來可選 take-away/sync，scaffold 階段未落 — 未用先抽象係過早設計）
- 分類規則將來行 **rule-based**（純 client，慳成本，唔用 LLM）

## 點本地跑

PWA 需要透過 HTTP server 行（service worker 唔可以 `file://`）。喺 repo 根目錄揀一個：

```bash
# Python 3（最常見）
python3 -m http.server 8000

# 或 Node（有裝 npx）
npx --yes serve -l 8000 .
```

然後開瀏覽器去 **http://localhost:8000/**。

驗證 PWA：

- 開 DevTools → Application → Manifest：應見「極簡記支出」+ icon，無 error
- Application → Service Workers：應見 `sw.js` activated
- 第二次載入後關網／offline：頁面仍開得到（app shell 已 cache）
- 手機 Safari／Chrome：分享 → 加到主畫面 → 以 standalone 全螢幕開

## 維護

- 純 client、無 build、無後端
- **改 code 後一定要 bump `sw.js` 嘅 `VERSION`**（offline-first，唔 bump 用戶 cache 唔更新）
- 部署：暫未部署（站4 上線先處理；push / deploy 要先問主公）

## Update log

- **2026-05-18 v1.1**（UU spec，主公揀方向A）：常用 chips（近30筆高頻token預填）+ live parse preview（submit前見「→$X·類✎」可改）+ inline 編輯一筆（撳 row 改金額/註/類/刪）+ 本月分析（分類橫bar+%+近3月trend，可收起）。新純函式 topTokens/catBreakdown/lastNMonths，11/11 隔離測試綠（含 regression）。SW bump `v3-2026-05-18`。
- **2026-05-18 v1 dogfood**：實作 parseEntry / categorize(8類, learnable) / detectRecurring(≥3) / isAnomaly(>2.5×中位數) + 月預算 banner + 帳目列表(改類/刪/清空) + recurring 建議卡。19/19 純邏輯隔離單元測試綠。SW bump `v2-2026-05-18`。**未部署、非 git repo**（要版本控制/部署再問主公 init）。
- 2026-05-18 v0：站0 scaffold（空殼）。
