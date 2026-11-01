# 待办

## 部署前

- [ ] 确认 GitHub 仓库名确实是 `Blog`。如果不是，修改 `astro.config.mjs` 的 `base`（例如仓库名为 `blog` 则改为 `/blog`）。
- [ ] 在仓库 **Settings → Pages → Build and deployment → Source** 选择 **GitHub Actions**。
- [ ] 确认默认分支是 `main`；不是的话修改 `.github/workflows/deploy.yml` 的 `branches`。
- [ ] 初始化 git 并推送：

  ```powershell
  git init
  git add .
  git commit -m "feat: migrate blog to Fuwari"
  git branch -M main
  git remote add origin https://github.com/AEBC08/Blog.git
  git push -u origin main
  ```

## 内容

- [ ] 用 `pnpm new-post <文件名>` 创建第一篇文章（`src/content/posts/` 目前为空）。
- [ ] 如需恢复旧文章，参考 `guides/frontmatter-migration.md`。
- [ ] 更新 `src/content/spec/about.md` 的个人简介（当前为简短占位）。
- [ ] 更换头像 `src/assets/images/avatar.png`（当前是本地生成的字母头像）。

## 可选定制

- [ ] 自定义 favicon：替换 `public/favicon/`，或在 `siteConfig.favicon` 配置。
- [ ] 调整主题色：`siteConfig.themeColor.hue`（0–360，当前 250 蓝色）。
- [ ] 开启 banner：`siteConfig.banner.enable = true`，并把 `banner.src` 换成自己的图片。
- [ ] 修改版权协议：`licenseConfig`。
- [ ] 确认 `.backup/` 不再需要后再删除（已 gitignore，不会被提交）。

## 已知事项

- `src/content/posts/` 为空时，构建会提示 `The collection "posts" does not exist or is empty`，属预期，不影响构建。
- 对上游源码有 6 个文件被本地修改，升级 Fuwari 时需保留：
  - `LightDarkSwitch.svelte`、`ArchivePanel.svelte`（D-010）
  - `Layout.astro`、`robots.txt.ts`、`rss.xml.ts`、`markdown.css`（D-014 / D-015）
