# 2026-11-01 站点配置变更日志

在 Fuwari 安装完成的基础上，根据用户提供的信息完成部署配置与内容清理。

## 1. GitHub Pages 项目页配置（D-011）

`astro.config.mjs`：

```diff
-site: "https://fuwari.vercel.app/",
-base: "/",
+site: "https://aebc08.github.io",
+base: "/Blog",
```

## 2. 中文与站点身份（D-012）

`src/config.ts`：

- `lang`: `en` → `zh_CN`
- `title`: `Fuwari` → `AEBC08 的博客`
- `subtitle`: `Demo Site` → `记录与分享`
- `profileConfig.name`: `Lorem Ipsum` → `AEBC08`
- `profileConfig.bio`: 拉丁占位文 → `记录与分享`
- 导航栏 / Profile 的 GitHub 链接改为 `https://github.com/AEBC08`
- 删除 Twitter、Steam 演示链接，只保留 GitHub

`src/content/spec/about.md` 改写为个人简介。

## 3. 删除示例内容（D-013）

删除：

- `src/content/posts/draft.md`
- `src/content/posts/expressive-code.md`
- `src/content/posts/markdown.md`
- `src/content/posts/markdown-extended.md`
- `src/content/posts/video.md`
- `src/content/posts/guide/`（含 `index.md`、`cover.jpeg`）
- `src/assets/images/demo-avatar.png`
- `src/assets/images/demo-banner.png`

新增：

- `src/content/posts/.gitkeep`
- `src/assets/images/avatar.png`（用 Sharp 本地生成，460×460，字母 A）

## 4. 子路径链接修复（D-014 / D-015）

- `src/layouts/Layout.astro`：RSS 自动发现链接拼接 `base`。
- `src/pages/robots.txt.ts`：Sitemap 链接拼接 `BASE_URL`。
- `src/pages/rss.xml.ts`：RSS channel 链接改用站点根 + `base`。
- `src/styles/markdown.css`：`@apply link` 改为等价工具类，避免 Tailwind 在空内容时找不到自定义类。

## 5. 部署工作流（D-016）

新增 `.github/workflows/deploy.yml`：

- pnpm 9.14.4 + Node 22
- `pnpm install --frozen-lockfile`
- `pnpm build`
- `actions/upload-pages-artifact@v3` + `actions/deploy-pages@v4`

## 6. memory 重构（D-017）

将根目录的 `00-*.md` ~ `05-*.md` 迁移为：

- `README.md`、`overview.md`
- `decisions/`（D-001 ~ D-017，一条一个文件）
- `logs/`（本文件、安装日志、验证日志）
- `guides/`（frontmatter 迁移指南）
- `tasks/`（待办）

## 7. 验证

- `pnpm check`：0 errors / 0 warnings / 1 hint。
- `pnpm build`（清空缓存后）：3 个页面构建成功。
- `astro preview` 子路径测试：`/Blog/`、`/Blog/archive/`、`/Blog/about/`、RSS、sitemap、Pagefind、favicon 全部 200。
- 详见 `logs/2026-11-01-verification.md`。
