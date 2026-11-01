# D-005 站点身份信息先保留 Fuwari 占位值

- **状态**：已被 D-011 / D-012 取代
- **日期**：2026-11-01

## 背景

安装时没有用户真实的站点标题、作者、GitHub 用户名或部署地址；当前 AstroPaper 配置也是演示值（`astro-paper.pages.dev`、Sat Naing）。目录名 `GhPages` 暗示 GitHub Pages，但当时没有远程仓库信息。

## 决策

安装阶段保持 Fuwari 的占位配置可运行，不猜测真实 URL；在待办中列出必须修改的字段。

## 理由

错误的 `site`/`base` 会导致 GitHub Pages 子路径部署时资源 404，比占位更危险；占位配置可以正常本地构建和预览。

## 影响

部署前必须完成 `astro.config.mjs` 与 `src/config.ts` 的配置。后续用户提供了 GitHub Pages 信息，已由 D-011、D-012 完成。
