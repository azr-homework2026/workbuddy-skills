---
name: learning-skill
description: 我的第一个 WorkBuddy Skill —— 用于记录学习过程中的可复用工作流。
---

# learning-skill

这是一个占位 Skill，用来演示 `.workbuddy/skills/<name>/SKILL.md` 的标准结构。

## 何时使用

- 当你完成一段新的学习任务、踩到一个明显的坑、或总结出一个可复用的工作流时，把要点写到这里。

## 如何扩展

1. 在 `scripts/` 目录里加入可执行脚本（可选）。
2. 在 `references/` 目录里放入参考资料（可选）。
3. 更新本文件的 `description`，让智能体能更准确地判断何时加载。

## 目录约定

```
.workbuddy/skills/learning-skill/
├── SKILL.md        # 本文件 —— 技能说明（必需）
├── scripts/        # 可执行脚本（可选）
└── references/     # 参考资料（可选）
```
