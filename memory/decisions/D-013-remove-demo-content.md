# D-013 删除全部示例文章与演示图片

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

用户要求删除所有示例文档。此时 `src/content/posts/` 下是 Fuwari 自带的 5 篇示例文章和一个 guide 目录；`src/assets/images/` 下是演示头像和演示 banner，About 页也是 Fuwari 演示文案。

## 决策

1. 删除 `src/content/posts/` 下全部示例文章和图片，保留目录并新增 `.gitkeep`，方便以后用 `pnpm new-post`。
2. 删除 `demo-avatar.png`、`demo-banner.png`；用 Sharp 在本地生成一个 460×460 的字母头像 `avatar.png`（主题色渐变 + “A”），并把配置指向它。
3. 将 `src/content/spec/about.md` 改写为个人简介（不能直接删除，`about.astro` 在内容缺失时会抛错）。
4. 保留 Fuwari 的 `README.md`、`CONTRIBUTING.md`、`docs/`（见 D-007，它们不是博客示例文章）。

## 理由

- 示例文章引用 Fuwari 专属图片和语法，留着会污染首页和归档。
- 直接删除 About 内容会导致构建失败，改写是最小且安全的做法。
- GitHub 头像下载在本机网络下超时（502），本地生成头像可以避免留下动漫演示图。

## 影响

- 首页和归档页目前为空，构建时 Astro 会提示 `The collection "posts" does not exist or is empty`，这是预期警告，不影响构建。
- 站点只剩首页、归档、关于 3 个页面。
- 新建文章：`pnpm new-post <文件名>`。
- 如需换头像，替换 `src/assets/images/avatar.png` 或修改 `profileConfig.avatar`。
