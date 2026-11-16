# Codex 桌面端

桌面端的本地编程任务可以使用自定义模型服务。先完成 [Codex CLI 配置](/codex/cli)，再让桌面程序读取相同的提供商与凭据。

## 安装与配置

从 [官方下载页](https://chatgpt.com/download/) 安装包含 Codex 的桌面版本。当前官方桌面体验可能显示为 ChatGPT；系统支持和功能入口以安装版本为准。

打开用户目录下的 `~/.codex/config.toml`，按 [CLI 教程](/codex/cli#配置服务) 配置 `yuai` 提供商。在文件顶层设置 `model = "实际模型 ID"` 与 `model_provider = "yuai"`。桌面 UI 提供自定义网关表单时，也可填写同样的 Base URL 和环境变量名称。

## 让应用读取密钥

桌面端必须能够读取 `YUAI_API_KEY`。在一个终端里执行 `export`，不会自动更新已经运行的桌面进程。

### Windows

通过 Windows「编辑账户的环境变量」添加用户变量 `YUAI_API_KEY`，值为你的密钥。完全退出应用后重新打开；若仍读取旧环境，注销并重新登录 Windows。不要把环境变量设置截图公开。

### macOS

先在终端准备 `YUAI_API_KEY`，然后传给当前登录会话启动的图形应用：

```bash
launchctl setenv YUAI_API_KEY "$YUAI_API_KEY"
```

完全退出应用后重新打开。此设置不保证跨注销或重启持久化；新的登录会话需要重新设置，或使用你的凭据管理工具加载。

### Linux

先在终端导出 `YUAI_API_KEY`，再从该终端启动实际安装的桌面可执行程序。桌面快捷方式通常不继承另一个终端的临时变量，具体启动命令以安装包为准。

## 验证本地任务

创建新的本地会话，选择一个测试项目，让它简要解释项目结构。到 Yuai 使用日志确认模型、密钥和请求已生效。已有会话可能保留原配置，需要新建会话验证。

Yuai 密钥用于模型服务。账号登录、云端任务、插件和外部网站仍使用客户端各自的服务与权限；能调用模型不代表这些功能全部可用。

官方参考：[Codex 配置](https://developers.openai.com/codex/config-advanced/) · [桌面设置](https://developers.openai.com/codex/app/settings/)。
