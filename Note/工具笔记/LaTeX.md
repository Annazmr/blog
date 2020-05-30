## LaTeX论文排版总结

宣凯洲 更新于2018-02-21

张梦冉 更新于2018-09-04

* **LaTeX文件结构**
v
  |— IJCAI

      |— ijcai.bib		参考文献BibTeX内容

      |— named.bst		参考文献BibTeX格式

  ​    |— ijcai.sty		排版格式代码

      |— ijcai.tex		论文LaTeX内容

#### 1. 参考文献引用

* 搜索参考文献的BibTeX格式（谷歌学术-引用-BibTeX）

* 将所有参考文献的BibTeX逐一列入ijcai.bib中，分别以第一行的索引字符串作为该文献的Label

* 在ijcai.tex中，采用"\cite{Label}"来引用文献，显示为"[Name *et al*., 2018]"

* 同时引用多个文献，采用"\cite{Label1,Label2,…}"（逗号前后不可增加空格）

* 当文献引用需要作为主语等句子成分时，写作"Name *et al.* \shortcite{Label}"（！使用"natbib"可以有别的写法）

* 引用格式所导入的文件设置在文末：

  \bibliographystyle{named}
  \small\bibliography{ijcai}

* 参考文献注释：

  @inproceedings注释部分为：(1) page、volume、number; (2) 有booktitle注释organization;

  @article都不注释

  @incollection都不注释

**!** 撰写论文时，按引用顺序逐一拷贝文献的BibTeX格式，并添加其Label作为引用标识，排版时较为方便

#### 2. 项目罗列

* 需要分点详细描述，采用"123"、"abc"等作为分点标识，使用以下格式：

  \begin{enumerate}[X]

  \item

  \end{enumerate}

  其中X部分可填入"(1)"、"1)"、"(a)"、"a"等标识

* 仅需罗列内容，采用"•"作为分点标识，使用以下格式：

  \begin{itemize}

  \item

  \end{itemize}

#### 3. 公式

* 常规公式：

  \begin{equation}
  \label{eqn_example}
  XXX.
  \end{equation}

* 需要拆分行的公式：

  \begin{equation}
  \label{eqn3_2}
  \begin{aligned}
  Y=&XXX\\\
  &ZZZ.
  \end{aligned}
  \end{equation}

* 段内公式：\$XXX$

* 常用：

  …：\ldots

  |：\mid

  ·：\cdots

  \log \sin \arg \tanh \sum

#### 4. 图片

* 横跨两列的图片采用：

  \begin{figure*}[!t]
  \centering
  \includegraphics[width=7in]{XXX.pdf}
  \caption{\label{font-table} Introduction.}
  \label{fig_sim1}
  \end{figure*}

* 无需横跨的图片将"figure*"替换为"figure"

#### 5. 表格

* 横跨两列与否的方式与图片相同

* 采用：

  \begin{table}
  \small (or \\scriptsize) (设置表格大小)
  \setcounter{table}{N}	(设置表标号为N+1)
  \centering
  \caption{\label{font-table} Introduction. }
  \begin{tabular}{|c|c|c|}
  \hline \bf A & \bf B & \bf C \\ \hline
  A1 & B1 & C1 \\
  \hline
  \end{tabular}
  \end{table}
\begin{tabular}{c||c|r}
%一个c表示有一列，通过添加 | 来表示是否需要绘制竖线，%l左 r右 c居中，两个竖杠在表格中插入双竖线
\hline  % 在表格最上方绘制横线
(1,1)&&(1,2)\\
\hline  %在第一行和第二行之间绘制横线
(2,1)&&(2\\
\hline % 在表格最下方绘制横线
\end{tabular}


#### 6. 章节

* 摘要采用：

  \begin{abstract}

  \end{abstract}

* 一级标题：\section{Introduction}

* 二级标题：\subsection{Multi-label Learning}

* 三级标题：\subsubsection{Multi-label Learning}

  默认标题均有标号

* 消除缩进：\noindent

#### 7. 文字

* 加粗：\textbf，部分加粗：\textbf{XXX}，简写：\bf
* 斜体：\emph，简写：\em
* 下划线：\underline

#### 8. 脚标

* 在需要设置脚标的字词后面采用：\footnote{XXX}