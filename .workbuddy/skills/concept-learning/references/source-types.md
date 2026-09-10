# 不同学科的可信来源类型

> 不要把所有"看起来权威的网站"都当来源。下面按学科列出**默认应当优先**的来源类型。

## 一、共识

无论什么学科，下列来源**优先级最高**：

- 该领域的**官方文档 / RFC / 标准**（如 IEEE 802.11、Python PEP、Go spec）
- 该领域**主流教材**（被多门大学课程使用的书）
- 该领域**综述论文**（survey paper）
- **维基百科**作为起点，但不可作为唯一来源

下列来源**仅作辅助或不使用**：

- Medium / 个人博客（除非作者是该领域公认的专家）
- 知乎 / CSDN（技术问题可参考，但不可作为概念定义来源）
- 论坛回复（Stack Overflow 可用于"这样做行不行"，不用于"XXX 是什么"）
- AI 自己生成的解释（**永远不是来源**）

## 二、计算机科学

| 类别 | 推荐来源 |
|------|----------|
| 语言/框架 | python.org、golang.org、rust-lang.org、kubernetes.io |
| 论文 | arXiv.org、ACM Digital Library、IEEE Xplore、USENIX |
| 标准 | IETF RFC、ISO、W3C |
| 算法/数据结构 | CLRS《算法导论》、leetcode 题解（仅作练习） |
| 系统 | OSDI/SOSP/NSDI 论文 |
| AI/ML | paperswithcode.com、distill.pub、huggingface docs |

## 三、数学

| 类别 | 推荐来源 |
|------|----------|
| 入门教材 | Strang《Linear Algebra》、Rudin《Principles of Mathematical Analysis》 |
| 在线 | 3Blue1Brown（直观理解）、Wolfram MathWorld（查定义） |
| 论文 | arXiv math.* |
| 百科 | Wikipedia + Encyclopedia of Mathematics |

## 四、物理 / 工程

| 类别 | 推荐来源 |
|------|----------|
| 教科书 | MIT OCW、费曼物理学讲义 |
| 期刊 | Physical Review、Nature Physics |
| 标准 | NIST、ISO |

## 五、生物 / 医学

| 类别 | 推荐来源 |
|------|----------|
| 论文 | PubMed、bioRxiv |
| 数据库 | UniProt、NCBI Gene、Ensembl |
| 临床 | UpToDate、Cochrane Library |
| 百科 | Wikipedia + Britannica |

## 六、社会 / 经济

| 类别 | 推荐来源 |
|------|----------|
| 数据 | World Bank、IMF、OECD、各国统计局 |
| 论文 | NBER、JSTOR、SSRN |
| 主流期刊 | AER、QJE、JPE |

## 七、哲学 / 人文

| 类别 | 推荐来源 |
|------|----------|
| 经典 | Stanford Encyclopedia of Philosophy、Internet Encyclopedia of Philosophy |
| 原始文献 | 古登堡计划、标准引用（Beebek、Chicago） |
| 综述 | 期刊综述、Handbook |

## 检索时的"红旗"清单（命中即放弃）

- [ ] URL 中带 `?utm_source=` 且没有原始域名 → 不是第一手来源
- [ ] 维基百科条目被标注为 "this article may be unbalanced" → 找替代
- [ ] 来源是某个 AI 工具的官网（"由 ChatGPT 生成"） → 不算来源
- [ ] 来源日期 < 2020 且涉及快速演进的领域（AI、Web）→ 可能过时
- [ ] 来源是 PDF 但未提供作者、年份 → 不可信

## 引用格式建议

学习资料中推荐使用**数字编号 + 表格**：

```
[1] Vaswani et al. (2017)《Attention Is All You Need》arXiv:1706.03762
[2] python.org《Lists - Python 3.13 documentation》
```

文末给出对应表格，附"检索日期"。

## 参考来源

| # | 来源 | URL | 检索日期 |
|---|------|-----|----------|
| [1] | Wikipedia: Wikipedia:Reliable sources（来源可靠性政策） | https://en.wikipedia.org/wiki/Wikipedia:Reliable_sources | 2026-09-10 |
| [2] | Wikipedia: Identifying reliable sources (science) | https://en.wikipedia.org/wiki/Wikipedia:Identifying_reliable_sources_(science) | 2026-09-10 |
