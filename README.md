# workbuddy-skills

> 我的 AI Agent / LLM / Skill 学习仓库。

## 仓库用途

这是一个**个人学习 + Skill 沉淀**仓库，做三件事：

1. **保存** 自己写的 WorkBuddy Skill（可被 WorkBuddy 自动加载的工作流定义）
2. **保存** 用 `concept-learning` Skill 产出的结构化概念学习资料
3. **示范** "AI 起草 + 人工核查"的工作流：每份资料都明确标注 AI 做了什么、人类需要核读什么

## 仓库结构

```
workbuddy-skills/
├── .workbuddy/
│   └── skills/
│       ├── learning-skill/                # ⚠️ 占位 Skill（仅目录结构示例，非可用 Skill）
│       │   └── SKILL.md
│       └── concept-learning/              # ✅ 项目级 Skill（核心）：七段式概念学习包生成器
│           ├── SKILL.md                   # 主入口（六要素：场景/输入/步骤/输出/来源/自检）
│           ├── README.md
│           └── references/
│               ├── template.md            # 七段式输出模板
│               ├── bloom-taxonomy.md      # 学习目标 & 自测题动词速查
│               ├── deai-checklist.md      # 去 AI 痕迹核查清单
│               ├── source-types.md        # 不同学科可信来源
│               └── INDEX-template.md      # learning-materials 索引模板
├── learning-materials/                    # 学习资料（AI 起草，待人工核读）
│   ├── INDEX.md                           # 资料索引
│   ├── agent.md                           # AI Agent 学习包
│   ├── llm-context.md                     # LLM 上下文窗口学习包
│   ├── skill.md                           # Skill 学习包
│   └── concept-relationship.md            # 三概念关系（含 Mermaid）
├── README.md                              # 本文件
└── .gitignore
```

## Skill 存放路径

所有 WorkBuddy Skill 都放在：

```
.workbuddy/skills/<skill-name>/SKILL.md
```

约定：
- `<skill-name>` 用英文小写 + `-` 分隔
- `SKILL.md` 是必需入口文件
- 可选子目录：`scripts/`（可执行脚本）、`references/`（参考资料、模板）
- `SKILL.md` 顶部必须有 YAML frontmatter，至少含 `name` 和 `description`

本仓库现有 Skill：

| Skill 名 | 状态 | 作用 | 入口 |
|---------|------|------|------|
| **`concept-learning`** | ✅ **项目级 Skill（核心）** | 七段式概念学习包生成器 | `.workbuddy/skills/concept-learning/SKILL.md` |
| `learning-skill` | 🟡 **占位 / 模板** | 仓库初始化时建的最简示例，**不用于实际工作流** | `.workbuddy/skills/learning-skill/SKILL.md` |

> 📌 **项目级 Skill 指 `concept-learning`**。`learning-skill` 是仓库创建当天放进来的最小占位文件，仅用于演示 `.workbuddy/skills/<name>/SKILL.md` 的目录结构，**不是可用的工作流 Skill**。后续若新增 Skill，请按 `concept-learning` 的六要素结构（适用场景 / 输入信息 / 生成步骤 / 输出结构 / 资料来源要求 / 自检要求）来写。

## 如何在 WorkBuddy 中调用

### 方式 1：直接用语言触发（推荐）

直接告诉 WorkBuddy 你想做什么。例如：

> "用 concept-learning Skill 帮我做一份 **Transformer 架构** 的学习资料，我是中级工程师，要工程实践深度。"

WorkBuddy 会加载 `.workbuddy/skills/concept-learning/SKILL.md` 并按其七步流程跑。

### 方式 2：把仓库克隆到 WorkBuddy 工作区

```bash
cd /path/to/workbuddy/workspace
git clone https://github.com/azr-homework2026/workbuddy-skills.git
```

WorkBuddy 会自动扫描工作区下的 `.workbuddy/skills/`，把每个 Skill 注册到可加载列表。

### 方式 3：在 WorkBuddy 提示词里显式引用

> "请按 `.workbuddy/skills/concept-learning/SKILL.md` 的七段式流程，给 X 概念做一份学习资料。"

### ⚙️ Skill 加载机制（重要）

WorkBuddy 自动扫描的 Skill 目录是 **WorkBuddy 工作区根目录的 `.workbuddy/skills/`**，**不**是仓库子目录里的 `.workbuddy/skills/`。

| 位置 | 是否被 WorkBuddy 自动加载 | 用途 |
|------|------------------------|------|
| `workbuddy-skills/.workbuddy/skills/concept-learning/` | ❌（在仓库子目录里） | 仓库内版本控制 |
| `<workbuddy 工作区根>/.workbuddy/skills/concept-learning/` | ✅（WorkBuddy 自动扫描） | WorkBuddy 运行时加载 |

为了让本仓库的 Skill 在 WorkBuddy 里**真正可用**，本项目还把这个 Skill 复制到了 WorkBuddy 工作区根目录：

