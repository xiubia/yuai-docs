# Claude Code · Linux / WSL

通过 Anthropic Messages 接口连接 Yuai。Base URL 填网关根地址，不加 `/v1`。

## 安装

按 [Claude Code 官方安装说明](https://code.claude.com/docs/en/setup) 选择 Linux / WSL 对应方式。安装后运行 `claude --version` 确认命令可用。

在 Linux 终端中运行。WSL 是独立的 Linux 环境，请在 WSL 内安装工具、设置变量并进入项目目录；Windows 用户变量不会可靠地同步到 WSL。

## 设置地址与凭据

先按 [快速开始](/guide/quickstart) 设置 `YUAI_BASE_URL`、`YUAI_API_KEY` 与 `YUAI_MODEL`。选择支持 Anthropic Messages 和 Claude Code 所需工具调用的模型，在同一个终端执行：

```bash
export ANTHROPIC_BASE_URL="$YUAI_BASE_URL"
export ANTHROPIC_AUTH_TOKEN="$YUAI_API_KEY"
claude --model "$YUAI_MODEL"
```

`ANTHROPIC_AUTH_TOKEN` 以 Bearer token 发送网关密钥。若已有其他 Anthropic 凭据，检查实际生效来源，避免沿用旧服务的登录配置。

## 验证连接

在 Claude Code 中执行 `/status`，确认 Anthropic base URL 是你的 Yuai 地址，凭据来源是 `ANTHROPIC_AUTH_TOKEN`。发送一条短消息，并在 Yuai 使用日志中核对模型和请求。

## 持久配置

用户级 `~/.claude/settings.json`（Windows 为 `%USERPROFILE%\.claude\settings.json`）支持 `env` 字段：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "填入 API 根地址",
    "ANTHROPIC_AUTH_TOKEN": "填入你的 API 密钥"
  }
}
```

合并到已有 JSON，不要覆盖其他配置。该文件包含明文密钥，应保存在受保护的用户目录，不要提交到项目仓库。这里填写实际值，不能假设 JSON 自动展开 `$YUAI_API_KEY`。设置文件中的同名变量可能覆盖终端变量，修改后用 `/status` 再确认。

## 排查问题

- **仍出现登录提示**：确认从设置过变量的终端启动，或凭据已放在用户级配置中。
- **404**：检查根地址是否误加 `/v1`，以及模型 ID 是否正确。
- **400 / 工具调用失败**：检查模型支持的协议与参数，保留错误字段并反馈，避免通过关闭执行审批来排查模型问题。
- **终端可用、编辑器不可用**：各客户端读取配置的位置不同，参考官方对应界面的设置。

官方参考：[网关连接配置](https://code.claude.com/docs/en/llm-gateway-connect)。
