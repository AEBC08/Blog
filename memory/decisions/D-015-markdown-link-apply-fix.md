# D-015 移除 markdown.css 对自定义 `link` 类的依赖

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

删除全部示例文章后，`pnpm build` 曾报错：

```text
[vite:css] [postcss] src/styles/markdown.css:23:9: The `link` class does not exist.
```

原因：`markdown.css` 里的 `a:not(.no-styling)` 使用 `@apply ... link ...`，而 `link` 是 `main.css` 中 `@layer components` 定义的自定义类。Tailwind 只有在页面内容中出现 `link` 时才会生成该类；删光示例文章后内容里不再出现 `link`，`@apply` 就找不到它。该问题与构建顺序/缓存有关，表现为偶发失败。

## 决策

把 `@apply` 中的 `link` 替换为它提供的等价工具类：

```css
@apply relative bg-none transition rounded-md p-1 -m-1 font-medium text-[var(--primary)] ...
```

## 理由

不依赖 Tailwind 是否扫描到自定义类，保证空内容、任意内容下都能稳定构建；视觉上保留 padding、圆角、过渡和主题色。Markdown 链接本身已有 hover 背景样式，去掉 `expand-animation` 的伪元素动画影响很小。

## 影响

- 清空 `.astro`、`node_modules/.vite`、`dist` 后重新构建成功。
- 这是对上游的额外补丁，升级 `markdown.css` 时需保留。
