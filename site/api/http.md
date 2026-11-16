# HTTP API 与 SDK

先按 [快速开始](/guide/quickstart) 设置 `YUAI_BASE_URL`、`YUAI_API_KEY` 和 `YUAI_MODEL`。根地址不带 `/v1`，模型 ID 取自你的 Yuai 模型广场。

## 接口选择

| 接口             | 方法与路径                  | 用途                       |
| ---------------- | --------------------------- | -------------------------- |
| 模型列表         | `GET /v1/models`            | 查询当前凭据可见的模型     |
| Chat Completions | `POST /v1/chat/completions` | OpenAI 兼容聊天            |
| Responses        | `POST /v1/responses`        | Codex 等客户端所用响应接口 |
| Messages         | `POST /v1/messages`         | Anthropic 兼容消息         |
| Embeddings       | `POST /v1/embeddings`       | 使用支持向量化的模型       |

支持的端点取决于模型、分组及站点配置。先用小请求验证对应接口，再接入复杂的多模态或工具调用。

## Python：Chat Completions

```bash
python -m pip install openai
```

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url=os.environ["YUAI_BASE_URL"].rstrip("/") + "/v1",
    api_key=os.environ["YUAI_API_KEY"],
)
response = client.chat.completions.create(
    model=os.environ["YUAI_MODEL"],
    messages=[{"role": "user", "content": "你好"}],
)
print(response.choices[0].message.content)
```

## Responses

在同一 Python 客户端中，使用支持 Responses 的模型：

```python
response = client.responses.create(
    model=os.environ["YUAI_MODEL"],
    input="简要介绍这个接口。",
)
print(response.output_text)
```

## JavaScript / TypeScript

```bash
npm install openai
```

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: process.env.YUAI_BASE_URL.replace(/\/+$/, "") + "/v1",
  apiKey: process.env.YUAI_API_KEY,
});
const response = await client.responses.create({
  model: process.env.YUAI_MODEL,
  input: "你好",
});
console.log(response.output_text);
```

该代码应运行在服务端或本地 Node.js 中。公开网页前端不应持有你的 API 密钥。

## Python：Anthropic Messages

```bash
python -m pip install anthropic
```

```python
import os
from anthropic import Anthropic

client = Anthropic(
    base_url=os.environ["YUAI_BASE_URL"].rstrip("/"),
    api_key=os.environ["YUAI_API_KEY"],
)
message = client.messages.create(
    model=os.environ["YUAI_MODEL"],
    max_tokens=256,
    messages=[{"role": "user", "content": "你好"}],
)
for block in message.content:
    if block.type == "text":
        print(block.text)
```

SDK 自动追加 `/v1/messages`，所以 `base_url` 填网关根地址。直接发送 HTTP 时，使用 `x-api-key`、`anthropic-version: 2023-06-01` 和 JSON 请求体。

## 流式响应与错误处理

使用对应 SDK 的流式接口并消费到结束。HTTP 200 可能仅表示流已开始；流中仍可能返回错误或异常断开。应处理 SDK 异常、超时和完成事件，并保留响应提供的请求 ID 便于定位。

对 429 或暂时性 5xx 采取有上限的退避重试。对 401、权限、额度或参数错误，先修正原因。具有外部副作用的任务应确认执行状态，避免重试造成重复操作。

官方参考：[OpenAI Python](https://github.com/openai/openai-python) · [OpenAI Node](https://github.com/openai/openai-node) · [Anthropic Python](https://github.com/anthropics/anthropic-sdk-python)。
