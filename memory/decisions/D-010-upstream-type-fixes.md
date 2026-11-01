# D-010 对上游两处类型错误做最小修复

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

安装后 `pnpm check` 报 2 个错误，而 Fuwari 自带的 CI 会执行 `pnpm astro check`：

1. `src/components/Navbar.astro:54`：`<LightDarkSwitch client:only="svelte">` 报 `client:only` 与 `Record<string, never>` 不兼容（Svelte 5 对无 prop 组件的类型生成 + Astro 指令注入）。
2. `src/pages/archive.astro:12`：`ArchivePanel` 缺少必填的 `tags`/`categories`，且 `PostForList` 的 `category` 为 `string | null`，与组件内 `category?: string` 不匹配。

## 决策

只做两处最小改动：

1. `LightDarkSwitch.svelte` 用 `$props()` 声明可选 `class` prop 并应用到根节点；既满足类型检查，也提供样式扩展点。
2. `ArchivePanel.svelte` 给 `tags`/`categories` 默认值 `[]`，并把 `category` 类型改为 `string | null`（与 `src/content/config.ts` 的 schema 一致）。运行时行为不变，因为这两个值本来就会被 URL 参数覆盖。

## 理由

保持主题功能与上游一致，同时让 CI 的类型检查通过；不引入大范围改动。

## 影响

与上游有 2 个文件的差异，后续升级 Fuwari 时需要保留这两处补丁（或等上游修复后移除）。
