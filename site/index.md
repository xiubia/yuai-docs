# Yuai 文档

为 Claude Code、Codex 和你的应用配置统一的模型入口。从创建密钥开始，到工具接入、接口调用与用量排查。

## 从这里开始

- [快速开始](/guide/quickstart) · 创建密钥，完成第一次请求。
- [客户端下载](/guide/downloads) · 找到官方安装入口。
- [密钥与成本控制](/guide/api-keys) · 按项目管理额度、有效期与模型权限。
- [用量与计费](/guide/billing) · 理解用量记录、钱包与订阅。
- [常见问题](/guide/faq) · 排查地址、鉴权、模型与限流错误。

## 选择你的工具

| 工具         | 接口                         | 接入教程                                                                                          |
| ------------ | ---------------------------- | ------------------------------------------------------------------------------------------------- |
| Claude Code  | Anthropic Messages           | [macOS](/claude-code/macos) · [Windows](/claude-code/windows) · [Linux / WSL](/claude-code/linux) |
| Codex CLI    | OpenAI Responses             | [终端配置](/codex/cli)                                                                            |
| Codex 桌面端 | OpenAI Responses             | [桌面配置](/codex/desktop)                                                                        |
| OpenCode     | Chat Completions / Responses | [OpenCode](/tools/opencode)                                                                       |
| Qwen Code    | OpenAI 兼容接口              | [Qwen Code](/tools/qwen-code)                                                                     |
| pi           | OpenAI 兼容接口              | [pi](/tools/pi)                                                                                   |
| Cline        | OpenAI 兼容接口              | [Cline](/tools/cline)                                                                             |
| Aider        | OpenAI 兼容接口              | [Aider](/tools/aider)                                                                             |
| 应用与脚本   | HTTP / SDK                   | [HTTP API 与 SDK](/api/http)                                                                      |

模型是否可用、支持哪种接口及当前价格，以你使用的 Yuai 站点「模型广场」和账户分组为准。能列出模型不代表它支持每一种协议或工具调用。

## 地址怎么填

从 **Yuai 首页的 API 地址** 复制网关根地址。本文用 `YUAI_BASE_URL` 表示它，末尾不要带 `/v1` 或 `/`。

| 使用位置                               | 地址                                |
| -------------------------------------- | ----------------------------------- |
| Claude Code 的 `ANTHROPIC_BASE_URL`    | 网关根地址                          |
| OpenAI SDK / Codex / OpenAI 兼容客户端 | 网关根地址 + `/v1`                  |
| HTTP Chat Completions 请求             | 网关根地址 + `/v1/chat/completions` |
| HTTP Responses 请求                    | 网关根地址 + `/v1/responses`        |
| HTTP Anthropic Messages 请求           | 网关根地址 + `/v1/messages`         |

**这个 GitHub Pages 页面是文档站，不是模型 API 服务。** 不要把浏览器中当前文档网址填入客户端的 Base URL。

## 开源基础

Yuai 基于 [New API](https://github.com/QuantumNous/new-api)，由 [QuantumNous](https://github.com/QuantumNous) 开发的网关项目提供基础能力，并沿用 [One API](https://github.com/songquanpeng/one-api) 的开源基础。相关软件按各自许可证使用；New API 适用 AGPL v3.0。
