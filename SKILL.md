---
name: course-report
description: |
  帮助生成课程作业报告的LaTeX代码。每当用户提到"写报告"、"课程作业"、"期末报告"、"作业要求"、"帮我写"配合课程内容，或上传了作业要求文档时，必须使用本skill。即使用户只说"帮我写一下这个作业"也应触发。输出可在Overleaf直接编译的完整.tex文件，支持双栏学术期刊或单栏SYSUReport两种模板。
---

# 课程报告生成 Skill

## 你是谁

你是用户的课程报告助手。你的任务是：**根据教师提供的作业要求，生成符合用户固定LaTeX模板风格的完整报告**。

> **使用前配置**：请在下方模板中将 `[姓名]`、`[学号]`、`[学院]`、`[专业]`、`[邮箱]` 替换为你自己的信息。

---

## 第零步：开始前必须先问清楚

在读完作业要求、动笔规划大纲之前，如果以下任何一项不明确，**先集中问用户一次**，而不是直接开写：

1. **模板类型**：双栏学术期刊风格，还是单栏SYSUReport风格（有封面、目录、摘要页）？
   - 一般判断：论文/调研类 → 双栏；实验/编程类 → 单栏；教师有指定 → 遵循指定
2. **报告类型**：实验类（有实验步骤、代码、结果截图）还是论文类（理论分析、综述调研）？
3. **图片策略**：希望几张图？计划自己截图 / 从文献取图 / 让AI生成？
4. **文献年份要求**：有特殊限制吗？（默认规则见下方）

如果这些信息已经从作业要求文档或用户说明中明确可以推断，则不必追问，直接推进。

---

## 使用流程

### 第一步：读取作业要求

用户会上传作业要求文档（PDF/Word/图片/文字粘贴均可）。仔细阅读并提取：

- **报告主题**
- **章节结构要求**（教师是否规定了必须包含哪些章节）
- **字数/篇幅要求**
- **提交格式**（有无教师专属模板）
- **截止日期**（如有）
- **评分标准**（如有，影响各部分侧重）

### 第二步：规划报告结构

输出一个简短的**内容大纲**（不超过15行），包括：
- 拟定标题
- 各章节标题及核心内容一句话概述
- 图片规划（数量、每张图的来源类型：文献图/AI生图/用户截图）
- 参考文献数量估计

**除非用户明确说"直接写"，否则先确认大纲**。

### 第三步：生成LaTeX代码

根据报告类型选择对应模板（见下方）。

---

## 模板选择

### 模板A：双栏学术期刊（论文/调研类默认）

适用场景：综述、调研报告、理论分析类作业，偏学术论文风格。

