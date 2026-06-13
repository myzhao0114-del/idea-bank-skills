# idea-bank-skills

> 把"读完一篇论文"变成"往自己的方法银行里存一笔"。

中文 | [English](#english)

---

## 中文

### 为什么做这个

读论文的时候经常是这样：一篇文章看完，心里觉得"这个思路挺巧妙"，但读完就翻篇了。等到下次写论文、卡在某个设计上想不出办法的时候，完全想不起来"我好像在哪篇论文里见过类似的处理方式"，只能重新去找、重新去想。读得越多，这种"读过但留不下"的感觉反而越强——脑子里堆了一堆论文的印象，却没法直接拿来用。

更可惜的是跨领域的部分。很多方法的核心机制其实是领域无关的——比如"用一个生成式先验约束生成网络的局部统计量"这种思路，气象预报里能用，城市内涝预测里也能用，本质上是同一件事，只是换了个名字、换了个数据集。但如果读的时候没有把这层"本质"抽出来，下次在另一个领域遇到一篇用了同样思路的论文，大概率认不出来，更别说反过来主动想到"我现在这个问题，是不是可以套用我以前读过的某个机制"。

这个 skill 想做的事情很朴素：**每读一篇论文，不止产出一份精读笔记，还顺手把里面"换个数据集/换个领域依然成立"的方法思路提炼成一个个模块，存进一个会越攒越厚的知识库里**。读得越多，这个库就越有价值——下次精读新论文时，会自动去库里比对"这个机制是不是和之前某个模块本质相同"，相同就合并记录（多了一个"这个思路在哪些论文里都出现过"的证据），不同就新建条目。时间长了，这就是你自己的"idea 银行"：写论文卡住、想找idea的时候，翻一翻这个库，看看有没有哪个攒下来的模块能搬到当前的问题上——也就是"厚积薄发"。

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

Reading papers often goes like this: you finish one, think "that's a clever idea", and then move on. Months later, stuck on a design problem in your own work, you have a vague feeling that you've seen something similar before — but you can't remember where, so you end up reinventing it from scratch. The more you read, the worse this gets: a pile of half-remembered papers that you can't actually draw on.

The cross-domain case is even more frustrating. Many core mechanisms are genuinely domain-agnostic — e.g. "use a coarse generative prior to condition the local statistics of a generation network" shows up in weather nowcasting, urban flood modeling, and plenty of other places, under completely different names. If you don't abstract that out when you first read it, you won't recognize it the next time it shows up in a different field — let alone think to apply it proactively to your own problem.

What this skill does is simple: **every time you deep-read a paper, in addition to producing a reading note, it also extracts the "this idea still holds if you swap the dataset or domain" parts into modules, and appends them to a knowledge base that keeps growing**. The more you read, the more valuable that knowledge base becomes — each new paper gets checked against existing modules ("is this the same core mechanism as something I've already logged?"), merging when it matches and creating a new entry when it doesn't. Over time this becomes your own idea bank: when you're stuck writing a paper or looking for an idea, you can browse it and see what's transferable to your current problem.

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
