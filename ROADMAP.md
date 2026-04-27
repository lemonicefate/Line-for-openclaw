# Line-for-openclaw Roadmap

**Status**: 🟢 Active
**Last updated**: 2026-04-27
**Current milestone**: PRD v1.0 核心功能完成 → 即時推送 + 手動回覆
**Branch**: `claude/develop-prd-feature-DPGTY`

> LINE Messaging API 智能客服後台（Express + 多 LLM Factory + RAG）
> Fork 自 enzotseng-ops 上游，由無毒農 / OpenClaw 客製化擴充

---

## 🚧 In progress

- [ ] **手動回覆功能（P1）** — 人工客服模式下，管理員在後台主動傳訊給 LINE 用戶
- [ ] **WebSocket 即時推送（P2）** — 訊息列表自動更新，不需手動 F5

## 📅 Up next（本月）

- [ ] WebSocket 即時推送（Socket.IO 或原生 ws）
- [ ] 手動回覆 UI（Messages 頁面新增傳訊輸入框）
- [ ] 多管理員角色 / 權限系統（P3，admin / operator / viewer）
- [ ] Setup 精靈完成後的引導頁（指引初次使用者熟悉後台）
- [ ] 知識庫檔案管理 UX 優化（上傳進度、刪除確認）
- [ ] 系統設定 UI 補強（速率限制設定可視化）

## 🗂️ Backlog（someday/maybe）

- 與 upstream `enzotseng-ops` 同步策略（定期 rebase / cherry-pick 或永久分叉）
- 訊息查詢效能優化（索引、分頁、全文搜尋）
- 完整日誌系統（Winston → 持久化儲存或外部 log service）
- 自動化測試覆蓋（目前無 unit / integration test）
- CI/CD pipeline（GitHub Actions：lint + test + Zeabur auto deploy）
- 多 LINE Bot 帳號支援（單機部署多個 Channel）
- Webhook 重送機制（LINE 平台暫時無法到達時）
- 訊息範本 / 快速回覆庫（管理員常用回覆）
- 用戶標籤 / 分類系統（CRM 化）
- Dashboard 統計報表強化（轉換率、回覆時間分析）
- RAG 多檔案來源（除 PDF 外支援 Markdown / Notion）
- LINE Flex Message 編輯器（圖文選單、輪播）
- 備份 / 還原機制（DB dump、加密金鑰備份）
- 替換記憶體型 rate limit 為 Redis（多實例部署）
- i18n 多語系後台（目前僅繁中）

## ✅ Recently done（近一個月）

- [x] Zeabur 雲端部署支援（原生 Node.js，移除 Docker）
- [x] 零配置啟動精靈（JWT_SECRET / ENCRYPTION_KEY 自動產生）
- [x] Web UI 設定 DATABASE_URL（`POST /api/setup/database`）
- [x] MCP Server 管理（CRUD + 連線測試 + 工具發現）
- [x] MCP 認證支援（Bearer Token / X-Api-Key）
- [x] MCP 工具整合 LLM（Claude / OpenAI / Gemini 格式自動轉換）
- [x] 唯讀檔案系統相容（容器環境跳過 `.env` 寫入）
- [x] 啟動時自動執行 Knex migration
- [x] Setup 模式下跳過 rate limit + `trust proxy` 修正
- [x] 首次登入強制密碼變更
- [x] 登入 DDoS 防護（express-rate-limit）
- [x] CORS 開放 + 靜態檔案優先 serve（修 Zeabur 502 / asset 被擋）
- [x] PostgreSQL SSL 由連線字串控制（解決 Zeabur 不支援 SSL）

## ⚠️ Known concerns

- **WebSocket 未實作** — 訊息列表需手動重整，影響即時客服體驗
- **多管理員權限缺乏** — 目前所有登入者皆為 super admin，無細分角色
- **無 CI/CD** — 無自動化 lint / test / deploy，純手動推送至 Zeabur
- **無自動化測試** — 重構或升級時缺乏回歸保障
- **Rate limit 為記憶體儲存** — 多實例部署時計數器不共享（單機部署 OK）
- **與 upstream 分叉風險** — 大量客製化後與 enzotseng-ops 主線難以同步
- **ENCRYPTION_KEY 遺失即解不開舊資料** — 已有優雅降級，但仍需備份策略
- **MCP 工具發現快取 5 分鐘** — 上游 MCP server 異動後可能延遲生效
