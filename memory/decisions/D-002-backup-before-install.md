# D-002 安装前先做完整备份

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

目录不是 git 仓库，删除后无法用 git 恢复。

## 决策

把当前站点（排除 `node_modules/`、`.astro/`、`dist/`、`.backup/`、`memory/`）复制到 `E:\GhPages\Blog\.backup\astropaper-2026-11-01\`，并把 `.backup/` 加入 `.gitignore`。

## 理由

只备份源码和内容即可完整还原，同时避免复制 300MB 依赖；加入 gitignore 可避免误提交和部署。

## 影响

可随时回滚；备份不会出现在构建产物中。
