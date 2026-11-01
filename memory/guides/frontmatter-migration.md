# 文章 Frontmatter 迁移指南（AstroPaper → Fuwari）

> 旧文章目前都在 `.backup/astropaper-2026-11-01/src/content/posts/`，需要时按本文恢复。

## 字段映射

| AstroPaper | Fuwari | 说明 |
| --- | --- | --- |
| `title` | `title` | 必填 |
| `pubDatetime` | `published` | Fuwari 使用 `YYYY-MM-DD` 或日期字符串 |
| `modDatetime` | `updated` | 可选 |
| `description` | `description` | 可选，默认空 |
| `tags` | `tags` | 字符串数组 |
| `draft` | `draft` | 可选，默认 `false` |
| `slug` | — | Fuwari 由文件路径决定 URL |
| `featured` | — | Fuwari schema 无置顶字段 |
| `author` | — | 作者信息统一在 `src/config.ts` 的 profile 中 |
| `ogImage` | `image` | 文章封面/分享图，支持相对路径 |
| `canonicalURL` | — | Fuwari schema 无此字段 |

Fuwari 额外字段：`category`（分类）、`lang`（文章语言，可选）。

## 文件格式

- Fuwari 默认只集成 Markdown，**没有** `@astrojs/mdx`；旧 `.mdx` 需改为 `.md` 并去掉组件 import。
- 单文件：`src/content/posts/my-post.md`
- 带封面：`src/content/posts/my-post/index.md` + `image: "./cover.jpg"`

## 示例

```yaml
---
title: 我的第一篇文章
published: 2026-11-01
description: 文章摘要
image: ./cover.jpg
tags: [随笔, Astro]
category: 技术
draft: false
lang: zh_CN
---
```

## 步骤

1. 从备份复制需要的文章。
2. 按上表改写 frontmatter，删除 AstroPaper 专属字段和 MDX import。
3. 把引用的图片复制到文章同级目录，路径改为相对路径。
4. `pnpm dev` 检查渲染，`pnpm build` 检查构建。
