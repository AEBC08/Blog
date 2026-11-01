# D-009 安装时临时改用 npm 官方源（不改项目配置）

- **状态**：已采纳
- **日期**：2026-11-01

## 背景

本机 pnpm 全局 registry 为 `https://registry.npmmirror.com/`，但该域名在本机 DNS 解析失败（`ENOTFOUND` / `ETIMEDOUT`），导致首次安装卡住；`https://registry.npmjs.org/` 实测返回 200。

## 决策

本次安装通过命令行参数 `--registry=https://registry.npmjs.org/` 使用官方源；**不**把 registry 写入项目的 `.npmrc`。

## 理由

镜像可用性因网络环境而异，写死到项目会覆盖用户/CI 的全局选择；命令行覆盖只影响本次安装。pnpm 的 store 是内容寻址的，之前从镜像已下载的包仍可复用。

## 影响

以后在本机重装若仍走默认镜像失败，可加同样的 `--registry` 参数；GitHub Actions 默认使用官方源，不受影响。
