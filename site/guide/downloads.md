# 客户端下载

优先使用客户端官方发布入口。安装完成后，按对应教程添加 Yuai 地址和密钥。

## 选择客户端

| 你的用途                       | 客户端        | 下载与接入                                                                                          |
| ------------------------------ | ------------- | --------------------------------------------------------------------------------------------------- |
| 在桌面中读代码、修改项目       | Codex 桌面端  | [官方入口](https://chatgpt.com/download/) · [Yuai 配置](/codex/desktop)                             |
| 开源编程 Agent，终端和桌面共用 | OpenCode      | [官方下载](https://opencode.ai/download) · [Yuai 配置](/tools/opencode)                             |
| 多模型聊天与 API 调试          | Cherry Studio | [官方下载](https://www.cherry-ai.com/download)                                                      |
| 在编辑器内执行代码任务         | Cline         | [官方安装说明](https://docs.cline.bot/getting-started/installing-cline) · [Yuai 配置](/tools/cline) |

Codex 已整合进新版 ChatGPT 桌面体验。以官方入口列出的系统、架构和安装要求为准，确认下载的版本包含 Codex 功能。不要将 Yuai API 密钥填入 ChatGPT 账户登录表单。

## 终端工具

- Claude Code：[官方安装说明](https://code.claude.com/docs/en/setup)。
- Codex CLI：[官方仓库](https://github.com/openai/codex)。
- OpenCode：[官方文档](https://opencode.ai/docs/)。
- Qwen Code：[官方仓库](https://github.com/QwenLM/qwen-code)。
- pi：[官方仓库](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)。
- Aider：[官方安装说明](https://aider.chat/docs/install.html)。

## Cherry Studio 接入

在模型服务设置中添加 OpenAI 兼容服务，地址填 **Yuai API 根地址 + `/v1`**，密钥填 Yuai API Key，然后获取或手动添加模型。选择模型后发送短消息验证；部分版本会自动补全 `/v1`，请检查实际请求路径，避免 `/v1/v1`。

## 网络与更新

模型请求发送到配置的 Yuai 网关。软件安装、账号登录、扩展、更新与外部网站访问使用各自的服务，网络要求分别取决于这些服务。

下载失败时回到官方页面选择系统对应的安装方式，不要关闭系统安全校验。更新客户端后，确认自定义服务地址、模型与密钥仍生效。反馈下载问题时提供操作系统、CPU 架构与失败链接即可，无需发送 API 密钥。
