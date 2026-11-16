# Yuai 文档站

独立的 VitePress 文档站，发布到 GitHub Pages。主系统不需要新增路由或重新打包，只需在后台填写文档链接。

## 填入 Yuai 后台

- 文档链接：`https://xiubia.github.io/yuai-docs/`
- 关于内容：复制 `deliverables/about.html` 的完整内容，粘贴到支持 HTML 的「关于」设置并保存。
- 在顶部导航配置中启用「文档」和「关于」。不要将文档链接填写到 API 服务地址。

关于 HTML 使用主系统的相对链接 `/pricing`、`/keys`、`/usage-logs`，并通过绝对地址打开文档。样式支持主系统 `.dark`，且不依赖脚本，因此可通过现有 HTML 清理与隔离渲染。

## 本地维护

```sh
bun install --frozen-lockfile
bun run dev
bun run build
bun run preview
```

正文位于 `site/`，目录与导航在 `site/.vitepress/config.mts`，颜色与字体在 `site/.vitepress/theme/custom.css`。推送到 `main` 自动构建并发布。GitHub 仓库 Settings → Pages 的 Source 为 GitHub Actions。

默认发布子路径为 `/yuai-docs/`。如改仓库名或绑定独立域名，同步修改 VitePress base、favicon 和 CSS 字体地址。复制字体文件时保留 `site/public/fonts/` 的许可证。

文档只记录接入方式。价格、套餐、退款、联系方式与隐私承诺以实际站点配置和运营方公布为准。未提供正式 API 域名，因此用 `YUAI_BASE_URL` 表示从 Yuai 首页复制的地址，避免将文档域名当成网关。

`deliverables/service-terms-draft.md` 是未发布的条款准备稿，不在 `site/` 中，不会进入 Pages 或站内搜索。不要直接作为正式法律条款上线。

## 来源与边界

教程依据官方客户端文档与 Yuai 当前控制台能力编写。官方参考链接附在对应文章末尾。OpenCode 1.x 和 2.x 分别提供配置，pi 的环境变量插值遵循当前官方配置。没有复制其他站点的套餐、联系方式或价格保护承诺。

Yuai 网关基于 New API / QuantumNous，并保留 One API 来源说明。此仓库中的字体分别遵循其附带的 OFL 许可证。文档与样式为 Yuai 接入场景编写。
