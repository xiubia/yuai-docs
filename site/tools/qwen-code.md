# Qwen Code

使用 OpenAI 兼容认证，让 Qwen Code 访问 Yuai 提供的模型。

## 安装

按 [官方仓库](https://github.com/QwenLM/qwen-code) 安装。已有兼容 Node.js 环境时：

```bash
npm install -g @qwen-code/qwen-code
qwen --version
```

## 配置环境变量

先按 [快速开始](/guide/quickstart) 准备三个 `YUAI_` 变量，再转换为客户端要求的名字：

::: code-group
```bash [macOS / Linux / WSL]
export OPENAI_API_KEY="$YUAI_API_KEY"
export OPENAI_BASE_URL="$YUAI_BASE_URL/v1"
export OPENAI_MODEL="$YUAI_MODEL"
qwen
```

```powershell [Windows PowerShell]
$env:OPENAI_API_KEY = $env:YUAI_API_KEY
$env:OPENAI_BASE_URL = "$env:YUAI_BASE_URL/v1"
$env:OPENAI_MODEL = $env:YUAI_MODEL
qwen
```
:::

已有其他认证方式时，通过 `/auth` 选择 API Key / OpenAI 兼容方式。账户登录的免费额度与 Yuai 密钥属于不同的凭据来源。

## 验证与排错

发送简短请求，然后核对 Yuai 使用日志。若仍指向其他服务，检查 `~/.qwen/settings.json` 中保存的 `modelProviders`、`security.auth.selectedType` 和模型配置是否覆盖了本次选择。更新这些字段时保留其他工具与项目设置。

请求失败时，确认模型支持 Chat Completions 与工具调用，且密钥有权限访问该模型。

官方参考：[Qwen Code 认证配置](https://github.com/QwenLM/qwen-code/blob/main/docs/users/configuration/auth.md)。
