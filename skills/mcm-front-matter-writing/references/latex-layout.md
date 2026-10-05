# LaTeX 格式与检查

在用户要求插入模板或修改 LaTeX 时使用本参考。正文要求以 SKILL.md 为准；这里的尺寸、间距与示例内容只是实现起点。

## 原文档编辑

- 读取当前打开的 `.tex`，在原文件内修改，保留当前编辑器。不要为一次续写重建整篇文档、另编一份 PDF 或打开另一标签页。
- 已有摘要及其分页保持原样，前置章节接在正文起始位置，模型优缺点接在求解、检验等正文之后。遵守现有字体、字号、首行缩进、页眉与章节层级。
- 宏包已加载时不重复添加。以下示例按需使用 `booktabs`、`tabularx`、`graphicx`、`float`、`needspace` 和 `enumitem`；也可沿用模板提供的等效环境。
- 不为凑行数或塞进某页而缩小字体、行距和页边距。

## Our Work 空图

```latex
% 按实际图框和标题总高调整预留空间，避免标题孤立在上一页。
\Needspace{65mm}
\subsection{Our Work}
\begin{figure}[H]
  \centering
  % 这里仅占位；用户提供成图后替换下一行。
  \fbox{\rule{0pt}{45mm}\rule{0.90\linewidth}{0pt}}
  \caption{Overview of the modeling framework.}
  \label{fig:our-work}
\end{figure}
```

框内保持空白，不添加 “to be added”、流程节点或箭头。不要把尚不存在的图片文件写入 `\includegraphics`，以免编译失败。后续插图时，在同一个 figure 中用真实文件路径的 `\includegraphics` 替换框体，核对宽高与可读性。

## 假设与理由

```latex
\section{Assumptions and Justification}

\noindent\begin{minipage}{\linewidth}
\textbf{Assumption 1: Each room inspection proceeds without interruption.}\\
\textbf{Justification:} Complete inspections give each task a defined duration and an unambiguous clearance status.
\end{minipage}

\medskip
% 按论文需要继续下一条，最多四条。
```

这条内容来自疏散论文示例，只展示格式，不是任何赛题都适用的假设。`minipage` 用于让假设与理由保持同页，**不保证三行**。首行的粗体也会影响宽度，必须按目标字体与版心检查。

排版目标是首行一行假设，接下来一至两行理由。超出时压缩措辞，保留关键条件；不要用固定高度盒子裁去超出的内容、缩放整段或允许文字溢出。

## 标准三线符号表

```latex
\section{Notations}
The principal symbols used in the model are listed in Table~\ref{tab:notations}.

\begin{table}[H]
  \centering
  \caption{Principal model notation.}
  \label{tab:notations}
  \renewcommand{\arraystretch}{1.12}
  \begin{tabularx}{\linewidth}{@{}l>{\raggedright\arraybackslash}Xc@{}}
    \toprule
    \textbf{Symbol} & \textbf{Description} & \textbf{Unit} \\
    \midrule
    $d(e)$ & Physical length of edge $e$ & $\mathrm{m}$ \\
    $v_{\mathrm{eff}}(e,t)$ & Effective responder speed on edge $e$ at time $t$ & $\mathrm{m\,s^{-1}}$ \\
    $T_{\mathrm{makespan}}$ & Time required to complete all sweeps and verification & $\mathrm{s}$ \\
    \bottomrule
  \end{tabularx}
\end{table}
```

三行数据只是格式例子，必须换成目标论文的实际主要符号。使用可换行的 Description 列适应版心，保持正常字号，不通过 `\resizebox` 缩小文字。不要加入额外的 `\hline`、列格式中的 `|`、逐行分隔线或表后注释。

如表格较长，按真实高度预留空间，确保节标题、表题与表格合理衔接；不要硬编码示例页数或为所有论文强制另起一页。可用 `\Needspace` 或模板已有的布局手段，避免标题独留上一页。

## 模型优缺点

```latex
\section{Strengths and Weaknesses}
\subsection{Strengths}
\begin{enumerate}[label=\textbf{\arabic*.},leftmargin=2em,itemsep=6pt,topsep=4pt,parsep=0pt]
  \item \textbf{Hazard-dependent routing.} Smoke and fatigue modify travel costs, linking route selection to changing local conditions.\par
\end{enumerate}

\subsection{Weaknesses}
\begin{enumerate}[label=\textbf{\arabic*.},leftmargin=2em,itemsep=6pt,topsep=4pt,parsep=0pt]
  \item \textbf{Fixed connectivity.} Route closures can invalidate schedules; updating the graph and recalculating assignments would address this limitation.\par
\end{enumerate}
```

每一点的加粗短标题与解释在同一段内，**合计最多两行**。两段文字只是疏散论文的格式示例，条数、内容和是否另起一页均按目标论文处理。列表缩进、字体、粗体字宽与版心都影响实际行数。

需要自动核查时，可以临时使用以下 TeX 检查，在每条单段条目末尾立即调用 `\CheckEvaluationLines{条目标识}`，再用同一文件的内置编译器编译：

```latex
\newcommand{\CheckEvaluationLines}[1]{%
  \par
  \ifnum\prevgraf>2\relax
    \PackageError{layout-check}{Evaluation item #1 exceeds two lines}{Shorten the item text.}%
  \fi
}
```

这个检查读取刚结束段落的排版行数，不能检查包含多个段落或嵌套盒子的条目，也不能代替文字溢出检查。若超限，缩短相应条目；通过后移除临时定义，将调用还原为 `\par`，保留相同文字和版式，再编译最终文件。只有实际启用了此类检查并通过，才能报告已自动核查两行上限；普通编译成功不能证明行数。

## 编译与版面核查

在 Codex 内置 LaTeX 编辑器中，保存后调用 `compile_latex_document` 检查同一文件；若有错误，在工具的修复次数限制内处理。不要用另一个编译流程导出独立 PDF 代替当前预览。

有可用的预览检查能力时核查：摘要分页未被破坏；Our Work 框体为空且处于正确小节；每条假设为一至三行；表格无越界、无竖线、无表后说明；模型优缺点每点含标题为一至两行。只返回编译成功而没有页面内容时，不声称已经完成视觉检查，也不把源码中的换行数当作排版行数。