```latex
\documentclass{article}
\usepackage{graphicx}
\usepackage{ctex}
\usepackage{authblk}
\usepackage{abstract}
\usepackage{titling}
\usepackage{multicol}
\usepackage{geometry}
\usepackage{gbt7714}
\usepackage{amsmath}
\usepackage{fontspec}
\usepackage{xcolor}
\usepackage{capt-of}
\usepackage{titlesec}
\usepackage{caption}
\usepackage{threeparttablex}
\usepackage{booktabs}
\usepackage{array}
\usepackage{longtable}
\usepackage{fancyhdr}
\usepackage{setspace}
\usepackage{hologo}

% 颜色
\definecolor{mycolor}{rgb}{0,0.28,0.6}

% 字体
\setmainfont{Times New Roman}
\newcommand{\customsectionformat}{\zihao{4}\songti}
\newcommand{\customsubsectionformat}{\zihao{5}\heiti}
\newcommand{\customsubsubsectionformat}{\zihao{5}\kaishu}

% 章节标题样式
\titleformat{\section}{\normalfont\customsectionformat\color{mycolor}}{\thesection}{1em}{}
\titleformat{\subsection}{\normalfont\customsubsectionformat\color{mycolor}}{\thesubsection}{1em}{}
\titleformat{\subsubsection}[runin]{\normalfont\customsubsubsectionformat\color{mycolor}}{\thesubsubsection}{1em}{}

% 页面边距
\geometry{headsep=0.5cm}
\geometry{left=14mm,right=14mm,top=1mm,bottom=21mm}

% 页眉页脚
\pagestyle{fancy}
\fancyhf{}
\chead{{\zihao{-5}\songti [课程名]}}
\rhead{\thepage}
\renewcommand{\headrulewidth}{0.5pt}
\fancypagestyle{plain}{\pagestyle{fancy}}

% 首页特殊页眉页脚
\fancypagestyle{mystyle}{
    \chead{{\zihao{-5}\songti 中山大学学报（自然科学版）}\par\noindent ACTA \; SCIENTIARUM \; NATURALIUM \; UNIVERSITI \; SUNYATSENI}
    \rhead{\thepage}
    \lfoot{\zihao{-5} \heiti 作者简介:\songti [姓名]，男；\heiti 研究方向：\songti [研究方向关键词]；E-mail：[邮箱]}
    \renewcommand{\headrulewidth}{0.5pt}
    \renewcommand{\footrulewidth}{0.5pt}
}

% 标题格式
\makeatletter
\def\@maketitle{%
  \newpage\null\vskip 0.5em%
  \begin{center}%
    {\LARGE \@title \par}%
    \vskip .5em%
    {\large \linespread{1.3}\@author \par}%
    \vskip 1em%
    {\large }%
  \end{center}%
  \par\vskip 1.5em}
\makeatother

\ctexset{bibname=\zihao{5} 参考文献：}

\begin{document}

\title{\zihao{2}\songti \color{mycolor}{\textbf{[报告标题]}}}
\author{\zihao{4}\kaishu\color{mycolor} {[姓名]}}
\affil{\zihao{5}\kaishu [学院全称]，[省份] \ [城市邮编]}
\date{}
\maketitle
\thispagestyle{mystyle}
\ziju{0.085}

\noindent
\zihao{-5}\heiti {\textbf{摘 \ \  要}}：\zihao{-5}\songti{[摘要内容，150-300字]}

\noindent
\zihao{-5}\heiti{\textbf{关键词}}:\zihao{-5}\songti{[关键词1]；[关键词2]；[关键词3]；[关键词4]；[关键词5]}

\setlength\columnsep{0.5cm}
\begin{multicols}{2}
\zihao{5}\songti

% ===== 正文章节 =====
\section{[第一章标题]}
[正文内容...]

\end{multicols}

\bibliographystyle{gbt7714-numerical}
\begin{multicols}{2}
\nocite{*}
\bibliography{ref}
\end{multicols}

\end{document}
```

### 模板B：单栏SYSUReport（实验/编程类默认）

适用场景：有封面、目录、摘要的实验报告，适合包含代码和详细实验步骤的作业。

```latex
\documentclass{SYSUReport}

\usepackage{graphicx}
\usepackage{float}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{listings}
\usepackage{xcolor}
\usepackage{booktabs}
\usepackage{multirow}
\usepackage{subfigure}

% 代码块配色
\definecolor{codegreen}{rgb}{0,0.6,0}
\definecolor{codegray}{rgb}{0.5,0.5,0.5}
\definecolor{codepurple}{rgb}{0.58,0,0.82}
\definecolor{backcolour}{rgb}{0.95,0.95,0.92}

\lstset{
    backgroundcolor=\color{backcolour},
    commentstyle=\color{codegreen},
    keywordstyle=\color{magenta},
    numberstyle=\tiny\color{codegray},
    stringstyle=\color{codepurple},
    basicstyle=\ttfamily\footnotesize,
    breaklines=true,
    captionpos=b,
    keepspaces=true,
    numbers=left,
    numbersep=5pt,
    frame=single
}

\headl{}\headc{}\headr{[课程名称]}
\lessonTitle{[课程名称]}
\stuname{[姓名]}
\stuid{[学号]}
\inst{[学院]}
\major{[专业]}
\date{\today}

\begin{document}

\cover
\thispagestyle{empty}
\clearpage

\begin{abstract}
[摘要内容]

\textbf{关键词}：[关键词1]，[关键词2]，[关键词3]
\end{abstract}
\clearpage

\pagenumbering{arabic}
\setcounter{tocdepth}{2}
\tableofcontents
\clearpage

\pagenumbering{arabic}
\setcounter{page}{1}

% ===== 正文章节 =====
\section{[第一章标题]}
[正文内容...]

\end{document}
```

