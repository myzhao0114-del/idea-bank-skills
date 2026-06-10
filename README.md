# paper-method-deconstruct

> 把论文当成"我是作者，要把这套方法重新做一遍"来读：拆解设计思想、方法流程、输入输出数据形态，并给出跨领域迁移方案。

中文 | [English](#english)

---

## 中文

### 这是什么

这是一个 Claude Code skill。日常读论文时，常见的痛点是：摘要看完了，但说不清楚——

- 作者为什么这么设计？这个设计解决了前人方法的什么问题？
- 方法到底是怎么一步步跑起来的？
- 它需要什么样的数据？是栅格影像、格网提取的表格、矢量、点位观测，还是时间序列？
- 它最终输出什么？是一张预测图、一组分类标签，还是一份指标表？
- 这套方法能不能用到我自己的数据/领域上？哪些部分能照搬，哪些必须改？

`paper-method-deconstruct` 就是为了系统性回答这些问题而设计的。它不产出"这篇论文做了什么、达到了 SOTA"这类摘要式总结，而是产出一份**可复现、可迁移**的方法拆解笔记。

### 工作流程

1. **确认范围**：单篇精读，还是多篇横向对比？是否需要结合用户自己的数据评估迁移可行性？
2. **通读全文**：定位 Method、Data、Experiments 等关键章节，重点看流程图和图注。
3. **还原设计思想**：重构作者的推理链——目标问题、现有方法的局限、核心洞见，以及这个洞见如何对应到具体的设计选择。
4. **拆解方法**：把 Method 整理成可执行的流程清单、核心模型/公式的直觉解释、消融实验给出的"哪些组件是核心"的线索。
5. **梳理输入输出**：具体到数据形态——空间/时间分辨率、数据来源、预处理方式；输出形态、评价指标、可复用的中间产物。
6. **跨领域迁移分析**：区分"领域无关的核心机制"与"必须替换的领域特定实现"，给出"原方法 → 用户场景"的对应表和具体改造建议。
7. **输出笔记**：按统一模板生成 Markdown 精读笔记；多篇论文时附加横向对比表。

### 使用方式

#### 1. 安装

PowerShell：

```powershell
git clone https://github.com/myzhao0114-del/paper-method-deconstruct.git "$HOME\.claude\skills\paper-method-deconstruct"
```

Bash：

```bash
git clone https://github.com/myzhao0114-del/paper-method-deconstruct.git "$HOME/.claude/skills/paper-method-deconstruct"
```

如果目录已存在，先删除旧版本或克隆到其他目标路径，然后重启 Claude Code。

#### 2. 安装后怎么用

直接给 Claude Code 一篇论文（PDF 路径或正文），并提出诉求即可，例如：

```text
帮我精读一下这篇论文的方法，包括设计思想、用了什么方法、
需要什么样的输入数据、输出什么结果，以及怎么跨领域应用。
```

```text
这两篇论文的方法路线有什么区别？哪个更容易迁移到我的格网数据上？
```

### 仓库结构

```text
paper-method-deconstruct/
├── SKILL.md
├── README.md
└── references/
    ├── note-template.md          单篇精读笔记模板
    └── cross-domain-checklist.md 跨领域迁移可行性检查清单
```

### 适合谁用

- 想把一篇论文的方法"学透、能复用"的研究生/科研人员
- 想评估某个方法能否迁移到自己数据/领域的人
- 不满足于"论文摘要"，想要可执行方法拆解的人

---

<a name="english"></a>

## English

### What this is

A Claude Code skill for reading a paper the way its author would — to figure out, step by step, how to redo the method yourself.

Common gaps after reading a paper's abstract:

- Why did the authors design it this way? What limitation of prior work does this design address?
- How does the method actually run, step by step?
- What kind of data does it need — raster imagery, grid-extracted tables, vector data, point observations, or time series?
- What does it output — a prediction map, classification labels, a metrics table?
- Can this method be transplanted to my own data/domain? What stays the same, and what must change?

`paper-method-deconstruct` produces a structured, **reproducible, transferable** method-deconstruction note instead of a generic "what the paper did / SOTA results" summary.

### Workflow

1. **Scope**: single deep-read, or comparative reading across multiple papers? Does the user have their own data to evaluate transfer feasibility?
2. **Full read**: locate Method, Data, and Experiments sections; pay special attention to pipeline figures and captions.
3. **Reconstruct the design rationale**: the target problem, the limitations of prior work, the core insight, and how that insight maps to specific design choices.
4. **Deconstruct the method**: turn the Method section into an executable pipeline, explain the intuition behind 1-3 key formulas, and use ablation results to flag which components are core vs. optional.
5. **Map inputs and outputs**: data type, spatial/temporal resolution, source, preprocessing; output format, evaluation metrics, reusable intermediate representations.
6. **Cross-domain transfer analysis**: separate domain-agnostic core mechanisms from domain-specific implementation details, and produce an "original method → target scenario" mapping table with concrete adaptation steps.
7. **Output**: a structured Markdown note per paper, plus a comparison table when multiple papers are involved.

### How to Use

#### 1. Install

PowerShell:

```powershell
git clone https://github.com/myzhao0114-del/paper-method-deconstruct.git "$HOME\.claude\skills\paper-method-deconstruct"
```

Bash:

```bash
git clone https://github.com/myzhao0114-del/paper-method-deconstruct.git "$HOME/.claude/skills/paper-method-deconstruct"
```

If the directory already exists, remove the old copy or clone to a different path, then restart Claude Code.

#### 2. After installation

Give Claude Code a paper (PDF path or text) and state your goal, e.g.:

```text
Deep-read this paper's method: design rationale, technique, required
input data, produced outputs, and how to apply it to a different domain.
```

```text
Compare the method designs of these two papers — which one is easier
to transplant onto my grid-based dataset?
```

### Repository Structure

```text
paper-method-deconstruct/
├── SKILL.md
├── README.md
└── references/
    ├── note-template.md          per-paper deep-read note template
    └── cross-domain-checklist.md cross-domain transfer checklist
```

### Who this is for

- Graduate students/researchers who want to truly understand and reuse a paper's method
- Anyone evaluating whether a method can be transplanted to their own data/domain
- Readers who want an executable method breakdown, not just an abstract summary
