# capacitor-cloudflare-fullstack-pwa-app


## 项目简介

本项目是一个现代化 Progressive Web App (PWA) 全栈起步模板，前端基于 React + Vite + TypeScript，后端采用 Cloudflare Worker + Cloudflare D1（Serverless SQLite），前后端通过 tRPC 实现类型安全的 API 通信。适用于各种通用业务场景，支持快速二次开发和全栈拓展。

---

## 架构设计

- **前端**：React + Vite + TypeScript，采用模块化目录结构，支持 PWA 能力，使用 Redux 进行状态管理。
    - **离线存储**：集成 Dexie（基于 IndexedDB）实现本地数据的持久化与离线访问，支持离线缓存、数据同步等典型 PWA 场景。
- **服务层**：src/services 采用 tRPC 客户端模式，所有 API 调用类型自动推导，便于维护和扩展。
- **后端**：Cloudflare Worker（TypeScript），通过 tRPC 提供类型安全 API，数据存储采用 Cloudflare D1（Serverless SQLite）。
- **开发与构建**：统一使用 pnpm 管理依赖，支持多环境构建与测试。
- **自动化与质量保障**：集成 ESLint、Prettier、Vitest、Playwright，保障代码风格与功能正确性。

---

## 目录结构

```
a-voyager-pwa-app/
├── backend/                  # 后端服务（Cloudflare Worker + D1 + tRPC）
│   ├── src/
│   │   ├── routers/         # tRPC 路由
│   │   ├── db/              # D1 数据库操作封装
│   │   ├── utils/           # 工具函数
│   │   └── index.ts         # Worker 入口
│   ├── schema.sql           # D1 数据库结构定义
│   ├── wrangler.toml        # Cloudflare 配置
│   └── README.md
│
├── public/                   # 前端静态资源
├── src/                      # 前端源码
│   ├── assets/               # 资源文件
│   ├── components/           # React 组件
│   ├── pages/                # 页面
│   ├── services/             # tRPC 客户端封装
│   ├── store/                # 状态管理
│   ├── helpers/              # 通用辅助函数
│   ├── routes/               # 路由定义和页面组件
│   │   ├── pages/            # 页面组件
│   │   └── tabs/             # 标签页组件
│   ├── features/             # 业务功能模块
│   │   ├── auth/             # 认证登录相关
│   │   ├── post/             # 帖子功能
│   │   ├── user/             # 用户中心
│   │   ├── comment/          # 评论功能
│   │   ├── settings/         # 设置中心
│   │   ├── feed/             # 信息流
│   │   ├── moderation/       # 内容管理
│   │   ├── media/            # 多媒体
│   │   └── ...               # 其他领域模块
│   ├── App.tsx
│   └── main.tsx
│
├── scripts/                  # 构建、发布等脚本
├── manuall-docs/             # 项目文档（含架构与开发规范）
├── package.json              # 前端依赖
├── pnpm-lock.yaml
├── tsconfig.json
└── README.md                 # 项目总说明
```

---

## src/features 目录规划与建设

src/features 目录用于组织前端应用的所有“业务功能模块”。每个子目录代表一个独立的功能领域，实现高内聚、低耦合的模块化开发。推荐的建设与规划如下：

### 设计原则
- 按照“领域驱动”或“特性分区”组织代码，每个业务功能单独成模块，便于独立开发、测试和维护。
- 每个功能模块应包含：
  - 业务相关的 React 组件
  - 状态管理（如 Redux slice）
  - 服务/API 调用
  - 样式文件（如 .module.css）
  - 类型定义（如 types.ts）
  - 单元测试（如 .test.tsx）

### 典型结构示例
```
src/features/
├── auth/         # 认证登录相关
├── post/         # 帖子功能
├── user/         # 用户中心
├── comment/      # 评论功能
├── settings/     # 设置中心
├── feed/         # 信息流
├── moderation/   # 内容管理
├── media/        # 多媒体
├── ...           # 其他领域模块
```

### 建设建议
- 新增业务功能时，建议在 features 下新建对应目录，保持模块独立。
- 各模块内部可自由组织子目录（如 components、services、slice、types、tests 等），但建议保持风格统一。
- 公共组件、工具函数等可放在 src/shared 或 src/helpers，避免重复代码。
- 强调单元测试和类型定义，提升代码健壮性。

### 价值
- 便于多人协作和大型项目演进。
- 支持功能级别的解耦和复用。
- 让代码结构清晰、易于维护和扩展。

---

## 技术栈说明

本项目采用现代全栈 TypeScript 技术栈，主要依赖如下：

### 前端
- **React**：主流 UI 框架，采用函数组件 + Hooks。
- **Vite**：极速开发与构建工具。
- **Redux Toolkit**：状态管理。
- **tRPC**：类型安全的 API 通信。
- **Dexie**：基于 IndexedDB 的本地离线存储。
- **Ionic/Antd/Material UI**（如有）：UI 组件库。
- **TypeScript**：类型系统，前后端类型共享。
- **ESLint & Prettier**：代码风格和格式化。
- **Vitest**：单元测试。
- **Playwright**：端到端测试。
- **pwa-asset-generator**：PWA 资源生成。
- **@capacitor/core**：PWA 与原生桥接能力。