```bash
# 等价命令（已执行）
cp -r workbuddy-skills/.workbuddy/skills/concept-learning \
      <workbuddy 工作区>/.workbuddy/skills/concept-learning
```

> 之后 WorkBuddy 启动时会自动加载它，会话里直接说"用 concept-learning 帮我做 XXX"即可。

## 已生成的学习资料

详见 [`learning-materials/INDEX.md`](./learning-materials/INDEX.md)。当前包含：

| 文件 | 主题 | 状态 |
|------|------|------|
| `learning-materials/agent.md` | AI Agent | v1（AI 起草 + 待用户核读） |
| `learning-materials/llm-context.md` | LLM 上下文窗口 | v1（AI 起草 + 待用户核读） |
| `learning-materials/skill.md` | Skill（Agent 领域） | v1（AI 起草 + 待用户核读） |
| `learning-materials/concept-relationship.md` | 三概念关系 | v1（AI 起草 + 待用户核读） |

## AI 与人工核查记录

> 本节是**诚信声明**：本仓库内容由 AI（小豆，WorkBuddy 内置助手）起草，作者（`azr-homework2026`）负责核读、修订和最终采纳。

### AI（我）做了什么

对每一份学习资料和 Skill，AI 负责：

1. **检索**：用 `WebSearch` 检索 ≥ 3 个候选来源（Wikipedia / 官方文档 / 学术或权威）
2. **核查**：用 `WebFetch` 实际抓取每个 URL，**只引用验证可达的来源**
3. **起草**：按 `concept-learning` Skill 的七段式写出初稿
4. **自检**：跑真假 / 结构 / 去 AI 痕迹 / 个人理解 4 项检查
5. **诚实标注**：在每份资料末尾的"修订记录"区写明"AI 起草 + 待用户核读"

### 人类作者（你）需要核查 / 修改什么

按"重要程度从高到低"：

| 优先级 | 核查项 | 怎么核 |
|--------|--------|--------|
| 🔴 P0 | **每条参考 URL 的真实性** | 点开每条 `[n]`，确认页面真的存在、内容真的支撑正文 |
| 🔴 P0 | **个人解释的准确性** | `agent.md` §3.3 "实习生"类比、`llm-context.md` §3.3 "图书管理员桌面"类比 —— 是不是你同意的类比？ |
| 🟡 P1 | **原创对比表的内容** | `agent.md` §5 / `llm-context.md` §5 / `skill.md` §5 —— 对比维度是否合理、是否漏了关键区分 |
| 🟡 P1 | **自测题答案的正确性** | `agent.md` §6 / `llm-context.md` §6 / `skill.md` §6 —— AI 写答案容易"自信地错" |
| 🟢 P2 | **措辞 / 个人风格** | 把 AI 的口吻改写成你自己说话的样子 |
| 🟢 P2 | **"我的理解"类比** | §3.3 / §3.5 中的原创类比 —— 是不是你想用的类比？不喜欢就换 |

### 哪些内容**没有**经过 AI 核查（必须人工补）

- **Wikipedia 链接**：`agent.md` §7 [2] 引用了 Wikipedia，但本次沙箱网络下 HTTPS 不可达（curl 返回 000），未做正文级引用。**Russell & Norvig Agent 定义是与 [1][3] 交叉验证过的**，但请用户再独立核验。
- **任何标注为"AI 起草"的内容**：每份资料末尾的"修订记录"区都明确写了"AI 起草 + 待用户核读"。

### 修订流程

1. 用户核读 → 在文件末尾"修订记录"区追加条目（注明日期 + 修订人 + 修订内容）
2. 用户在 `learning-materials/INDEX.md` 表格里更新"修订"列
3. 用户自己 `git commit + push`（或让 WorkBuddy 协助）

## 安全

- `.gitignore` 已排除常见敏感文件（`.env`、`.pem`、`*.key`、凭据等）
- 本仓库的 GitHub PAT **不**保存到任何文件（详见各次提交的 commit message 与 `git log`）
- 提交前请确认没有误把 `credentials.json` 之类的文件 `git add` 进去

## 在线地址

- 仓库主页：https://github.com/azr-homework2026/workbuddy-skills
- concept-learning Skill：https://github.com/azr-homework2026/workbuddy-skills/tree/main/.workbuddy/skills/concept-learning

## 快速开始

```bash
# 克隆
git clone https://github.com/azr-homework2026/workbuddy-skills.git
cd workbuddy-skills

# 查看 Skill
cat .workbuddy/skills/concept-learning/SKILL.md

# 看学习资料
ls learning-materials/
```

## 修订记录

| 日期 | 修订人 | 修订内容 |
|------|--------|----------|
| 2026-09-10 | 小豆（AI 起草） | 初版。包含仓库用途、Skill 路径、调用方式、已生成资料清单、AI 与人工核查记录 |
| _（待补）_ | _（用户）_ | _（待用户核读后追加）_ |
