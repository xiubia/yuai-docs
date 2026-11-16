# Cline

在 Cline 中选择 OpenAI Compatible 提供商，填写 Yuai 的地址、密钥和模型。

## 安装

按 [官方安装说明](https://docs.cline.bot/getting-started/installing-cline) 为你的编辑器安装 Cline，打开 Cline 面板中的设置。

## 填写连接信息

| 字段         | 填写内容                  |
| ------------ | ------------------------- |
| API Provider | OpenAI Compatible         |
| Base URL     | Yuai API 根地址 + `/v1`   |
| API Key      | 为 Cline 创建的 Yuai 密钥 |
| Model ID     | 模型广场中的完整模型 ID   |

选择支持 Chat Completions 和工具调用的模型。若客户端需要上下文、输出上限、图片能力等参数，按所选模型的实际能力填写。

## 验证

在一个测试目录中提出简短问题，确认收到回复，并在 Yuai 使用日志中核对调用。Plan 与 Act 如果配置了不同模型，应分别检查提供商和密钥。

连接后按你的项目风险设置文件修改、命令执行与自动批准选项。更换模型服务不需要开启全部自动批准。

## 常见问题

401 通常需要核对密钥，404 优先核对地址是否重复 `/v1`，工具调用报错则检查模型能力。保存后仍使用旧配置时重新打开面板或新建任务。

官方参考：[OpenAI Compatible](https://docs.cline.bot/provider-config/openai-compatible)。