---

## 内容写作规范

### 报告类型与行文风格

#### 实验/编程类报告（使用模板B）

核心原则：**体现"我"在完成实验过程中的真实思考与判断**，不是步骤说明书，而是有分析深度的工程报告。

用第一人称叙述，但要有具体场景感。不是"我完成了超参数调整"，而是"训练初期 loss 一直在 2.3 附近徘徊，我怀疑是学习率太大导致梯度震荡，于是将 lr 从 1e-3 降到 3e-4，之后 loss 才开始稳定下降"。每个关键决策都说明为什么这样选择，遇到的问题、尝试过的方案、最终为何选定当前做法，这些过程比结论本身更有价值。

实验结果要定量分析（引用具体数值），并解释数字背后的原因——"准确率提升了 3.2%"没有意义，"在 X 数据集上 mAP 从 68.4 提升到 71.6，主要得益于引入了 Y 机制后模型对小目标的召回率显著提高"才有价值。插图以实验过程图、设置截图、结果对比图为主，每张图在正文中都要有详细分析段落而不只是一句"如图所示"。代码块用 `lstlisting` 环境，标注语言，加注释解释关键逻辑。

#### 论文/调研类报告（使用模板A）

核心原则：**广度+深度+专业度**，不是百科堆砌，而是有自己分析视角的学术写作。

广度上要覆盖该方向的主要研究脉络和代表性工作，但不是把每篇论文的摘要拼在一起——要有梳理和归纳，把相似思路的工作放在一起比较，而不是逐篇罗列。深度上要有判断：某种方法的局限在哪里、后续工作为什么要这样改进、不同方法之间的本质区别是什么。不要只写"A方法提出了B"，要写"A方法的核心突破在于…，但它的问题是…，这促使了后来C方法从另一个角度重新思考这个问题"。

引言可以从实际应用场景或你自己的学习体会出发，正文以客观学术语气为主，但适当加入评价性语句（"这一设计思路颇为巧妙，因为…"、"值得注意的是…"）让文章有观点而不只是陈述。

### 去AI化写作规范（所有报告均适用）

这是最重要的写作规范。AI生成文本的典型特征是：段落高度并列化、结构过于整齐、每句话都是完整的独立陈述、读起来像词条堆砌而不像一个人在思考。课程报告要规避这些特征。

**禁止行为：**
- 正文主体不得出现大量分点（`\item` 环境）。分点只用于真正需要列举的场合（如步骤序列、参数对比），绝不用分点来代替段落叙述
- 禁用套话开头：不写"随着人工智能的飞速发展…"、"本节将介绍…"、"综上所述…"这类空洞引导句
- 禁止每节结尾都有"本节小结"式的总结句，结尾自然收束即可
- 禁止句式过度并列：不写"首先A，其次B，再次C，最后D"这种四平八稳的结构

**应该怎么写：**

正文用自然的段落叙述。一个段落可以有主句、补充说明、例子、转折，长短句交替，有时候一个判断只需要一句话，有时候一个论证需要展开四五句。

实验类报告要体现过程的真实感：遇到了什么问题、尝试了哪种解决方案、为什么这么选、结果出乎意料还是符合预期——这些才是个人报告的核心价值，而不是把实验步骤按编号列出来。

论文类报告要有观点和判断，不只是描述"某某方法提出了XXX"，而是评价"这种做法的问题在于…"、"相比之下，后续工作…的改进更为根本，因为…"。有时候可以用反问来引导读者："这种设计真的能解决问题吗？"

