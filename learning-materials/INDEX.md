# Learning Materials 索引

> 本目录存放用 `concept-learning` Skill 产出的结构化学习资料。
> 每份资料按"七段式"产出：学习目标 / 核心问题 / 结构化解释 / 应用案例 / 概念辨析 / 自测题 / 参考来源。

## 资料清单

| 文件 | 概念 | 学习者背景 | 深度 | 生成日期 | 修订 |
|------|------|-----------|------|----------|------|
| `agent.md` | AI Agent | 学生 / 转行中 | 科普 + 工程 | 2026-09-10 | v1（待核读） |
| `llm-context.md` | LLM 上下文窗口 | 学生 / 转行中 | 科普 + 工程 | 2026-09-10 | v1（待核读） |
| `skill.md` | Skill（Agent 领域） | 学生 / 转行中 | 科普 + 工程 | 2026-09-10 | v1（待核读） |
| `concept-relationship.md` | 三概念关系 | 学生 / 转行中 | 科普 + 工程 | 2026-09-10 | v1（待核读） |

## 主题分类

### AI / Agent 体系
- `agent.md` —— Agent 三零件、控制循环、真假判断
- `skill.md` —— Skill 四大特征、目录结构、与 Prompt 区别
- `concept-relationship.md` —— 三概念关系 + Mermaid 图

### LLM 工程实践
- `llm-context.md` —— 上下文窗口、5 种优化技术、Lost-in-the-Middle

## 生成方式

每份资料均由 `concept-learning` Skill 驱动：
1. AI 通过 `WebSearch` 检索至少 3 个来源
2. AI 用 `WebFetch` 实际抓取每个 URL 验证可达
3. AI 按七段式起草
4. AI 自检（真假 / 结构 / 去 AI 痕迹 / 个人理解 4 项）
5. 人类作者（用户）做最终核读

详见根目录 `README.md` 末尾的"AI 与人工核查记录"。

## 维护说明

- 修订时只更新本文件"修订次数"列，并在对应 `.md` 文件末尾的"修订记录"表里追加条目
- 新增概念学习资料后，请在本文件追加一行
- 删除资料时，请同时删除对应行 + 在 git commit message 里说明

---

_最近更新：2026-09-10_
