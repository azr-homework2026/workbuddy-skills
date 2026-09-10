# Skill（AI Agent 领域）—— 学习包

> 学习者背景：学生 / 转行中
> 学习深度：科普 + 工程实践
> 生成日期：2026-09-10
> 参考来源核查日期：2026-09-10

---

## 1. 学习目标

完成本资料后，你应当能够：

1. **能用自己的话解释** 在 AI Agent 语境下，"Skill" 是什么以及和 Prompt 的区别
2. **能列出** Anthropic 官方定义的 Skill 四大特征（composable / portable / efficient / powerful）
3. **能描述** 一个标准 Skill 的目录结构（SKILL.md + 可选 scripts/ + references/）
4. **能写出** 一个最简 SKILL.md 的 YAML frontmatter（至少含 name + description）
5. **能判断** 何时把工作流沉淀成 Skill（而不是每次重新写 prompt）

---

## 2. 核心问题

1. **是什么**：Skill = Prompt 吗？Skill = System Prompt 吗？Skill = 预设工具吗？
2. **为什么**：Anthropic 在 2025 年 10 月推出 Skill，是想解决 AI 应用的哪个具体痛点？
3. **怎么做**：怎样从一段"用得顺手的 prompt"沉淀成一个可复用的 Skill？
4. **何时不用**：什么情况下**不要**用 Skill（用 prompt 就够了）？
5. **怎么判断**：Skill 写得好不好？有什么最低标准？

---

## 3. 结构化解释

### 3.1 前置知识

- 了解 LLM 的 system prompt / user prompt 区别
- 了解 Agent 的工具调用（Function Calling / Tool Use）机制
- 了解"工作流"（Workflow）vs"智能体"（Agent）的区别（见 `agent.md` §5.1）

### 3.2 核心定义

> **Skill（Anthropic 定义）= 一个包含指令、脚本和资源的文件夹，Claude 按需加载，用来提升在特定任务上的表现** [1]。

把它想成"**给 AI 的标准化入职培训手册**"：
- 不是一次性的 prompt 字符串
- 是一个**有结构的目录**（SKILL.md 是入口，可选 scripts/、references/）
- **按需加载** —— 任务相关才加载，不相关就跳过（节省 token、保持速度）[1]
- **跨产品复用** —— 同一个 Skill 可以在 Claude Apps、Claude Code、API 里用同一份 [1]

### 3.3 关键机制：Skill 的四大特征

Anthropic 官方原文 [1]：

| 特征 | 英文 | 含义 | 工程价值 |
|------|------|------|----------|
| 可组合 | **Composable** | 多个 Skill 可叠加，Claude 自动识别需要哪些 | 一次写好，多场景用 |
| 可移植 | **Portable** | 同一份 Skill 在 Claude Apps / Code / API 都跑 | 写一次，到处用 |
| 高效 | **Efficient** | 只加载需要的部分 | 不浪费 token 预算 |
| 强大 | **Powerful** | 可包含可执行代码 | 编程比 prompt 更可靠的场景直接用代码 |

### 3.4 形式化：标准 Skill 的目录结构

来自 Anthropic 官方对 `skill-creator` Skill 的描述 [1]，以及 Claude Code 的目录约定：

```
<my-skill>/
├── SKILL.md           ← 入口：YAML frontmatter + 详细说明（必需）
├── scripts/           ← 可执行脚本（可选）
│   └── helper.py
└── references/        ← 参考资料、模板（可选）
    └── template.md
```

**SKILL.md 的最小 frontmatter**（[1][2] 一致）：

```yaml
---
name: my-skill                  # Skill 名称（必填）
description: 何时用这个 Skill   # 一句话说明，供模型判断何时加载（必填）
---
```

> **关键洞见**：`description` 字段**就是** Skill 的"触发器"。LLM 看到任务时，会根据 description 决定要不要加载这个 Skill。所以 description 写得越精准，Skill 越"知道自己什么时候该出现"。

### 3.5 我的理解（原创类比）

> 把 Skill 想成**手机里的"快捷指令"App**：
> - 你不用每次都手动打开天气 App 查天气，而是设一个"出门时自动播报天气"的快捷指令
> - 触发条件 = Skill 的 `description`
> - 步骤 = SKILL.md 里的"工作流"段
> - 配套资源 = `scripts/` 和 `references/`
> - 不同手机都能用同一个快捷指令 = Portable

> 反过来，**Prompt 是"你跟 Siri 说的话"**，每次都得重新组织语言；**Skill 是"你事先写好的快捷指令"**，触发一次就自动跑完整套动作。

