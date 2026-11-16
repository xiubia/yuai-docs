# OpenCode

先运行 `opencode --version` 查看版本。OpenCode 1.x 与 2.x 的配置结构不同，请选择匹配的一份。

## 安装与参数

从 [官方页面](https://opencode.ai/download) 安装，按 [快速开始](/guide/quickstart) 准备密钥、API 根地址和模型 ID。以下示例使用 Chat Completions，请选择支持该接口和工具调用的模型。

## OpenCode 2.x

在项目的 `opencode.jsonc` 中合并：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "providers": {
    "yuai": {
      "name": "Yuai",
      "env": ["YUAI_API_KEY"],
      "package": "@opencode/ai/providers/openai-compatible",
      "settings": {
        "baseURL": "填入 API 根地址/v1"
      },
      "models": {
        "填入实际模型 ID": { "name": "Yuai 模型" }
      }
    }
  }
}
```

## OpenCode 1.x

在项目的 `opencode.json` 或用户配置 `~/.config/opencode/opencode.json` 中合并：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "yuai": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Yuai",
      "options": {
        "baseURL": "填入 API 根地址/v1",
        "apiKey": "{env:YUAI_API_KEY}"
      },
      "models": {
        "填入实际模型 ID": { "name": "Yuai 模型" }
      }
    }
  }
}
```

如果 1.x 使用的是 Responses 模型，官方建议将 `npm` 改为 `@ai-sdk/openai`。协议选择要与模型能力一致。

## 选择模型与验证

将地址和模型占位文字替换为真实值，保持已有配置的其他字段。从设置了环境变量的终端启动 `opencode`，在模型选择器中选择 `yuai/实际模型ID`，发送一个短请求。

桌面版需要在启动环境中提供密钥；终端里临时导出的变量不会传入已经运行的桌面程序。若模型不出现，检查配置文件位置、JSON 格式、版本和凭据来源。

官方参考：[提供商配置](https://opencode.ai/docs/providers/) · [配置文件](https://opencode.ai/docs/config/)。
