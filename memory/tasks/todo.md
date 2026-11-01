# 待办

## 已完成（2026-11-01）

- [x] 确认 GitHub 仓库名为 `Blog`，`base: "/Blog"` 无需修改。
- [x] 创建仓库 `AEBC08/Blog`（公开，默认分支 `main`）。
- [x] 仓库 **Settings → Pages → Source** 设为 **GitHub Actions**（`build_type: workflow`）。
- [x] 初始化 git 并推送，首次部署成功。
- [x] 线上验证：https://aebc08.github.io/Blog/

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
- [ ] 绑定自定义域名（如需）：在仓库 Pages 设置中填 Custom domain，并在 `public/` 放 `CNAME`。

## 日常发布流程

```powershell
git add -A
git commit -m "post: 文章标题"
git push
```

推送后 GitHub Actions 自动构建并发布，约 1–2 分钟生效。

## 已知事项

- `src/content/posts/` 为空时，构建会提示 `The collection "posts" does not exist or is empty`，属预期，不影响构建。
- 对上游源码有 6 个文件被本地修改，升级 Fuwari 时需保留：
  - `LightDarkSwitch.svelte`、`ArchivePanel.svelte`（D-010）
  - `Layout.astro`、`robots.txt.ts`、`rss.xml.ts`、`markdown.css`（D-014 / D-015）
- 仓库 remote 为 `https://github.com/AEBC08/Blog.git`，认证依赖 Windows 凭据管理器中的 GitHub PAT；换机器需重新登录。