### 后端
- **Cloudflare Worker**：无服务器边缘计算。
- **tRPC**：API 路由与类型安全。
- **Cloudflare D1**：Serverless SQLite 数据库。
- **Wrangler**：Cloudflare Worker 本地开发与部署工具。

### 依赖库（摘自 package.json）
- `react`, `react-dom`：核心前端库
- `redux`, `@reduxjs/toolkit`, `react-redux`：状态管理
- `dexie`：IndexedDB 离线存储
- `@trpc/client`, `@trpc/server`：tRPC 客户端与服务端
- `@capacitor/core`, `@capacitor/keyboard`, `@capacitor/android`：PWA/移动端集成
- `vite`, `typescript`, `eslint`, `prettier`：开发、构建与质量工具
- `vitest`, `playwright`：测试工具
- `pwa-asset-generator`：PWA 资源自动化
- 其他库详见 package.json

### Capacitor 插件（详细）

本项目集成了如下 Capacitor 插件，赋能 PWA 以接近原生 App 的体验：

- **@capacitor/core**：Capacitor 核心库，API 桥接。
- **@capacitor/android**、**@capacitor/ios**：原生平台支持。
- **@capacitor/keyboard**：软键盘控制。
- **@capacitor/filesystem**：文件系统访问（读写本地文件）。
- **@capacitor/haptics**：震动与触觉反馈。
- **@capacitor/network**：网络状态检测。
- **@capacitor/share**：系统分享能力。
- **@capacitor/splash-screen**：启动页管理。
- **@capacitor/status-bar**：状态栏控制。
- **@capacitor/app**：应用生命周期、最小化、退出等。
- **@capacitor-community/app-icon**：应用图标切换。
- **capacitor-android-nav-mode**：Android 导航栏模式。
- **capacitor-application-context**：应用上下文扩展。
- **capacitor-biometric-lock**：生物识别锁。
- **capacitor-clear-cache**：清理缓存。
- **capacitor-launch-native**：启动原生应用或功能。
- **capacitor-plugin-safe-area**：安全区域适配。
- **capacitor-reader**：文件阅读器。
- **capacitor-share-safari**：Safari 分享扩展。
- **capacitor-stash-media**：媒体资源存储。
- **capacitor-tips**：原生提示与引导。

> 这些插件极大提升了 PWA 在移动端的原生能力，包括文件操作、分享、震动、网络检测、安全、UI 适配等，满足多样化业务需求。

---

## 开发规范

### 1. 依赖与脚本管理

- 推荐使用 pnpm 作为包管理器，所有依赖声明于 package.json。
- 常用脚本：
  - `pnpm install` 安装依赖
  - `pnpm run dev` 启动前端开发服务器
  - `pnpm run build` 构建前端产物
  - `pnpm run lint` 代码风格检查
  - `pnpm run test` 单元测试
  - `pnpm run test:e2e` 端到端测试

### 2. 目录与模块组织

- 每个功能模块应包含：
  - 组件文件（.tsx）
  - 样式文件（.module.css）
  - 状态管理文件（xxxSlice.ts）
  - 测试文件（.test.tsx）
  - 类型定义（可在组件文件或单独 types.ts）
- 服务层（src/services）：统一通过 tRPC 客户端调用后端 API，类型自动推导。
- 辅助函数、工具类统一放在 helpers/ 和 utils/。

### 3. React 与 Redux 最佳实践

- 使用函数组件和 Hooks，避免类组件。
- 组件应为纯函数，避免副作用。
- 使用 React.memo 优化渲染。
- 使用 React.lazy 和 Suspense 进行代码分割。
- 状态管理推荐使用 Redux Toolkit，按模块拆分 slice。

### 4. 代码风格与质量

- 强制使用 ESLint 检查代码风格，Prettier 自动格式化。
- 所有新功能需配套单元测试（Vitest）、端到端测试（Playwright）。
- 类型定义优先采用 TypeScript，接口类型由 tRPC 自动推导。

### 5. API 与后端开发

- 后端 API 统一通过 tRPC 路由暴露，前端直接类型安全调用。
- 数据库 schema 统一维护于 backend/schema.sql，支持迁移与扩展。
- 后端支持 JWT 鉴权、参数校验、全局异常处理。

---

## 启动与部署

### 前端开发
```bash
pnpm install
pnpm run dev
```

### 后端开发
```bash
npm install -g wrangler
cd backend
wrangler dev
```

### 构建与部署
```bash
pnpm run build         # 前端构建
wrangler deploy        # 后端部署
```

---

## 相关文档

- manuall-docs/架构文档和开发规范.md
- manuall-docs/代码规范.md
- manuall-docs/项目新手指南.md
- backend/README.md

---

## 贡献与反馈

欢迎提 issue、PR 或参与讨论，共同完善本通用全栈 PWA Starter 项目！
