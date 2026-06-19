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

### 去AI化写作规范（所有报告均适