---

## 4. 应用案例

### 案例 1：组织级 Excel 报表生成（正面，Anthropic 官方示例 [1]）

- **场景**：Rakuten 财务团队每月要把多个 Excel 数据源汇总成标准化报表
- **之前**：用通用 LLM 写公式，每次格式都跑偏
- **引入 Skill 后**：
  - 把"公司的报表标准"沉淀成 `financial-reporting` Skill
  - Skill 包含 SKILL.md（"何时用 / 步骤 / 输出格式"）+ scripts/（读 Excel 的标准脚本）
  - Claude 加载这个 Skill 后，每次生成的报表都符合公司规范
- **结果**：原本 1 天的工作，缩短到 1 小时 [1]
- **意义**：把"个人经验"沉淀成"组织级可复用资产"

### 案例 2（反面 / 踩坑）：把"一次性的提示词"包装成 Skill

- **症状**：有人写了一个 Skill，SKILL.md 长达 200 行，**把任务的所有细节、所有 case、所有边界条件都塞在 description 里**
- **问题**：
  - LLM 每次都会"看到"这个 Skill（因为 description 太宽泛），但其实 80% 的任务用不到
  - Token 浪费 —— description 越长，每次推理消耗越多
  - 可维护性差 —— 改一个 case 要读整篇
- **正确做法**：
  - description **精准描述触发条件**（"当用户上传 Excel 并要求生成报表时"），不要写"通用助手"
  - 详细步骤放**正文**，不放 frontmatter
  - 一个 Skill 只做一类事（财务归财务、PPT 归 PPT），不要做大杂烩
- **来源**：Anthropic 强调"Claude will only access a skill when it's relevant to the task at hand" —— 这就要求 description 必须**精准**才能实现"按需加载" [1]

---

## 5. 概念辨析

### 5.1 Skill vs Prompt vs System Prompt vs Tool

| 概念 | 范围 | 持久性 | 触发方式 | 适用 |
|------|------|--------|----------|------|
| **Prompt** | 单次对话 | 不持久 | 用户输入 | 一次性任务 |
| **System Prompt** | 单次会话 | 不持久（除非平台存） | 每次会话开头 | 设定角色 / 行为基线 |
| **Tool** | LLM 可调用的 API | 持久 | LLM 决策 | 读文件、调 API、跑代码 |
| **Skill** | 跨会话、跨产品 | 持久 | 任务匹配 | 标准化、可复用工作流 |

> 关键区分：**Tool 是 LLM 用的"手"，Skill 是 LLM 的"操作手册"**。一个 Skill 内部往往就规定了"何时调用哪个 Tool、按什么顺序"。

### 5.2 Skill vs MCP（Model Context Protocol）

| 维度 | Skill | MCP |
|------|-------|-----|
| 是什么 | 工作流 / 操作手册 | 工具调用的标准协议 |
| 由谁定义 | 人写（标准化文档） | 协议 + 实现 |
| 解决了什么 | "LLM 不知道怎么做复杂任务" | "LLM 怎么发现 / 调用外部工具" |
| 出现时间 | Anthropic 2025-10 推出 [1][2] | Anthropic 2024 末推出 [2] |
| 关系 | Skill 可以**使用** MCP 暴露的工具 | MCP 提供**基础设施**，Skill 在上层 |

> 简单说：**MCP 让 LLM 能"接上"工具，Skill 让 LLM 知道"什么时候用哪个工具、怎么组合"**。

### 5.3 好 Skill vs 坏 Skill（实操判断表）

| 检验项 | 好 Skill | 坏 Skill |
|--------|---------|---------|
| description 精准？ | ✅（明确触发条件） | ❌（"通用助手"） |
| 步骤可执行？ | ✅（可被 LLM 一步步跟做） | ❌（"按情况处理"等模糊词） |
| 有可核查输出？ | ✅（有明确格式 / 例子） | ❌（"输出合理结果"） |
| 长度合理？ | ✅（SKILL.md 100–500 行） | ❌（几行 / 几千行） |
| 单一职责？ | ✅（一个 Skill 做一类事） | ❌（什么都往里塞） |

---

## 6. 自测题

<details>
<summary><strong>题 1（理解）</strong></summary>

**问题**：一句话区分"Skill"和"Prompt"。

**答案**：Prompt 是一次性输入，Skill 是跨会话、跨产品、可复用的标准化工作流。

**解析**：核心差别在**持久性**和**结构化**。Skill 是"提前写好、按需加载"，Prompt 是"每次重新组织"。
</details>

