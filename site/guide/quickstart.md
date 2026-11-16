# 快速开始

准备 Yuai 账户、API 密钥和一个可用模型，先完成一次简单请求，再配置 Coding Agent。

## 1. 注册并查看可用服务

在你使用的 Yuai 站点注册并登录。注册方式由站点配置决定；未开放注册时，联系该站点管理员。

打开「模型广场」，确认模型 ID、可用分组、支持的接口和价格。需要余额或套餐时，先在「控制台 → 钱包」查看当前可用的购买方式与说明。

## 2. 创建 API 密钥

进入 **控制台 → API 密钥 → 创建**：

1. 用项目或工具命名，例如 `local-codex`。
2. 选择账户可用的分组。
3. 设置额度、有效期，按需限制模型或 IP。
4. 保存后复制密钥，并放入本机的环境变量或凭据管理工具。

每个项目使用独立密钥，方便停用、轮换和核对用量。完整密钥不要发给他人，不要放进 Git 仓库、截图或网页前端代码。

## 3. 准备连接参数

从首页复制 API 根地址，从模型广场复制模型 ID。下列中文内容必须替换为你自己的值。

::: code-group
```bash [macOS / Linux / WSL]
export YUAI_BASE_URL='填入首页的 API 根地址'
export YUAI_API_KEY='填入你的 API 密钥'
export YUAI_MODEL='填入模型广场中的模型 ID'
```

```powershell [Windows PowerShell]
$env:YUAI_BASE_URL = '填入首页的 API 根地址'
$env:YUAI_API_KEY = '填入你的 API 密钥'
$env:YUAI_MODEL = '填入模型广场中的模型 ID'
```
:::

这些变量只影响当前终端及从它启动的程序。下面的教程复用这三个变量；新开终端时需要重新设置。正式使用时通过你信任的凭据管理方式加载密钥，避免把明文密钥留在共享终端历史中。

## 4. 完成首次调用

先获取当前密钥可见的模型：

::: code-group
```bash [macOS / Linux / WSL]
curl -sS "$YUAI_BASE_URL/v1/models" \
  -H "Authorization: Bearer $YUAI_API_KEY"
```

```powershell [Windows PowerShell]
Invoke-RestMethod -Uri "$env:YUAI_BASE_URL/v1/models" `
  -Headers @{ Authorization = "Bearer $env:YUAI_API_KEY" }
```
:::

选用支持 Chat Completions 的模型发送消息：

::: code-group
```bash [macOS / Linux / WSL]
# 使用 Python 生成 JSON，避免模型名称中的字符破坏请求体。
python3 -c 'import json,os; print(json.dumps({"model":os.environ["YUAI_MODEL"],"messages":[{"role":"user","content":"你好"}]}))' | \
  curl -sS "$YUAI_BASE_URL/v1/chat/completions" \
    -H "Authorization: Bearer $YUAI_API_KEY" \
    -H "Content-Type: application/json" --data-binary @-
```

```powershell [Windows PowerShell]
$body = @{
  model = $env:YUAI_MODEL
  messages = @(@{ role = 'user'; content = '你好' })
} | ConvertTo-Json -Depth 5
Invoke-RestMethod -Uri "$env:YUAI_BASE_URL/v1/chat/completions" `
  -Method Post -Headers @{ Authorization = "Bearer $env:YUAI_API_KEY" } `
  -ContentType 'application/json; charset=utf-8' -Body ([Text.Encoding]::UTF8.GetBytes($body))
```
:::

响应中出现正常的 `choices` 和消息内容，即完成了这次调用。只支持 Responses 的模型请使用 [Responses 示例](/api/http#responses)。收到 HTML 登录页或错误 JSON 时，按 [常见问题](/guide/faq) 排查。

## 接入日常工具

接下来配置 [Claude Code](/claude-code/macos)、[Codex](/codex/cli)、[OpenCode](/tools/opencode) 或 [桌面客户端](/guide/downloads)。先发送一条短消息，再运行较长的代码任务；在控制台「使用日志」确认模型与用量。
