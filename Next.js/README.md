## 專案結構

### 1. App Router
```bash
/app
├── layout.js  (應用程式的根佈局)
├── page.js  (首頁)
├── /dashboard
│   ├── page.js
│   ├── layout.js  (Dashboard 的專屬佈局)
├── /api
│   ├── hello/route.js  (API 路由)
├── next.config.js
├── package.json
```
區分 `Server Components 伺服器組件`、`Client Components 客戶端組件`
- 如果要使用 Hook（如 `useState`、`useEffect`），需要標註 "use client"，讓組件變成 Client Component（客戶端組件）

獲取資料方式
- 無 `getStaticProps`、`getServerSideProps`、`getStaticPaths`
- 但可以透過 `RSC`、`fetch`、`Server Actions` 來達成類似效果

### 2. Pages Router
```bash
/app
├── index.js  (首頁)
├── about.js
├── contact.js
├── /api
│   ├── hello.js  (API 路由)
├── next.config.js
├── package.json
```
獲取資料方式
- `getStaticProps (SSG)`
- `getServerSideProps (SSR)`
- `getServerSideProps (SSR)`
- `getStaticPaths (ISR)`

## 渲染模式

| 模式 | 函式 | 機制 | 應用 | SEO | 速度 |
| :- | :- | :- | :- | :- | :- |
| `Server-Side Rendering (SSR)【伺服器端渲染】` | `getServerSideProps` | 每次請求會在 Server 動態產生 html 並返回 Client | 即時資料更新 | 好 | 慢 |
| `Static Site Generation (SSG)【靜態網站生成】` | `getStaticProps` | 編譯時預先生成 HTML，並將靜態文件提供給用戶 | 不常變動的內容 / 最快的加載速度 | 很好 | 超快 |
| `Incremental Static Regeneration (ISR)【增量靜態生成】` | `getStaticProps` & `revalidate` | 類似 SSG，但可以 定期重新生成靜態頁面，不需要重新部署 | 需要部分動態更新的靜態頁面 | 很好 | 快 |
| `Client-Side Rendering (CSR)【客戶端渲染】` | `useEffect` | 先載入 空白頁面，再由瀏覽器執行 API 請求，並動態渲染內容 | 使用者個人化內容 | 差 | 快 |
| `Streaming (React Server Components) (RSC)` | `App Router (app/ 目錄) + async Server Components` | 使用 React 服務端組件 (RSC)，允許在伺服器端 分批傳輸 內容 | 減少首屏載入時間（可以優先傳遞部分內容） / 適合大型數據頁面 | 好 | 超快 |

### App Router 下的各種渲染模式
| 模式 | App Router | Pages Router |
| :- | :- | :- |
| `Static Site Generation (SSG)` | 直接在 Server Component 裡 fetch | `getStaticProps` |
| `Server-Side Rendering (SSR)` | 直接在 Server Component 裡 fetch | `getServerSideProps` |
| `Incremental Static Regeneration (ISR)` | `fetch` + `next: { revalidate: 秒數 }` | `revalidate: 秒數` |
| `Client-Side Rendering (CSR)` | Client Component + `useEffect` | `useEffect` + API |
| `API Routes` | app/api/ (route.js) | pages/api/ (index.js) |