# 仓库贡献指南

## 项目结构与模块组织
- 根目录包含 `server`（Go/Gin 后端）与 `website`（React + TypeScript，Vite）。
- 前端源码：`website/src`（入口 `website/src/main.tsx`，主组件 `website/src/App.tsx`）。静态资源：`website/public`、`website/src/assets`。构建产物：`website/dist`。
- 后端入口：`server/main.go`。模块定义：`server/go.mod`，依赖：`server/go.sum`。
- 文档：`README.md`。包管理器：npm。

## 构建、测试与开发命令
- 前端开发：`cd website && npm run dev` — 启动 Vite 开发服务器。
- 前端构建：`cd website && npm run build` — 先编译 TypeScript，再进行 Vite 生产构建。
- 前端预览：`cd website && npm run preview` — 本地服务 `dist` 构建产物。
- 前端代码检查：`cd website && npm run lint` — 运行 ESLint（参考 `website/eslint.config.js`）。
- 后端运行：`cd server && go run .` — 启动 Gin 服务，默认 `http://localhost:8080`。
- 后端构建：`cd server && go build` — 在 `server/` 目录生成可执行文件。

## 代码风格与命名约定
- TypeScript/React：遵循 ESLint 推荐规则、React Hooks 与 Vite Refresh 配置。2 空格缩进；变量/函数 `camelCase`，组件 `PascalCase`。
- 文件命名：组件 `*.tsx`，工具 `*.ts`；资源置于 `website/src/assets`。
- Go：使用 `go fmt` 格式化；本地标识符 `camelCase`，导出标识符 `PascalCase`；按功能分组 HTTP 处理器。

## 测试指南
- 当前未配置测试。若新增：
  - 前端：建议使用 Vitest/Jest；测试文件命名 `*.test.tsx`，或放在 `website/src/__tests__`。
  - 后端：使用 Go `testing`；测试文件命名 `*_test.go`，与源码同目录。
  - 关注路由、组件与 hooks 的有效覆盖率。

## 提交与 Pull Request 规范
- 提交风格示例：`feat: initial`。遵循 Conventional Commits（如 `feat`、`fix`、`docs`、`chore`）。主题行不超过 72 字符，必要时包含 scope。
- Pull Request：提供清晰描述、关联 Issue、运行步骤；UI 变更附截图。确保 `npm run lint` 通过，前后端可成功构建（`npm run build`、`go build`）。

## 安全与配置提示（可选）
- 不要提交秘钥。使用环境变量或 `.env` 文件，并通过 `.gitignore` 忽略。
- 服务端进行输入校验与清理；返回结构化 JSON，使用合适的 `http.Status*`。
- 固定 Node（v18+）与 Go 版本；使用 `npm ci` 保证可复现安装。
