# 项目现状

- 日期：2026-11-01
- 工作目录：`E:\GhPages\Blog`
- 主题：Fuwari（https://github.com/saicaca/fuwari）
- 安装基线 commit：`6d39b0dec41282e7852e23e032998a5789abee28`
- 部署目标：GitHub Pages 项目页 `https://aebc08.github.io/Blog/`
- 仓库主人：AEBC08（https://github.com/AEBC08）

## 技术栈

| 项目 | 版本 |
| --- | --- |
| Astro | 5.13.10 |
| Svelte | 5.39.8 |
| Tailwind CSS | 3.4.19 |
| 包管理器 | pnpm 9.14.4（项目声明） |
| Node.js | v24.21.0（本地） |

## 当前站点配置

- `site`: `https://aebc08.github.io`
- `base`: `/Blog`
- 语言：`zh_CN`（HTML `lang="zh-CN"`）
- 标题：`AEBC08 的博客`
- 副标题：`记录与分享`
- 内容：示例文章已全部删除，`src/content/posts/` 为空（保留 `.gitkeep`）
- 关于页：已替换为个人简介
- 头像：本地生成的字母头像 `src/assets/images/avatar.png`
- 部署：`.github/workflows/deploy.yml`（GitHub Actions）

## 目录说明

- `memory/`：本次迁移与配置记录，不参与构建
- `.backup/astropaper-2026-11-01/`：旧 AstroPaper 站完整备份，已 gitignore
- `dist/`：构建产物