<details>
<summary><strong>题 2（理解）</strong></summary>

**问题**：Anthropic 定义的 Skill 四大特征是什么？

**答案**：Composable（可组合）/ Portable（可移植）/ Efficient（高效）/ Powerful（强大）[1]。

**解析**：这四个词是记忆口诀 ——"CPEP"。每个词背后都有具体工程含义（见 §3.3）。
</details>

<details>
<summary><strong>题 3（应用）</strong></summary>

**问题**：一个 Skill 的 SKILL.md 最少要有哪两个 YAML 字段？

**答案**：`name` 和 `description` [1]。

**解析**：这是最低要求。`description` 决定 LLM 何时加载 Skill，所以即便字段少，`description` 也要写精准。
</details>

<details>
<summary><strong>题 4（分析）</strong></summary>

**问题**：某 Skill 的 description 写"我是一个通用 AI 助手"。**这有什么问题？**

**答案**：description 太宽泛，会导致 LLM **每次都加载**这个 Skill，浪费 token，且"通用助手"反而让 LLM 不知道具体该怎么做 [1] 强调"only access a skill when it's relevant"。

**解析**：description 是 Skill 的"触发器"，写得越精准，触发越准。这是一个看似细节但影响巨大的设计点。
</details>

<details>
<summary><strong>题 5（评价）</strong></summary>

**问题**：有人说"以后所有 prompt 都会被 Skill 取代"。**你怎么评价？**

**答案**（三个反驳点）：
1. **场景差异**：一次性 / 临时探索性任务用 prompt 更快，写 Skill 是过度工程
2. **维护成本**：每个 Skill 都要写 YAML、目录、维护，反而对小任务是负担
3. **Skill 内部也用 prompt**：Skill 的 SKILL.md 本质上就是结构化 prompt —— 两者不是替代关系，是**不同抽象层级**
更准确的说法是："**反复用得顺的 prompt** 会被沉淀成 Skill"。

**解析**：这是考察"对 Skill 抽象层级的理解"。Skill 解决的是"标准化复用"，不是"替代一切"。
</details>

<details>
<summary><strong>题 6（创造）</strong></summary>

**问题**：你发现自己每次写"帮我把这段 Python 重构得更可读"都要重新组织 prompt。**请设计一个 Skill 的 description（一句）和 SKILL.md 的目录结构。**

**答案要点**（开放题）：
- **description** 示例：
  > "当用户提供一段 Python 代码并要求'重构 / 提高可读性 / 清理'时使用此 Skill。它会按 PEP 8 风格 + 单一职责原则审查代码并给出 diff。"
- **目录结构**：
  ```
  python-refactor/
  ├── SKILL.md
  └── references/
      └── pep8-cheatsheet.md
  ```

**解析**：这是个 mini 设计题。考察"能不能把个人经验转化为结构化 Skill"。关键是 description 要精准，不是宽泛。
</details>

---

## 7. 参考来源

> 所有 URL 在 2026-09-10 实际访问过并验证可达。

| # | 来源 | URL | 检索日期 | 在正文中支撑的事实 |
|---|------|-----|----------|-------------------|
| [1] | Anthropic, "Introducing Agent Skills" | https://www.anthropic.com/research/skills | 2026-09-10 | §3.2 定义、§3.3 四大特征、§3.4 目录结构、§4 两个案例、§5.1/5.2 区分、§6 全部题 |
| [2] | Claude Blog, "Skills for organizations, partners, the ecosystem"（Anthropic 官方） | https://claude.com/blog/organization-skills-and-directory | 2026-09-10 | §3.4 SKILL.md 字段、§5.2 Skill vs MCP 区分 |

> 备注：本主题**几乎所有内容**都来自 Anthropic 官方，因为 Skill 是 Anthropic 2025-10 才正式发布的产品概念 [2]，没有更早的独立学术文献。这是正常的"产品定义 → 文档 → 实践"早期阶段。

---

## 修订记录

| 日期 | 修订人 | 修订内容 |
|------|--------|----------|
| 2026-09-10 | 小豆（AI 起草） | 初版。AI 起草七段式文本 + 原创类比（"手机快捷指令"类比） + 原创对比表。**特别注意**：因 Skill 是 2025-10 才发布的产品概念，几乎所有来源都是 Anthropic 官方；这导致"来源多样性"指标偏低（只有 1 个一手来源），但这是产品现实，不是引用造假 |
| _（待补）_ | _（用户）_ | _（待用户核读后追加）_ |