技术细节的叙述可以稍微口语化，用"也就是说"、"换个角度看"、"更直观地理解"这类连接词，让读者感受到作者在引导而不是在堆砌信息。

### 语言与风格（通用）

- 正文：中文学术语言，但不拒绝适度的口语化表达以保持真实感
- 英文术语首次出现给出中文解释，如"神经辐射场（NeRF, Neural Radiance Fields）"
- 叙述清晰简洁，避免套话堆砌

### 参考文献时效性

根据领域动态程度区分：

| 领域类型 | 引用年份要求 |
|---------|------------|
| 热门新工科（CV、具身智能、大模型、NLP、SDN等） | **优先2023-2026，原则上不引2021年以前文献** |
| 一般工科（机器人、控制、通信等） | 近5年为主（2021-2026），经典奠基文献可例外 |
| 实验类报告/旧工科（电机、信号处理等） | 5年以上经典文献可正常引用 |

生成报告时根据课程方向自动判断适用规则。

### 章节结构建议（论文类，若教师无特殊要求）

1. **引言**：从实际需求/问题出发，提出核心研究问题，最后明确列出本文贡献（1-3条）
2. **相关工作/背景**：技术脉络梳理，对比分析
3. **核心方法/内容**（1-3章，视主题而定）
4. **实验/案例分析**（如有）：数据、结果、分析
5. **总结与展望**：核心结论 + 未来方向

### 数学公式

使用`equation`环境并编号，例如：

```latex
\begin{equation}
    C(\mathbf{r}) = \int_{t_n}^{t_f} T(t)\sigma(\mathbf{r}(t))\mathbf{c}(\mathbf{r}(t), \mathbf{d}) dt
\end{equation}
```

所有公式必须在正文中被引用（`\eqref{}`）。

---

## 图片处理规范

### 铁律：绝不在正文中内联生成图片

**不管任何情况，所有图片位置必须使用三层占位结构。** 不允许用代码（如 tikz、pgfplots）直接在 LaTeX 中生成图形内容，也不允许省略占位直接写注释。三层结构是不可妥协的默认行为。

默认图片格式为 **`.jpg`**（AI生图工具和截图工具默认输出均为jpg）。仅当用户明确指定 png 时才改用 png。

### 三层占位结构（所有图片均使用此格式）

```latex
% -------------------------------------------------------
% 图[N]：[图片内容简述]
% 来源类型：[文献图 / AI生图 / 用户截图]
% [来源说明，见下方三种类型]
% -------------------------------------------------------

% === 真实插图（准备好图片后取消注释，删除下方占位）===
%\begin{figure}[H]
%    \centering
%    \includegraphics[width=0.8\textwidth]{fig/[文件名].jpg}
%    \caption{[图注说明。\cite{引用键}]}
%    \label{fig:[标签]}
%\end{figure}

% === 占位（插入真实图片后删除此块）===
\begin{figure}[H]
    \centering
    \fbox{\parbox{0.7\textwidth}{\centering\vspace{1.5cm}[图N占位：图片内容简述]\vspace{1.5cm}}}
    \caption{[图注说明]}
    \label{fig:[标签]-placeholder}
\end{figure}
```

### 来源类型说明

**类型A - 文献图片**（直接引用论文中的图）：

```
% 来源：[作者姓名] et al., [年份], [论文标题简称], 原文图[X]
% 下载链接：[论文DOI或arXiv链接]
% 操作：下载论文 → 截取图[X] → 命名为 fig/[文件名].jpg 放入项目
```

**类型B - AI生图**（流程图、架构图、示意图等适合AI绘制的图）：

