# Aider

Aider 通过 OpenAI 兼容接口连接 Yuai。适合在终端里围绕 Git 项目进行代码修改。

## 安装

按 [官方安装说明](https://aider.chat/docs/install.html) 安装，确认 `aider --version` 能运行。在项目目录中启动前，先保存当前工作或建立可恢复的 Git 提交。

## 设置环境

按 [快速开始](/guide/quickstart) 准备三个 `YUAI_` 变量，再执行：

::: code-group
```bash [macOS / Linux / WSL]
export OPENAI_API_KEY="$YUAI_API_KEY"
export OPENAI_API_BASE="$YUAI_BASE_URL/v1"
aider --model "openai/$YUAI_MODEL"
```

```powershell [Windows PowerShell]
$env:OPENAI_API_KEY = $env:YUAI_API_KEY
$env:OPENAI_API_BASE = "$env:YUAI_BASE_URL/v1"
aider --model "openai/$env:YUAI_MODEL"
```
:::

这里的变量是 **`OPENAI_API_BASE`**，不是 `OPENAI_BASE_URL`。模型参数需要 `openai/` 前缀，后面接 Yuai 模型 ID。

## 验证与模型能力

先让 Aider解释一个小文件，确认回复与 Yuai 使用记录。模型需支持 Chat Completions；编辑格式、上下文长度与代码能力会影响实际修改效果。

Aider 对未内置的模型可能缺少上下文或成本元数据。只有掌握实际参数时才补充模型设置；界面估算金额以 Yuai 使用日志中的实际记录核对。

官方参考：[OpenAI-compatible APIs](https://aider.chat/docs/llms/openai-compat.html)。
