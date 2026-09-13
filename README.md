# ProTask - 現代化 Vue 3 任務管理應用程式

這是一個專業、模組化且功能豐富的任務管理應用程式，使用 Vue 3 (Composition API) 構建。專案採用乾淨的 UI/UX 設計、強健的元件架構，以及流暢的客戶端狀態持久化機制。

## 核心功能 (Features)

- 元件驅動架構 (Component-Driven Architecture)：清晰的父子階層結構，將關注點分離至獨立的模組化元件（如 Navbar、TaskInput、TaskList）。
- 動態任務管理 (Dynamic Task Management)：
  - 即時新增任務。
  - 透過刪除線視覺回饋切換任務完成狀態。
  - 無縫刪除單一任務。
  - 透過「清除已完成」工具進行批次清理。
- 即時搜尋與多條件篩選 (Real-time Search & Multi-condition Filtering)：
  - 依狀態動態篩選任務：全部、未完成與已完成。
  - 即時關鍵字搜尋列，可隨時查詢特定任務。
- 資料持久化 (Data Persistence)：利用 Vue 的響應式 watch 與深度屬性監聽，自動與瀏覽器的 localStorage 進行狀態同步。
- 即時統計 (Live Statistics)：即時標頭計數器，追蹤總任務數與已完成項目。
- 響應式與現代化介面 (Responsive & Modern UI)：採用簡約的色彩配置、圓角容器、互動式懸停狀態以及平滑的 CSS 過渡效果。

## 技術棧 (Tech Stack)

- 前端框架：Vue 3 (Composition API (`<script setup>`), ref, computed, watch)
- 樣式設計：Scoped CSS、Flexbox 佈局、現代化 UI 設計系統變數
- 資料儲存：瀏覽器 localStorage API
- 建置工具：Vite

## 專案結構 (Project Structure)

src/
├── components/
│ ├── Navbar.vue # 模擬使用者登入狀態的導覽列元件
│ ├── TaskInput.vue # 用於新增任務的輸入表單元件
│ └── TaskList.vue # 動態渲染任務項目的清單元件
├── App.vue # 管理全域狀態與篩選邏輯的主容器
├── main.js # 應用程式進入點
└── style.css # 全域基礎樣式

## 快速開始 (Getting Started)

### 前置需求

請確認你的系統已安裝 Node.js。

### 安裝與本機執行

1. 複製儲存庫 (Clone the repository)：
   git clone https://github.com/your-username/pro-task.git
   cd pro-task

2. 安裝相依套件：
   npm install

3. 啟動開發伺服器：
   npm run dev

4. 於瀏覽器中開啟：
   前往終端機中所指定的網址（通常為 http://localhost:5173）。

## 核心架構亮點 (Key Architectural Highlights)

- 單向數據流 (One-Way Data Flow)：父元件 (App.vue) 擁有唯一的資料來源 (tasks)，並透過 props (:tasks) 將資料向下傳遞給子元件。
- 事件冒泡 (Event Bubbling / Emits)：子元件透過觸發 @toggle-task、@delete-task 與 @add-task 事件，將操作向上回報給父元件。
- 串接式計算過濾 (Chained Computed Filtering)：在單一個響應式計算屬性 (filteredTasks) 中，高效率地結合狀態篩選與搜尋關鍵字比對。