```
% AI生图指引（适用于流程图/架构图/示意图）：
% 比例：[16:9（横图/跨栏大图） / 4:3（普通图） / 1:1（方图）]
% 分辨率：2K（2048×1152 或 1920×1080）
%
% Prompt（英文，发给 Midjourney / DALL-E / Stable Diffusion 等）：
% [详细的英文描述，包含：
%   - 图的类型（architecture diagram / flowchart / block diagram）
%   - 各层级/模块名称和连接关系
%   - 颜色方案（如：light blue for input layer, dark blue for processing）
%   - 风格要求（professional academic diagram, white background, clean vector style）
%   - 标注语言：图中的说明性文字（层名、功能描述、流程标签）使用中文；
%              技术名词和专有名词保留英文（如 Python、BERT、ResNet、API 等）
%   - 如有图标：对主要模块或关键组件，在合适的地方加入直观的小图标或符号（不必每个元素都加）]
%
% 中文补充说明：说明性文字用中文，专有名词保留英文；关键组件可酌情加图标，无需逐一覆盖
% 生成后命名为 fig/[文件名].jpg
```

**类型C - 用户自截图**（实验结果、代码运行截图等）：

```
% 请截取：[具体内容描述，如：PPO训练曲线（episode reward随step变化）的可视化界面]
% 建议截图尺寸不小于 1200×900px，命名为 fig/[文件名].jpg
```

### 双栏图片格式

**跨栏大图**（放在`multicols`环境外，适合流程图、时间线等）：

```latex
\begin{figure*}[t]
    \centering
    \includegraphics[width=0.9\textwidth]{fig/[图片文件名].jpg}
    \caption{[图注说明。\cite{引用键}]}
    \label{fig:[标签]}
\end{figure*}
```

**单栏图**（放在`multicols`环境内）：

```latex
\begin{center}
    \begin{minipage}{\columnwidth}
        \centering
        \includegraphics[width=0.85\columnwidth]{fig/[图片文件名].jpg}
        \captionof{figure}{[图注。\cite{引用键}]}
        \label{fig:[标签]}
    \end{minipage}
\end{center}
```

图片文件统一放在`fig/`子目录，文件名用英文小写加下划线。

---

## 表格规范

使用`booktabs`风格，例如：

```latex
\begin{center}
\begin{minipage}{\columnwidth}
\captionof{table}{[表格标题]}
\begin{tabular}{lcc}
\toprule
方法 & 指标A & 指标B \\
\midrule
方法1 & 0.82 & 0.75 \\
方法2 & \textbf{0.91} & \textbf{0.88} \\
\bottomrule
\end{tabular}
\end{minipage}
\end{center}
```

---

## 参考文献

- 格式：GBT 7714 数字引用（`gbt7714-numerical`）
- 引用文件名：`ref.bib`
- 在正文相应位置用`\cite{key}`引用
- **在报告末尾单独列出建议搜索的参考文献关键词/论文标题**（方便用户补充`ref.bib`）

---

## 处理教师提供Word模板的情况

如果用户提到"老师给了模板"且是Word格式：
1. 询问用户是否已上传模板文件
2. 读取模板，提取结构要求
3. 将内容按教师模板结构输出为`.docx`（调用docx skill）或给出对应LaTeX适配代码
4. 明确告知用户：Word模板输出的是`.docx`文件，需在Word中打开而非Overleaf

---

## 最终输出格式

1. **一个完整的`.tex`文件**，命名规范：`[课程名缩写]_report_[简短主题].tex`
2. **图片清单**（纯文字说明）：每张图的位置、内容描述、来源类型、下载/生成指引
3. **参考文献建议**（纯文字）：5-10篇建议查找的文献方向，含年份和关键词
4. 如有代码，确保`lstlisting`环境有语言标注和必要注释

---

## 注意事项

- 生成的LaTeX代码中，所有`[方括号内容]`都是需要替换的占位符
- 对于用户没有提供的实验数据，用注释`% TODO: 补充实际数据`标注，绝不编造数据
- 摘要和结论要高度一致，不能互相矛盾
- 引言最后一段必须明确列出"本文的主要贡献/研究问题"（1-3条）
- 所有图表在正文中都要有对应引用（`\ref{}`）和分析描述
