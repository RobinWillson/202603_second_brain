# NextJS Second Brain Web App: 逐步建置計畫

## 步驟 1: 環境設定與初始化
1. **建立 NextJS 專案**: 使用 App Router、TypeScript 與 Tailwind CSS 初始化專案 (`npx create-next-app@latest .`)。
2. **安裝核心套件**: 
   - Markdown 處理: `react-markdown`, `remark-gfm`, `rehype-highlight`
   - UI 與動畫: `lucide-react`, `framer-motion`
   - 資料庫/搜尋 (選用): `better-sqlite3`, `sqlite-vec`
3. **設定環境變數**: 設定 `.env.local` 以配置系統路徑 (`NOTES_PATH`, `TRASH_PATH`) 與 AI 金鑰 (`OPENAI_API_KEY`)。

## 步驟 2: 後端開發 (Next.js API 路由)
1. **檔案系統操作**: 
   - `GET /api/tree`: 將本地資料夾轉換成樹狀 JSON 結構（排除隱藏資料夾）。
   - `GET / PUT / DELETE /api/file`: 提供讀取、編輯（包含時間戳衝突偵測）及將檔案移至 `.trash` 中。
2. **搜尋與收集 (Capture)**: 
   - `POST /api/search`: 提供全文搜尋功能。
   - `POST /api/capture`: 接收即時文字內容並在 Inbox 自動建立新檔案。
3. **AI 與整合**: 
   - `POST /api/copilot/ask` & `semantic-search`: 將本地文字脈絡連接至 AI 語言模型進行提問或語意搜尋。

## 步驟 3: 前端開發 (React 元件)
1. **版面架構 Layout**: 建立支援響應式設計的深色主題版面，包含可收合的側邊欄 (Sidebar，顯示檔案樹) 以及主內容區。
2. **Markdown 閱讀器與編輯器**: 實作主內容區，使用 `react-markdown` 俐落地渲染 `.md` 檔案，並能無縫切換至純文字編輯模式。
3. **全域快速收集 (Quick Capture)**: 在畫面頂部新增一個全域輸入框，用來快速儲存文字、想法或解析網址。
4. **情境互動工具**: 
   - **浮動工具列**: 在反白選取文字時自動浮出，可將文字轉為待辦事項或點子卡片。
   - **搜尋對話框**: 支援 `Cmd/Ctrl + K` 快捷鍵喚出，快速跳轉檔案。
5. **洞察面板**: 建立「每日回顧」(Daily Review) 介面以及右側拉出的 AI Copilot 對話抽屜。

## 步驟 4: 測試與本地部署
1. **功能驗證**: 準備範例 `.md` 資料夾測試跨裝置版面、解析邏輯與 Markdown 格式渲染。
2. **編譯專案**: 執行 `npm run build`。
3. **本地背景運行**: 使用 PM2 (`pm2 start npm --name "second-brain" -- start`) 讓 NextJS 伺服器在背景持續運行，確保隨時可存取。
