# pi

通过自定义模型配置，把 Yuai 加入 pi 的模型选择器。

## 安装

按 [pi 官方说明](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) 安装，确认 `pi --version` 能运行。按 [快速开始](/guide/quickstart) 设置 `YUAI_API_KEY`。

## 配置模型

编辑 `~/.pi/agent/models.json`，在已有 `providers` 中合并 `yuai`：

```json
{
  "providers": {
    "yuai": {
      "baseUrl": "填入 API 根地址/v1",
      "api": "openai-completions",
      "apiKey": "$YUAI_API_KEY",
      "models": [{ "id": "填入实际模型 ID" }]
    }
  }
}
```

地址和模型 ID 必须替换。当前 pi 支持在 `apiKey` 中使用 `$变量名` 环境插值；不要将真实密钥写入公开配置。若使用了自定义 Agent 目录，配置文件位置也随之变化。

## 使用与验证

从设置了密钥的终端运行 `pi`，执行 `/model` 并选择 Yuai 模型。打开模型选择器会重新加载配置；看不到模型时检查 JSON 格式及凭据是否可读取。

先让模型回答短问题，再测试工具调用。上下文长度、输出上限与能力声明应根据实际模型填写，不要复制其他模型的参数。本示例选择 `openai-completions`，需要与模型的协议能力匹配。

官方参考：[模型配置](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/models.md)。
