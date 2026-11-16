# Codex CLI

Codex 通过 OpenAI Responses 接口连接 Yuai。先在模型广场选择支持 Responses 和工具调用的模型。

## 安装

按 [Codex 官方仓库](https://github.com/openai/codex) 安装当前稳定版。使用 npm 的环境可执行：

```bash
npm install -g @openai/codex
codex --version
```

## 设置凭据

先按 [快速开始](/guide/quickstart#_3-准备连接参数) 设置 `YUAI_BASE_URL`、`YUAI_API_KEY` 和 `YUAI_MODEL`。在启动 Codex 的同一终端中设置变量。

## 配置服务

编辑用户目录下的 `~/.codex/config.toml`，Windows 对应 `%USERPROFILE%\.codex\config.toml`。先备份已有文件，再合并以下设置，不要覆盖其他提供商、MCP 或项目配置。

```toml
model_provider = "yuai"

[model_providers.yuai]
name = "Yuai"
base_url = "填入 API 根地址/v1"
env_key = "YUAI_API_KEY"
wire_api = "responses"
requires_openai_auth = false
```

把 `base_url` 替换为实际完整地址，确保只出现一次 `/v1`。`env_key` 指向环境变量名，无需将密钥写入 TOML。`model_provider` 是顶层配置，须放在所有 `[表]` 之前。

## 启动并验证

::: code-group
```bash [macOS / Linux / WSL]
codex --model "$YUAI_MODEL"
```

```powershell [Windows PowerShell]
codex --model "$env:YUAI_MODEL"
```
:::

在一个测试项目中发起简短的代码阅读请求，检查控制台使用日志。需要固定默认模型时，在 TOML 顶层加 `model = "实际模型 ID"`；TOML 中的模型名不会自动展开 `$YUAI_MODEL`。

## 常见配置问题

- **提示缺少环境变量**：从设置了 `YUAI_API_KEY` 的终端启动，或重开已更新用户环境的应用。
- **404 / 不支持接口**：确认模型支持 `/v1/responses`；不要把 `wire_api` 改成 `chat`。
- **仍使用旧模型**：检查启动参数、profile、项目配置和已有会话的设置，修改后创建新会话。
- **工作区访问被限制**：按 Codex 自身的沙箱与批准设置处理。模型接入不需要关闭这些保护。

官方参考：[自定义模型提供商](https://developers.openai.com/codex/config-advanced/) · [配置参考](https://developers.openai.com/codex/config-reference/)。
