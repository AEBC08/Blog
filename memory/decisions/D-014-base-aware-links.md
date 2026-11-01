# D-014 修复子路径部署下的 RSS / robots 链接

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

`base` 改为 `/Blog` 后，检查发现 Fuwari 上游有三处链接没有拼接 `base`：

1. `src/layouts/Layout.astro`：`href={`${Astro.site}rss.xml`}` → 生成 `https://aebc08.github.io/rss.xml`（缺少 `/Blog/`）。
2. `src/pages/robots.txt.ts`：`new URL("sitemap-index.xml", import.meta.env.SITE)` → 缺少 `/Blog/`。
3. `src/pages/rss.xml.ts`：`site: context.site` → RSS channel 的 `<link>` 指向域名根目录。

## 决策

- Layout 中改为 `new URL(url("/rss.xml"), Astro.site ?? Astro.url.origin)`。
- robots 中改为 `new URL(`${import.meta.env.BASE_URL}sitemap-index.xml`, import.meta.env.SITE)`。
- RSS 中 `site` 改为 `new URL(url("/"), context.site ?? ...)`。

## 理由

GitHub Pages 项目页所有资源都在 `/Blog/` 下，RSS 自动发现和 sitemap 声明必须指向正确路径，否则阅读器和搜索引擎会 404。

## 影响

- 构建产物验证：`robots.txt` 的 Sitemap 为 `https://aebc08.github.io/Blog/sitemap-index.xml`。
- RSS `<link>` 为 `https://aebc08.github.io/Blog/`。
- HTML `<link rel="alternate" ... rss.xml>` 为 `https://aebc08.github.io/Blog/rss.xml`。
- 这是对上游的额外补丁，升级时需保留（与 D-010 类似）。
