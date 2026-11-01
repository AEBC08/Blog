# D-011 配置 GitHub Pages 项目页的 site/base

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

用户确认部署到 GitHub Pages **项目页**，GitHub 账号为 `AEBC08`；本地目录名为 `Blog`，据此推断仓库名为 `Blog`。

## 决策

在 `astro.config.mjs` 中设置：

```js
site: "https://aebc08.github.io",
base: "/Blog",
```

## 理由

- GitHub Pages 项目页的访问路径是 `https://<用户名>.github.io/<仓库名>/`。
- `site` 只写到域名，`base` 单独写仓库路径，符合 Astro 官方 GitHub Pages 配置方式；`Astro.url`、sitemap 和内部链接会自动组合出 `/Blog/` 前缀。

## 影响

- 所有站内链接、favicon、RSS、sitemap 都带 `/Blog/` 前缀。
- 如果实际仓库名不是 `Blog`，必须同步修改 `base`；否则部署后资源会 404。
- 已验证构建产物：`https://aebc08.github.io/Blog/`、`/Blog/about/`、`/Blog/archive/` 均正确。
- **2026-11-01 补充**：用户确认仓库名即为 `Blog`，且已创建远程仓库并部署成功，配置无需调整。
