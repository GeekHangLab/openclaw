# 🦞 OpenClaw — 个人 AI 助手

<p align="center">
    <picture>
        <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text-dark.png">
        <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text.png" alt="OpenClaw" width="500">
    </picture>
</p>

<p align="center">
  <strong>去壳！去壳！</strong>
</p>

<p align="center">
  <a href="https://github.com/openclaw/openclaw/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/openclaw/openclaw/ci.yml?branch=main&style=for-the-badge" alt="CI 状态"></a>
  <a href="https://github.com/openclaw/openclaw/releases"><img src="https://img.shields.io/github/v/release/openclaw/openclaw?include_prereleases&style=for-the-badge" alt="GitHub 发布版本"></a>
  <a href="https://discord.gg/clawd"><img src="https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT 许可证"></a>
</p>

**OpenClaw** 是一款运行在您自己设备上的_个人 AI 助手_。
它可以在您日常使用的聊天频道上回复您（WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、BlueBubbles、IRC、Microsoft Teams、Matrix、飞书、LINE、Mattermost、Nextcloud Talk、Nostr、Synology Chat、Tlon、Twitch、Zalo、Zalo Personal、WebChat），支持在 macOS/iOS/Android 上语音交互，并可渲染由您掌控的实时画布（Canvas）。Gateway 是控制平面，而产品核心是 AI 助手本身。

