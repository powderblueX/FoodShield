# FoodShield Frontend

FoodShield 是一个食品安全信息与溯源管理系统的 Vue 3 前端。项目包含普通用户和管理员界面，覆盖食品信息、食品溯源、食品报告、投诉、文章与食品安全知识管理等功能。

> 本仓库仅包含前端。登录、数据查询和管理功能需要配套后端 API。

## 主要功能

- 用户注册、登录、密码重置和个人资料管理
- 食品信息查询与食品溯源
- 食品安全报告上传
- 投诉提交、查询与后台受理
- 食品安全文章和知识内容展示
- 管理员食品、文章、知识、投诉及日志管理
- 基于 Token 的登录状态和角色路由控制

## 技术栈

- Vue 3
- Vue Router 4
- Element Plus
- Axios
- Vite 6

## 环境要求

- Node.js 18 或更高版本
- npm 9 或更高版本
- 可访问的 FoodShield 后端服务

## 安装

```powershell
npm ci
```

复制本地环境配置：

```powershell
Copy-Item .env.example .env
```

根据后端地址修改 `.env`：

```dotenv
VITE_API_BASE_URL=http://localhost:8080
```

Vite 会把所有 `VITE_` 开头的变量打包进前端代码，因此不要在其中保存密码、API Key 或其他秘密信息。

## 本地开发

```powershell
npm run dev
```

终端会显示本地访问地址，通常为 `http://localhost:5173`。

## 构建与预览

```powershell
npm run build
npm run preview
```

生产构建输出到 `dist/`。`dist/` 和 `dist.zip` 都是可重新生成的构建产物，已加入 `.gitignore`，不应提交到源码仓库。

## 项目结构

```text
.
├── public/             # 不经 Vite 处理的静态文件
├── src/
│   ├── assets/         # 图片等前端资源
│   ├── net/            # Axios 请求与 Token 管理
│   ├── router/         # 页面路由和权限控制
│   ├── validate/       # 表单校验
│   ├── views/          # 用户端与管理端页面
│   ├── App.vue
│   └── main.js
├── .env.example        # 后端地址示例
├── index.html
├── package.json
└── vite.config.js
```

## 发布注意事项

- 部署前通过 `VITE_API_BASE_URL` 设置生产后端地址。
- 后端应正确配置 CORS，并只允许可信前端来源。
- 前端 Token 不能替代后端权限校验，所有管理接口都必须由后端验证身份和角色。
- 使用 Vue Router history 模式时，Web 服务器需要把未知路径回退到 `index.html`。

