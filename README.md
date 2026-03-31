# Claude Code

![](https://img.shields.io/badge/Node.js-18%2B-brightgreen?style=flat-square) [![npm]](https://www.npmjs.com/package/@anthropic-ai/claude-code)

[npm]: https://img.shields.io/npm/v/@anthropic-ai/claude-code.svg?style=flat-square

Claude Code is an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster by executing routine tasks, explaining complex code, and handling git workflows -- all through natural language commands. Use it in your terminal, IDE, or tag @claude on Github.

**Learn more at [Claude Code Homepage](https://claude.com/product/claude-code)** | [Documentation](https://code.claude.com/docs/en/overview)

<img src="https://github.com/anthropics/claude-code/blob/main/demo.gif?raw=1" />

## Get started

1. Install Claude Code:

```sh
npm install -g @anthropic-ai/claude-code
```

2. Navigate to your project directory and run `claude`.

## Reporting Bugs

We welcome your feedback. Use the `/bug` command to report issues directly within Claude Code, or file a [GitHub issue](https://github.com/anthropics/claude-code/issues).

## Connect on Discord

Join the [Claude Developers Discord](https://anthropic.com/discord) to connect with other developers using Claude Code. Get help, share feedback, and discuss your projects with the community.

## Data collection, usage, and retention

When you use Claude Code, we collect feedback, which includes usage data (such as code acceptance or rejections), associated conversation data, and user feedback submitted via the `/bug` command.

### How we use your data

See our [data usage policies](https://code.claude.com/docs/en/data-usage).

### Privacy safeguards

We have implemented several safeguards to protect your data, including limited retention periods for sensitive information and restricted access to user session data.

For full details, please review our [Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms) and [Privacy Policy](https://www.anthropic.com/legal/privacy).

---

## 内部模块结构解析

> 以下内容基于 `@anthropic-ai/claude-code@2.1.88` npm 包中附带的 Source Map 还原的 `src/` 目录结构整理。
> Claude Code 为 Anthropic 闭源商业产品，本仓库内容并非官方开源发布。

### 顶层文件

| 文件 | 说明 |
|---|---|
| `main.tsx` | 应用入口 |
| `Tool.ts` | 工具基类定义 |
| `Task.ts` | 任务基类定义 |
| `query.ts` | 查询核心逻辑 |
| `QueryEngine.ts` | 查询引擎 |
| `context.ts` | 上下文管理 |
| `tasks.ts` | 任务调度 |
| `tools.ts` | 工具注册 |
| `commands.ts` | 命令注册 |
| `cost-tracker.ts` | Token 费用追踪 |
| `setup.ts` | 初始化配置 |
| `history.ts` | 对话历史管理 |

### 核心运行时

| 模块 | 文件数 | 说明 |
|---|---|---|
| `assistant/` | 1 | AI 助手核心逻辑 |
| `coordinator/` | 1 | 多 Agent 协调器 |
| `bootstrap/` | 1 | 启动引导 |
| `context/` | 9 | 上下文管理（项目、会话、环境等）|
| `state/` | 6 | 全局状态管理 |
| `query/` | 4 | 查询引擎相关 |

### 工具系统（`tools/` · 43个工具）

| 工具 | 说明 |
|---|---|
| `BashTool` | 执行 Shell 命令 |
| `FileReadTool` | 读取文件 |
| `FileEditTool` | 编辑文件 |
| `FileWriteTool` | 写入文件 |
| `GlobTool` | 文件路径匹配 |
| `GrepTool` | 内容搜索 |
| `WebFetchTool` | 抓取网页 |
| `WebSearchTool` | 网络搜索 |
| `AgentTool` | 启动子 Agent |
| `TaskCreateTool` | 创建任务 |
| `TaskGetTool` | 获取任务 |
| `TaskListTool` | 列出任务 |
| `TaskUpdateTool` | 更新任务 |
| `TaskStopTool` | 停止任务 |
| `TaskOutputTool` | 获取任务输出 |
| `MCPTool` | MCP 协议工具 |
| `McpAuthTool` | MCP 鉴权 |
| `ListMcpResourcesTool` | 列出 MCP 资源 |
| `ReadMcpResourceTool` | 读取 MCP 资源 |
| `SkillTool` | 执行 Skill |
| `ToolSearchTool` | 搜索可用工具 |
| `SendMessageTool` | 发送消息（Agent 间通信）|
| `RemoteTriggerTool` | 远程触发器 |
| `ScheduleCronTool` | 定时任务 |
| `EnterPlanModeTool` | 进入计划模式 |
| `ExitPlanModeTool` | 退出计划模式 |
| `EnterWorktreeTool` | 进入 Git Worktree |
| `ExitWorktreeTool` | 退出 Git Worktree |
| `NotebookEditTool` | Jupyter Notebook 编辑 |
| `AskUserQuestionTool` | 向用户提问 |
| `ConfigTool` | 配置管理 |
| `REPLTool` | 交互式 REPL |
| `LSPTool` | LSP 语言服务协议 |
| `TodoWriteTool` | 写入 Todo |
| `TeamCreateTool` | 创建团队 |
| `TeamDeleteTool` | 删除团队 |
| `BriefTool` | 简报工具 |
| `SleepTool` | 等待/延迟 |
| `PowerShellTool` | PowerShell 命令（Windows）|
| `SyntheticOutputTool` | 合成输出 |

### 命令系统（`commands/` · 101个命令）

用户可调用的斜杠命令（`/xxx`），部分示例：

`clear` / `compact` / `commit` / `config` / `branch` / `brief` / `advisor` / `autofix-pr` / `bughunter` / `chrome` / `color` / `agents` / `bridge` 等

### UI 层

| 模块 | 文件数 | 说明 |
|---|---|---|
| `components/` | 144 | React/Ink UI 组件 |
| `ink/` | 48 | Ink（终端 React）相关组件 |
| `screens/` | 3 | 主界面页面 |
| `hooks/` | 85 | React Hooks |
| `keybindings/` | 14 | 键盘快捷键绑定 |
| `vim/` | 5 | Vim 模式支持 |

### 服务层（`services/` · 36个服务）

| 服务 | 说明 |
|---|---|
| `api/` | Anthropic API 调用 |
| `mcp/` | MCP 服务器管理 |
| `oauth/` | OAuth 鉴权 |
| `lsp/` | LSP 语言服务 |
| `analytics/` | 使用分析 |
| `compact/` | 对话压缩 |
| `extractMemories/` | 记忆提取 |
| `MagicDocs/` | 文档生成 |
| `plugins/` | 插件管理 |
| `notifier.ts` | 通知系统 |
| `diagnosticTracking.ts` | 诊断追踪 |

### 通信与协议

| 模块 | 文件数 | 说明 |
|---|---|---|
| `bridge/` | 31 | IDE 插件通信桥（VS Code / JetBrains）|
| `server/` | 3 | 本地 HTTP 服务 |
| `remote/` | 4 | 远程 Agent 通信 |
| `upstreamproxy/` | 2 | 上游代理 |

### 其他模块

| 模块 | 文件数 | 说明 |
|---|---|---|
| `skills/` | 4 | Skill 系统（用户自定义技能）|
| `tasks/` | 9 | 任务执行引擎 |
| `buddy/` | 6 | Buddy（协作 Agent）|
| `utils/` | 329 | 通用工具函数（最大模块）|
| `types/` | 8 | TypeScript 类型定义 |
| `constants/` | 21 | 常量配置 |
| `memdir/` | 8 | 记忆目录管理 |
| `migrations/` | 11 | 数据迁移脚本 |
| `schemas/` | 1 | 数据结构 Schema |
| `entrypoints/` | 6 | 多端入口（CLI/Web/IDE）|
| `cli/` | 8 | CLI 参数解析 |
| `native-ts/` | 3 | 原生 TypeScript 绑定 |
| `voice/` | 1 | 语音输入支持 |
| `plugins/` | 2 | 插件系统 |
