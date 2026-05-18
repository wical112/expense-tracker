# 更新日誌 — 極簡記支出

## 2026-05-18 — 上 wicalyu.com 雜項 hub（money.wicalyu.com）

- 接入 `wicalyu.com` 個人雜項 hub，`CNAME` = `money.wicalyu.com`（已存在）。
- 加 `<meta name="robots" content="noindex">` + `<meta name="referrer" content="no-referrer">`（unlisted 定位，與 hub 其餘站一致 / Lucy 安全方案 T2-2）。
- sw.js `VERSION v3→v4`（index.html 改動，強制刷 PWA cache）。
- 定位澄清：本站係**自用 dogfood 工具**（離線、本機 localStorage、無帳號、無 LLM），非付費產品（付費角度已於微應用工廠站1 gate 判 KILLED — 紅海）。
- 待辦：Cloudflare 加 `CNAME money → wical112.github.io`（DNS only）→ GitHub 出證書 → Enforce HTTPS（背景 job 自動）。
