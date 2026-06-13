# idea-bank-skills

> 把"读完一篇论文"变成"往自己的方法银行里存一笔"。

中文 | [English](#english)

---

## 中文

### 为什么做这个

这个 skill 主要用于**文献精读与文献积累**：给它一篇论文（PDF），它会把这篇论文的方法思路和流程拆解、模块化——整体设计思想、整体方法拆解、输入数据类型、输出数据类型，以及"哪些部分可以跨领域应用"，逐项总结清楚，并把这些内容生成 Word 文档导出到你指定的目录，方便长期保存和查阅。

更重要的是积累。每读一篇新论文，提炼出来的"可跨领域应用的方法模块"会追加/合并进同一份知识库——读得越多，这份知识库就越厚。这么做的目的是"厚积薄发"：学习不同领域、不同方法的论文，把里面的思路用到自己的领域上，写论文的时候有地方找idea，而不是每次都从零想。

### 这个 skill 做什么

给它一篇（或几篇）论文（PDF 路径、链接或正文），它会：

1. **还原设计思想**——不是照抄摘要，而是搞清楚作者当时是怎么想的：现有方法卡在哪、这篇论文的核心洞见是什么、这个洞见怎么落到具体设计上。
2. **拆解方法**——把 Method 部分整理成"按论文顺序、每一步在做什么、为什么需要这一步"的清单，挑 1-3 个最关键的公式讲直觉，而不是逐条罗列。
3. **梳理输入输出数据**——具体到数据形态（栅格/表格/矢量/点位/时序）、分辨率、预处理方式。这是判断"能不能迁移到我的数据上"的基础。
4. **跨领域迁移分析**——区分"领域无关的核心机制"和"领域特定、必须替换的实现细节"，给出"原方法 → 我的场景"的对应表和具体改造建议。
5. **输出精读笔记**——按统一模板生成，多篇论文时附加横向对比表。
6. **更新方法模块知识库**——这是最关键的一步。把第 2、4 步提炼出的"领域无关核心机制"，按去重/合并规则追加或合并进一个持续积累的知识库文件。

笔记和知识库默认输出为 `.docx`（也可以按需改成其他格式，见 `SKILL.md`）。

### 适合谁

- 想把论文方法"学透、能复用"，而不是看完就忘的人
- 经常跨领域读论文、希望把别的领域的思路用到自己研究上的人
- 平时多读多攒，写论文/想 idea 的时候有地方可以翻一翻的人

### 安装

PowerShell：

```powershell
git clone https://github.com/myzhao0114-del/idea-bank-skills.git "$HOME\.claude\skills\idea-bank-skills"
```

Bash：

```bash
git clone https://github.com/myzhao0114-del/idea-bank-skills.git "$HOME/.claude/skills/idea-bank-skills"
```

如果目录已存在，先删除旧版本或克隆到其他目标路径，然后重启 Claude Code。

### 怎么用

直接给 Claude Code 一篇论文（PDF 路径或正文），并提出诉求即可，例如：

```text
帮我精读一下这篇论文的方法，包括设计思想、用了什么方法、
需要什么样的输入数据、输出什么结果，以及怎么跨领域应用。
顺便更新一下我的方法模块知识库。
```

```text
这两篇论文的方法路线有什么区别？哪个更容易迁移到我的格网数据上？
```

知识库文件默认放在论文所在目录下，会随着每次精读不断累积。

### 仓库结构

```text
idea-bank-skills/
├── SKILL.md
├── README.md
├── references/
│   ├── note-template.md            单篇精读笔记模板
│   ├── cross-domain-checklist.md   跨领域迁移可行性检查清单
│   └── module-knowledge-base.md    方法模块知识库的条目格式与去重合并规则
└── scripts/
    └── md_to_docx.py                把笔记/知识库转换为 .docx
```

---

<a name="english"></a>

## English

### Why this exists

This skill is built for **deep-reading and accumulating research papers**. Give it a paper (PDF), and it breaks down the method's design and pipeline into modular pieces — overall design rationale, method breakdown, input data type, output data type, and the parts that can be applied across domains — summarizes each of them, and exports the result as a Word document to a directory you specify, so it's easy to keep and revisit.

The real point is accumulation. Every new paper you read gets checked against a single growing knowledge base, and its "this still holds in a different domain" modules get appended or merged into it — the more you read, the thicker that knowledge base gets. The goal is to let small efforts compound: by learning methods and ideas from different fields and applying them to your own, you write better papers and build up a steady reservoir of ideas to draw on.

### What it does

Give it one or more papers (PDF path, link, or text), and it will:

1. **Reconstruct the design rationale** — not the abstract, but the actual reasoning: what limitation of prior work the authors were targeting, what their core insight was, and how that insight maps to specific design choices.
2. **Deconstruct the method** — turn the Method section into an ordered, executable step list, and explain the intuition behind the 1-3 most important formulas.
3. **Map inputs and outputs** — down to data type (raster/tables/vectors/points/time series), resolution, and preprocessing — the basis for judging transferability.
4. **Cross-domain transfer analysis** — separate domain-agnostic core mechanisms from domain-specific implementation details, with a concrete "original method → your scenario" mapping.
5. **Output a reading note** per paper, plus a comparison table when reading multiple papers.
6. **Update a cumulative method-module knowledge base** — the most important step: append or merge the domain-agnostic mechanisms from steps 2 and 4 into a knowledge base file that keeps accumulating across every paper you read.

Notes and the knowledge base default to `.docx` (configurable — see `SKILL.md`).

### Who this is for

- Anyone who wants to actually internalize and reuse a paper's method, not just remember "it got SOTA"
- Researchers reading across domains, looking to bring ideas from one field into another
- Anyone building up a personal idea bank over time to draw on when writing papers

### Install

PowerShell:

```powershell
git clone https://github.com/myzhao0114-del/idea-bank-skills.git "$HOME\.claude\skills\idea-bank-skills"
```

Bash:

```bash
git clone https://github.com/myzhao0114-del/idea-bank-skills.git "$HOME/.claude/skills/idea-bank-skills"
```

If the directory already exists, remove the old copy or clone to a different path, then restart Claude Code.

### How to use

Give Claude Code a paper (PDF path or text) and state your goal, e.g.:

```text
Deep-read this paper's method: design rationale, technique, required
input data, produced outputs, and how to apply it to a different domain.
Also update my method-module knowledge base.
```

```text
Compare the method designs of these two papers — which one is easier
to transplant onto my grid-based dataset?
```

The knowledge base file lives alongside the papers by default and keeps growing with every paper you read.

### Repository structure

```text
idea-bank-skills/
├── SKILL.md
├── README.md
├── references/
│   ├── note-template.md            per-paper deep-read note template
│   ├── cross-domain-checklist.md   cross-domain transfer checklist
│   └── module-knowledge-base.md    module entry format and dedup/merge rules
└── scripts/
    └── md_to_docx.py                converts notes/knowledge base to .docx
```
