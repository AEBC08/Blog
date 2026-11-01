# D-016 添加 GitHub Pages 部署工作流

- **状态**：已采纳（取代 D-008）
- **日期**：2026-11-01

## 背景

用户确认部署到 GitHub Pages 项目页。Fuwari 只自带 `.github/workflows/build.yml`（构建检查），不会发布站点；D-008 当时因信息不足没有添加部署配置。

## 决策

新增 `.github/workflows/deploy.yml`：

- 触发：`push` 到 `main`，以及手动 `workflow_dispatch`
- 权限：`contents: read`、`pages: write`、`id-token: write`
- 构建：pnpm 9.14.4 + Node 22 + `pnpm install --frozen-lockfile` + `pnpm build`
- 发布：`actions/upload-pages-artifact@v3` + `actions/deploy-pages@v4`
- 并发组：`pages`，不取消进行中的发布

## 理由

使用 GitHub 官方 Pages Actions，无需 `gh-pages` 分支；与项目声明的 pnpm 版本保持一致，确保 lockfile 可用。

## 影响

部署前需要在仓库 **Settings → Pages → Build and deployment → Source** 选择 **GitHub Actions**。如果默认分支不是 `main`，需修改 `deploy.yml` 的 `branches`。

- **2026-11-01 补充**：仓库 `AEBC08/Blog` 的 Pages 已通过 API 设为 `build_type: workflow`，默认分支为 `main`，首次推送即部署成功。
