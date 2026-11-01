# 2026-11-01 验证日志

## 环境

| 项目 | 版本 |
| --- | --- |
| Node.js | v24.21.0 |
| pnpm（全局） | 12.9.1 |
| pnpm（项目实际执行） | 9.14.4 |
| Astro | 5.13.10 |
| Fuwari commit | `6d39b0dec41282e7852e23e032998a5789abee28` |

## 1. 依赖安装

- 命令：`pnpm install --registry=https://registry.npmjs.org/`
- 结果：成功，1109 个包，8m22.8s（第二次重试，第一次因 Windows `EBUSY` 中断）。
- 锁文件与上游一致（`Lockfile is up to date`）。

## 2. 类型检查

```text
$ pnpm check
Result (55 files):
- 0 errors
- 0 warnings
- 1 hint
```

- 唯一 hint：上游 `src/plugins/expressive-code/language-badge.ts:10` 的 `_cssVar` 未使用，不影响构建。

## 3. 生产构建（最终配置）

命令：`pnpm build`（清空 `.astro`、`node_modules/.vite`、`dist` 后执行）

- Astro：3 个页面（首页、归档、关于），构建成功。
- 空文章集合警告：`The collection "posts" does not exist or is empty` —— 预期，因为示例文章已全部删除。
- Pagefind：索引 1 个页面（关于页）、16 个词，语言 `zh-cn`；不支持中文词干，但搜索仍可用。
- `dist/` 顶层：`index.html`、`about/`、`archive/`、`pagefind/`、`favicon/`、`_astro/`、`robots.txt`、`rss.xml`、`sitemap-index.xml`、`sitemap-0.xml`。

## 4. 子路径链接核对

| 文件 | 结果 |
| --- | --- |
| `sitemap-0.xml` | `https://aebc08.github.io/Blog/`、`/Blog/about/`、`/Blog/archive/` |
| `robots.txt` | `Sitemap: https://aebc08.github.io/Blog/sitemap-index.xml` |
| `rss.xml` | channel `<link>` 为 `https://aebc08.github.io/Blog/`，`<language>zh_CN</language>` |
| `index.html` | `<html lang="zh-CN">`，标题 `AEBC08 的博客 - 记录与分享`，资源均以 `/Blog/` 开头 |

## 5. 本地预览冒烟测试

命令：`pnpm exec astro preview --port 4400`（干净端口）

| 路径 | 状态 | 大小 |
| --- | --- | --- |
| `/Blog/` | 200 | 36,208 B |
| `/Blog/archive/` | 200 | 35,072 B |
| `/Blog/about/` | 200 | 35,939 B |
| `/Blog/rss.xml` | 200 | 224 B |
| `/Blog/sitemap-index.xml` | 200 | 192 B |
| `/Blog/sitemap-0.xml` | 200 | 504 B |
| `/Blog/pagefind/pagefind.js` | 200 | 33,851 B |
| `/Blog/favicon/favicon-light-32.png` | 200 | 554 B |

- CSS：5 个 stylesheet 正常输出，`custom-md` 样式存在。
- 备注：本机 `astro preview` 只监听 IPv6 `::1`，请用 `http://localhost:<port>/Blog/`，不要用 `127.0.0.1`。
- 测试完成后已关闭预览进程。

## 6. 结论

- `pnpm check`、`pnpm build`、子路径预览均通过。
- 站点已按 GitHub Pages 项目页配置，可直接推送并由 Actions 部署。
- 剩余事项见 `tasks/todo.md`。
