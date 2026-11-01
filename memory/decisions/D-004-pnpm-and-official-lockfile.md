# D-004 使用 pnpm，并以官方 lockfile 为准

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

Fuwari 通过 `preinstall: npx only-allow pnpm` 强制使用 pnpm；原站也使用 pnpm。

## 决策

删除 AstroPaper 的 `pnpm-lock.yaml` 和 `node_modules`，使用 Fuwari 仓库自带的 `pnpm-lock.yaml` 执行 `pnpm install`。

## 理由

保证依赖树与上游一致，避免旧主题依赖残留（Astro 7 / Tailwind 4）与新主题（Astro 5 / Tailwind 3）冲突。

## 影响

首次安装需要重新下载依赖；`manage-package-manager-versions = true` 会让 pnpm 12 自动切换到项目声明的 pnpm 9.14.4。
