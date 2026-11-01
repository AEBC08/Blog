# D-006 使用 GitHub 仓库快照（git clone）安装，固定 commit

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

可选方式有 `pnpm create fuwari@latest`、下载 ZIP、git clone。

## 决策

`git clone --depth 1` 官方仓库到临时目录，记录 commit hash 后再复制到项目。

- 安装基线：`6d39b0dec41282e7852e23e032998a5789abee28`
- 该 commit 日期：2025-12-12

## 理由

可以直接固定可复现的版本，避免交互式脚手架，也便于审查上游文件清单。

## 影响

安装版本可追溯；后续升级可参考该 commit 做 diff。