[官网](https://openclaw.ai) · [文档](https://docs.openclaw.ai) · [愿景](VISION.md) · [DeepWiki](https://deepwiki.com/openclaw/openclaw) · [入门指南](https://docs.openclaw.ai/start/getting-started) · [更新指南](https://docs.openclaw.ai/install/updating) · [展示](https://docs.openclaw.ai/start/showcase) · [FAQ](https://docs.openclaw.ai/help/faq) · [向导](https://docs.openclaw.ai/start/wizard) · [Docker](https://docs.openclaw.ai/install/docker) · [Discord](https://discord.gg/clawd)

📖 **[English README](README.md)**

---

## 目录

- [开发语言与技术栈](#开发语言与技术栈)
- [功能概览](#功能概览)
- [安装](#安装)
- [快速开始](#快速开始)
- [从源码构建](#从源码构建)
- [安全默认设置](#安全默认设置)
- [如何工作](#如何工作)

---

## 开发语言与技术栈

### 主要语言

OpenClaw 的核心代码库使用 **TypeScript**（ESM 模块，严格模式）编写。这是参与核心开发所需的首要语言。

| 组件 | 语言 / 技术 |
|---|---|
| 核心 Gateway / CLI / 插件 SDK | **TypeScript** (Node 22+, ESM) |
| macOS 菜单栏应用 | **Swift** / SwiftUI |
| iOS 节点应用 | **Swift** / SwiftUI |
| Android 节点应用 | **Kotlin** / Jetpack Compose |
| 控制 UI（Web 前端）| **TypeScript** / Lit |
| 构建工具 | tsdown、pnpm、Bun（可选） |
| 代码检查 / 格式化 | Oxlint、Oxfmt |
| 测试框架 | Vitest（V8 覆盖率） |

### 如果您想参与贡献

- **核心功能、CLI、Gateway、插件**：使用 TypeScript（ESM）。
- **macOS / iOS 应用**：使用 Swift / SwiftUI（`apps/macos`、`apps/ios`）。
- **Android 应用**：使用 Kotlin（`apps/android`）。
- **文档**：Markdown + Mintlify（`docs/`）。

> **推荐**：如果您只是想扩展 OpenClaw（添加新频道、工具或技能），请使用 **TypeScript** 编写 npm 插件包，通过插件 SDK（`openclaw/plugin-sdk`）接入。这是最简单、风险最低的贡献方式。

### 运行时要求

- Node.js **≥22**（生产环境）
- pnpm（推荐，用于开发构建）
- Bun（可选，用于直接执行 TypeScript 脚本）

---

## 功能概览

### 核心平台

- **[本地优先 Gateway](https://docs.openclaw.ai/gateway)**：单一控制平面，统一管理会话、频道、工具和事件；内置 WebSocket 控制平面、[控制 UI](https://docs.openclaw.ai/web)、[Canvas 宿主](https://docs.openclaw.ai/platforms/mac/canvas#canvas-a2ui)。
- **[CLI 工具集](https://docs.openclaw.ai/tools/agent-send)**：`gateway`、`agent`、`send`、[向导](https://docs.openclaw.ai/start/wizard)、[doctor 诊断](https://docs.openclaw.ai/gateway/doctor)。
- **Pi 智能体运行时**：RPC 模式，支持工具流式传输与数据块流式传输。
- **[会话模型](https://docs.openclaw.ai/concepts/session)**：`main` 直聊、群组隔离、激活模式、队列模式、回复投递。
- **[媒体管道](https://docs.openclaw.ai/nodes/images)**：图片/音频/视频处理、转录钩子、大小上限、临时文件生命周期管理。

### 支持的消息频道

OpenClaw 支持多达 **24+ 个**消息频道，实现真正的多渠道统一收件箱：

| 频道 | 说明 |
|---|---|
| [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) | 通过 Baileys 库接入 |
| [Telegram](https://docs.openclaw.ai/channels/telegram) | 通过 grammY 库接入 |
| [Slack](https://docs.openclaw.ai/channels/slack) | 通过 Bolt SDK 接入 |
| [Discord](https://docs.openclaw.ai/channels/discord) | 通过 discord.js 接入 |
| [Google Chat](https://docs.openclaw.ai/channels/googlechat) | 通过 Chat API 接入 |
| [Signal](https://docs.openclaw.ai/channels/signal) | 通过 signal-cli 接入 |
| [BlueBubbles](https://docs.openclaw.ai/channels/bluebubbles) | iMessage（推荐方式） |
| [iMessage（旧版）](https://docs.openclaw.ai/channels/imessage) | 通过 imsg 脚本接入 |
| [IRC](https://docs.openclaw.ai/channels/irc) | 标准 IRC 协议 |
| [Microsoft Teams](https://docs.openclaw.ai/channels/msteams) | Bot Framework 接入 |
| [Matrix](https://docs.openclaw.ai/channels/matrix) | 去中心化协议 |
| [飞书 / Feishu](https://docs.openclaw.ai/channels/feishu) | 飞书开放平台 |
| [LINE](https://docs.openclaw.ai/channels/line) | LINE Messaging API |
| [Mattermost](https://docs.openclaw.ai/channels/mattermost) | 开源团队协作 |
| [Nextcloud Talk](https://docs.openclaw.ai/channels/nextcloud-talk) | 自托管协作 |
| [Nostr](https://docs.openclaw.ai/channels/nostr) | 去中心化社交协议 |
| [Synology Chat](https://docs.openclaw.ai/channels/synology-chat) | Synology NAS 内置聊天 |
| [Tlon / Urbit](https://docs.openclaw.ai/channels/tlon) | 去中心化 Urbit 网络 |
| [Twitch](https://docs.openclaw.ai/channels/twitch) | 直播频道聊天 |
| [Zalo](https://docs.openclaw.ai/channels/zalo) | 越南主流社交应用 |
| [Zalo Personal](https://docs.openclaw.ai/channels/zalouser) | Zalo 个人账号 |
| [WebChat](https://docs.openclaw.ai/web/webchat) | Gateway 内置浏览器聊天 |

### 配套应用与节点

- **[macOS 应用](https://docs.openclaw.ai/platforms/macos)**：菜单栏控制平台，支持语音唤醒/PTT、对话模式叠加层、WebChat、调试工具、远程 Gateway 控制。
- **[iOS 节点](https://docs.openclaw.ai/platforms/ios)**：Canvas、语音唤醒、对话模式、摄像头、屏幕录制、Bonjour 设备配对。
- **[Android 节点](https://docs.openclaw.ai/platforms/android)**：连接标签页（二维码/手动）、聊天会话、语音标签页、Canvas、摄像头/屏幕录制，以及 Android 设备命令（通知、位置、短信、照片、联系人、日历、运动、应用更新）。
- **[macOS 节点模式](https://docs.openclaw.ai/nodes)**：system.run/notify + Canvas/摄像头暴露接口。

### 工具与自动化

- **[浏览器控制](https://docs.openclaw.ai/tools/browser)**：专用 Chrome/Chromium、页面快照、操作执行、文件上传、多配置文件。
- **[Canvas 画布](https://docs.openclaw.ai/platforms/mac/canvas)**：[A2UI](https://docs.openclaw.ai/platforms/mac/canvas#canvas-a2ui) 推送/重置、脚本执行、快照。
- **[节点工具](https://docs.openclaw.ai/nodes)**：摄像头拍照/录制、屏幕录制、[位置获取](https://docs.openclaw.ai/nodes/location-command)、系统通知。
- **[定时任务与唤醒](https://docs.openclaw.ai/automation/cron-jobs)**；[Webhook](https://docs.openclaw.ai/automation/webhook)；[Gmail Pub/Sub](https://docs.openclaw.ai/automation/gmail-pubsub)。
- **[技能平台](https://docs.openclaw.ai/tools/skills)**：内置、托管、工作区技能，支持安装门控与 UI 管理。

### 多智能体路由

- **[多智能体路由](https://docs.openclaw.ai/gateway/configuration)**：将入站频道/账号/联系人路由到隔离的独立智能体（独立工作区 + 独立会话）。
- **[群组路由](https://docs.openclaw.ai/channels/group-messages)**：@提及门控、回复标签、按频道分块与路由。
- **[频道路由](https://docs.openclaw.ai/channels/channel-routing)**、[重试策略](https://docs.openclaw.ai/concepts/retry)、[流式传输与分块](https://docs.openclaw.ai/concepts/streaming)。

### 语音与 TTS

- **[语音唤醒（Voice Wake）](https://docs.openclaw.ai/nodes/voicewake)**：macOS/iOS 唤醒词，Android 连续语音。
- **[对话模式（Talk Mode）](https://docs.openclaw.ai/nodes/talk)**：全双工语音覆盖层。
- TTS 支持 ElevenLabs 以及系统内置 TTS 降级方案。

### 模型与 AI 提供商

- 支持 OpenAI、Anthropic Claude、Google Gemini、Qwen 通义千问、MiniMax 以及更多提供商。
- [模型选择与认证](https://docs.openclaw.ai/concepts/models)；[模型故障转移](https://docs.openclaw.ai/concepts/model-failover)。
- OAuth 订阅与 API Key 轮换。

### 插件生态

- **插件 SDK**（`openclaw/plugin-sdk`）：类型安全的频道/工具插件接口。
- **扩展目录**（`extensions/`）：官方扩展，包含 Matrix、Microsoft Teams、Mattermost、Zalo 等频道插件。
- **[MCP 支持](https://github.com/steipete/mcporter)**：通过 mcporter 灵活集成模型上下文协议。
- **[技能平台](https://docs.openclaw.ai/tools/skills)**：可发布到 ClawHub，社区驱动的技能生态。

### 运维与部署

- **[控制 UI](https://docs.openclaw.ai/web)**：直接由 Gateway 提供服务。
- **[Tailscale Serve/Funnel](https://docs.openclaw.ai/gateway/tailscale)** 或 **[SSH 隧道](https://docs.openclaw.ai/gateway/remote)**（带 token/密码认证）。
- **[Nix 模式](https://docs.openclaw.ai/install/nix)**：声明式配置；**[Docker 部署](https://docs.openclaw.ai/install/docker)**。
- **[Doctor 诊断](https://docs.openclaw.ai/gateway/doctor)**：迁移检查、配置审计与日志分析。

---

## 安装

运行时要求：**Node ≥22**。

```bash
npm install -g openclaw@latest
# 或者: pnpm add -g openclaw@latest

openclaw onboard --install-daemon
```

向导会自动安装 Gateway 守护进程（launchd/systemd 用户服务），确保其持续运行。

---

## 快速开始

```bash
# 一键入门向导
openclaw onboard --install-daemon

# 启动 Gateway
openclaw gateway --port 18789 --verbose

# 发送消息
openclaw message send --to +1234567890 --message "来自 OpenClaw 的问候"

# 与助手对话
openclaw agent --message "列出今日待办" --thinking high
```

---

## 从源码构建

推荐使用 `pnpm` 进行源码构建，Bun 可选（用于直接运行 TypeScript）。

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw

pnpm install
pnpm ui:build   # 首次运行时自动安装 UI 依赖
pnpm build

pnpm openclaw onboard --install-daemon

# 开发循环（TypeScript 变更自动热重载）
pnpm gateway:watch
```

常用开发命令：

| 命令 | 说明 |
|---|---|
| `pnpm install` | 安装所有依赖 |
| `pnpm build` | 编译 TypeScript 输出到 `dist/` |
| `pnpm tsgo` | TypeScript 类型检查 |
| `pnpm check` | 代码检查与格式化（Oxlint + Oxfmt） |
| `pnpm test` | 运行测试套件（Vitest） |
| `pnpm openclaw ...` | 通过 tsx 直接运行（开发模式） |

---

## 安全默认设置

OpenClaw 连接到真实的消息平台。请将入站 DM 视为**不可信输入**。

**DM 配对机制**（默认启用）：未知发件人会收到一个短配对码，机器人不会处理其消息，直到您通过以下命令审批：

```bash
openclaw pairing approve <channel> <code>
```

运行 `openclaw doctor` 可检测危险或配置错误的 DM 策略。

完整安全指南：[安全文档](https://docs.openclaw.ai/gateway/security)

---

## 如何工作

```
WhatsApp / Telegram / Slack / Discord / Signal / iMessage / ...
               │
               ▼
┌───────────────────────────────┐
│            Gateway            │
│         （控制平面）           │
│     ws://127.0.0.1:18789      │
└──────────────┬────────────────┘
               │
               ├─ Pi 智能体（RPC）
               ├─ CLI（openclaw …）
               ├─ WebChat UI
               ├─ macOS 应用
               └─ iOS / Android 节点
```

Gateway 是核心路由层，负责：
- 接收来自各频道的入站消息
- 路由到对应的 Pi 智能体（可按频道/账号/联系人隔离）
- 管理会话状态、工具调用、流式回复
- 将响应回传到原始频道

---

## 贡献指南

欢迎参与贡献！请查阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解详情。

- **Bugs 与小修复** → 直接提 PR！
- **新功能 / 架构调整** → 先在 [GitHub Discussion](https://github.com/openclaw/openclaw/discussions) 或 Discord 讨论
- **问题求助** → Discord [#help](https://discord.com/channels/1456350064065904867/1459642797895319552)

提交 PR 前请运行：

```bash
pnpm build && pnpm check && pnpm test
```

---

## 许可证

[MIT License](LICENSE)
