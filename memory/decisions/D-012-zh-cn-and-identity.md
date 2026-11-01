# D-012 启用 zh_CN 并设置站点身份信息

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

用户要求博客语言使用 `zh_CN`；同时站点仍使用 Fuwari 的占位标题、作者和社交链接，不适合作为个人博客。

## 决策

在 `src/config.ts` 中设置：

- `siteConfig.lang`: `zh_CN`
- `siteConfig.title`: `AEBC08 的博客`
- `siteConfig.subtitle`: `记录与分享`
- `profileConfig.name`: `AEBC08`
- `profileConfig.bio`: `记录与分享`
- 导航栏和 Profile 的 GitHub 链接：`https://github.com/AEBC08`
- 只保留 GitHub 一个社交链接

同时把 `src/content/spec/about.md` 改写为个人简介，而不是删除（`about.astro` 在缺失内容时会抛错）。

## 理由

语言是用户明确要求；标题、作者和链接需要与用户身份一致，否则首页仍显示 Fuwari 演示信息。

## 影响

- HTML `lang="zh-CN"`，Fuwari 自带 `zh_CN` 翻译生效（导航、归档、搜索等界面为中文）。
- RSS 的 `<language>` 为 `zh_CN`。
- 验证：首页标题为 `AEBC08 的博客 - 记录与分享`。
