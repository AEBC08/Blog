# Memory 索引

本目录记录博客从 AstroPaper 迁移到 Fuwari、以及后续配置的全部决策与操作，按类别存放。

## 目录结构

```text
memory/
├─ README.md              # 本索引
├─ overview.md            # 项目现状与目标
├─ decisions/             # 决策记录（ADR，一条一个文件）
│  └─ README.md           # 决策索引
├─ logs/                  # 操作与验证日志（按日期）
│  ├─ 2026-11-01-install.md
│  ├─ 2026-11-01-configuration.md
│  └─ 2026-11-01-verification.md
├─ guides/                # 可复用的操作指南
│  └─ frontmatter-migration.md
└─ tasks/                 # 待办事项
   └─ todo.md
```

## 约定

- **决策**：文件名 `D-<编号>-<短横线描述>.md`，包含状态、日期、背景、决策、理由、影响。
- **日志**：文件名 `YYYY-MM-DD-<主题>.md`，只记录实际执行过的命令与结果。
- **指南**：面向以后的操作步骤，不记录一次性事件。
- **待办**：可勾选清单，完成后移入日志或删除。
- 新决策追加编号，不修改旧决策正文；被取代时在旧文件标注 `状态：已被 D-xxx 取代`。

## 快速跳转

- 当前部署地址：`https://aebc08.github.io/Blog/`
- 当前主题：Fuwari（commit `6d39b0dec41282e7852e23e032998a5789abee28`）
- 旧站备份：`.backup/astropaper-2026-11-01/`
- 部署前待办：[`tasks/todo.md`](tasks/todo.md)
