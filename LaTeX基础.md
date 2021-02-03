## <center> LaTex笔记(Windowns) </center> 

### 1. LaTex安装 
#### LaTex下载 
1. 官方网站(<https://www.tug.org/texlive>)页面选择`on DVD`，然后选择`downloading the TeX Live ISO image and burning your own DVD`，点击`download from a nearby CTAN mirror`选择`texlive2020-20200406.iso`(iso文件大约4GB)下载；  
2. 打开下载好的`texlive.iso`文件,以管理员身份运行`install-tl-windowns.bat`windows批处理文件； 
3. 等待安装结束。  
#### LaTex集成开发软件下载(*此处使用 texstudio 软件*<<http://texstudio.sourceforge.net/>>)

#### 检测安装是否成功  
&emsp;&emsp;按<kbd>win</kbd>+<kbd>R</kbd>键启动命令提示符，输入`cmd`进入命令窗口，在窗口中输入`tex -v`，`latex -v`等等可查看是否安装成功。 


### 2. LaTex使用运行  
#### 用windows记事本写Latex  
1. 新建记事本，并将其后缀改为`.tex`（或者在Windows命令行中输入`notepad test.tex`创建Latex文件）；  
2. 编译命令：`latex test.tex`；编译含有中文的.tex文件先将文件选择为utf-8编码保存，并执行命令：`xelatex test.tex`;
3. 转化为PDF文件命令：`divpdffmx test.tex`;
4. 删除中间过程产生的文件：`del *.aux *.div *.log`。  
##### 以上过程可写成Windows批处理文件`.bat`执行：
全英文文档：  
```bat
latex test.tex
divpdfmx test.div
del *.aux *.div *.log
```
含有中文的文档：
```bat
xelatex test.tex
del *.aux *.div *.log
```


### 3. LaTex源文件的基础编写  
用`\documentclass{}`引入一个文档类，
`article`文档类为撰写论文相关操作的文档类。  
```laTex
\documentclass{article}

\begin{document}

Hello \LaTex.

\end{document}
```  
含有中文的源文件(支持中文必须要让源文件支持utf-8编码)：  
```laTex  
\documentclass{article}

\usepackage{ctex}  %ctex宏包为能够处理中文的宏包

\begin{document}

你好， \LaTex.

\end{document}
```  
*LaTex处理中文步骤：*  
+ 文档中需要引用`ctex`宏包  
+ 文档为utf-8编码进行存储  
+ 用`xelatex`命令对文件进行编译  


### 4. LaTex源文件基本结构  
```LaTex
% 导言区
\documentclass{article} % book, report, letter  

\title{My First Document}  
\author{Zhang San}
\date{\today}

% 正文区（文稿区）
\begin{document} 
    \maketitle % 输出标题

    Hello World!

    % here is my big formula
    Let $f(x)$ be defined by the formula $f(x)=3x^2+x-1$
    $$f(x)=3x^2+x-1$$
\end{document}
```
+ 正文区有且只有一个`document`环境
+ `$公式$`(一对`$`包围起来)称为数学模式 
+ *单`$`表示行类公式，双`$$`表示行间公式*
+ 增加一行空行表示回车(将文字分为两行)  
+ 使用`newcommand{}{}`定义一个命令


### 5. LaTex中的中文处理办法  
+ 源文件编码为`utf-8`  
+ 使用`usepackage{ctex}`引用`ctex`中文宏包

`equation`环境可以产生带有编号的行间公式：
```LaTex
\begin{document}

    \begin{equation}  % equation环境产生带有编号的行间公式 
    AB^2 = BC^2 + AC^2.
    \end{equation}

\end{document}
```
- ***可以在cmd命令行中输入`texdoc ctex`命令打开ctex宏包手册***
- ***使用`texdoc lshort-zh`命令查看LaTex简单使用教程***


### 6. LaTex的字体设置  
+ 字体族  
  + 罗马字体：笔画起始处有装饰
  + 无衬线字体：笔画起始处无装饰
  + 打字机字体：每个字符宽度相同，又称为等宽字体
+ 字体系列  
  + 粗细
  + 宽度
+ 字体形状
  + 直立
  + 斜体
  + 伪斜体
  + 小型大写
+ 字体大小  

字体族设置：
```LaTex
\documentclass[11pt]{article}  %[11pt]为字体大小为11磅（一般只有10、11、12磅）

\usepackage{ctex}

\newcommand{\myfont}{\textit{\textsf{Fancy Text}}}  % 使用newcommand命令定义一个\myfont命令

\begin{document}
    % 字体族设置（罗马字体、无衬线字体、打字机字体）
    \textrm{Roman Family}  % 设置字体族为Roman Family字体

    \textsf{Sans Serif Family}  % 无衬线字体

    \texttt{Typewriter Family}  % 打字机字体

    \rmfamily Roman Family  % 使用\rmfamily声明后续字体为Roman Family字体

    % 字体系列设置（粗细、宽度）
    \textmd{Medium Series} \textbf{Boldface Series}

    {\mdseries Medium Series} {\bfseries Boldface Series}

    % 字体形状（直立、斜体、伪斜体、小型大写）
    \textup{Uprignt Shape} \textit{Italic Shape}
    \textsl{Slanted Shape} \textsc{Small Caps Shape}

    {\upshape Uprignt Shape} {\itshape Italic Shape}
    {\slshape Slanted Shape} {\scshape Small Caps Shape}

    % 中文字体（必须使用ctex宏包）
    {\songti 宋体} \quad {\heiti 黑体} \quad {\fangsong 仿宋} \quad {\kaishu 楷书}

    中文字体的\textbf{粗体}与\textit{斜体}

    \myfont

\end{document}
```
*其他中文字体的相关命令可查看ctex文档*


### 7. LaTex文档基本结构  
+ **空**一行或多行可分段落（首行缩进）  
+ `\par`命令：分**段落**  
+ `\\`命令：分**行**
+ **`\tableofcontents`命令：生成目录**


```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}

% 正文区（文稿区）
\begin{document}
	\tableofcontents	% \tableofcontents生成目录
	
	\section{引言}	% \section{title}为一级标题
	\section{实验方法}
	\section{实验结果}
	\subsection{数据}		%\subsection{title}为二级标题
	\subsection{图表}
	\subsubsection{实验条件}	%\subsubsection{title}三级标题
	\subsubsection{实验过程}
	\subsection{结果分析}
	\section{结论}
	\section{致谢}
	
\end{document}
```

### 8. LaTex中的特殊字符  
+ 空行分段，多个空行等同1个  
+ 自动缩进，绝对不能使用**空格**代替  
+ 英文中多个空格处理为1个空格，中文空格自动忽略  
+ 汉字与其他字符的间距会自动由XeLaTex处理  
+ 禁止使用中文全角空格  

```LaTex
% 引言
% 引言
\documentclass{article}

\usepackage{ctex}

% 正文区（文稿区）
\begin{document}
	\section{空格字符}
	% 1em(当前字体中M的宽度)
	a\quad b
	
	% 2em
	a\qquad b
	
	% 约为1/6个em
	a\,b a\thinspace b
	
	% 0.5个em
	a\enspace b
	
	% 空格
	a\ b
	
	% 硬空格
	a~b
	
	% 1pc=12pt=4.218mm
	a\kern 1pc b
	
	a\kern -1em b
	
	a\hskip 1em b
	
	a\hspace{35pt}b
	
	% 占位宽度
	a\hphantom{xyz}b
	
	% 弹性长度
	a\hfill b
	\section{\LaTeX 控制符}
	\# \$ \% \{ \} \~{} \_{} \^{} \textbackslash % 反斜杠使用\textbackslash产生
	\&
	\section{排版符号}
	\S \P \dag \ddag \copyright \pounds
	\section{\TeX 标志符号}
	% 基本符号
	\TeX{} \LaTeX{} \LaTeXe{}
	\section{引号}
	` ' `` ''  ``你好''
	\section{连字符}
	- -- ---
	\section{非英文字符}
	\oe \OE \ae \AE \aa \AA \o \O \l \L \ss \SS !` ?`
	\section{重音符号(以o为例)}
	\`o \'o \^o \''o \~o \=o \.o \u{o} \v{o} \H{o} \r{o} \t{o} \b{o} \c{o} \d{o}
		
\end{document}
```


### 9. LaTex中的插图
#### 更多 graphicx 的用法可打开`texdoc graphicx`文档查看
+ 导言区：`\usepackage{graphicx}`宏包
+ 语法：`\includegraphics[<选项>]{<文件名>}`
+ 格式：EPS,PDF,PNG,JPEG,BMP

```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}

%导言区：\usepackage{graphicx}
%语  法：\includegraphics[< 选项 >]{< 文件名 >}
%格  式：EPS,PNG,PDF,JPEG,BMP
\usepackage{graphicx}
\graphicspath{{figures/},{pics/}}	% 图片在当前目录下的 figures 目录, pics 目录


% 正文区（文稿区）
\begin{document}
	\LaTeX{}中的插图：
	
	\includegraphics{wallpaper}
	\includegraphics{wallpaper.jpg}
	
	\includegraphics[scale=0.3]{wallpaper}
	
	\includegraphics[height=2cm]{wallpaper}
	
	\includegraphics[width=2cm]{wallpaper}
	
\end{document}
```

### 10. LaTex中的表格
+ #### 打开`texdoc booktab`三线表
+ #### 打开`texdoc longtab`跨页长表格
+ #### 打开`texdoc tabu`综合表格

```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}

% 正文区（文稿区）
\begin{document}
	% 使用tabular环境生成表格
	% l:左对齐，c:居中对齐，r:右对齐，p{< 宽度 >}:产生指定宽度的列格式(内容超过宽度会自动换行)
	% |:产生竖线，\hline:产生表格横线
	\begin{tabular}{|l||c|c|c|r|p{1.5cm}|}	%两个|产生双竖线
		\hline  % 产生表格横线
		姓名 & 语文 & 数学 & 英语 &备注 & \\
		\hline \hline % 两个\hline产生双横线
		张三 & 87 & 100 & 98 & 优秀 & \\
		\hline
		李四 & 75 & 64 & 52 & 补考另行通知&  \\
		\hline
		王五 & 80 & 82 & 78 &  & \\
		\hline
	\end{tabular}
	
\end{document}
```

### 11. LaTex中的浮动体
+ 浮动体
+ figure环境(table环境类似)
  + `\begin{figure}[htbp]`
  + `	< 任意内容 >`
  + `\end{figure}`

+ <允许位置>参数(默认tbp)
  + h，此页(here)——代码所在的上下文的位置
  + t，页顶(top)——代码所造的页面或之后的页面的顶部
  + b，页底(bottom)——代码所在页面或也买你之后页面的底部
  + p，独立一页(page)——浮动页面

+ 标题控制(caption、bicaption等宏包)
+ 并排与子图表(subcaption、subfig、floatrow等宏包)
+ 绕排(picinpar、wrapfig等宏包)

```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}
\usepackage{graphicx}

\graphicspath{{figures/}}

% 浮动体
% figure环境(table环境类似)
% \begin{figure}[htbp]
% 	< 任意内容 >
% \end{figure}

% <允许位置>参数(默认tbp)
% h，此页(here)——代码所在的上下文的位置
% t，页顶(top)——代码所造的页面或之后的页面的顶部
% b，页底(bottom)——代码所在页面或也买你之后页面的底部
% p，独立一页(page)——浮动页面

% 标题控制(caption、bicaption等宏包)
% 并排与子图表(subcaption、subfig、floatrow等宏包)
% 绕排(picinpar、wrapfig等宏包)

% 正文区（文稿区）
\begin{document}
	\LaTeX{}中的插图：
	壁纸可图\ref{fig-wallpaper}
	
	% figure：图片浮动体环境
	\begin{figure}[htbp] % 允许各个位置
		\centering	% \centering 居中对齐
		\includegraphics[scale=0.3]{wallpaper.jpg}
		
		% \caption{text}：设置图片标题
		% \label{key}设置标签
		\caption{壁纸}\label{fig-wallpaper}
	\end{figure}


	
	在\LaTeX{}中的表格：
	
	% table：表格浮动体环境
	\begin{table}[h] % 允许各个位置
		\centering
		\caption{考试成绩单}
		\begin{tabular}{|l||c|c|c|r|}
			\hline
			姓名 & 语文 & 数学 & 英语 &备注 \\
			\hline \hline
			张三 & 87 & 100 & 98 & 优秀 \\
			\hline
			李四 & 75 & 64 & 52 & 补考另行通知 \\
			\hline
			王五 & 80 & 82 & 78 & \\
			\hline
		\end{tabular}
	\end{table}

\end{document}
```


### 12. 数学公式初步

```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}
\usepackage{amsmath}


% 正文区（文稿区）
\begin{document}
	\section{行内公式}
	\subsection{美元符号}
	交换律是 $a+b=b+a$
	\subsection{小括号}
	交换律是 \(a+b=b+a\)
	\subsection{math环境}
	交换率是 
	\begin{math}
		a+b=b+c
	\end{math}

	\section{上下标}
	\subsection{上标}
	$3x^{20} - x + 2 = 0$
	\subsection{下标}
	$a_1,a_2,a_3...a_{100}$
	\section{希腊字母}
	% 直接使用希腊字母对应的英文名称
	$\alpha$
	
	$\alpha^3 + \beta^2 + \gamma = 0$
	\section{数学函数}
	$\log$
	$\sin$
	$\cos$
	$\arcsin$
	$\arccos$
	$\ln$
	
	$\sin^2 x + \cos^2 x = 1$
	
	$\sqrt{2}$
	$\sqrt[3]{27}$
	\section{分式}
	$3/4$,
	$\frac{3}{4}$
	\section{行间公式}
	\subsection{美元符号}
	$$a+b=b+a$$
	\subsection{中括号}
	\[a+b=b+a\]
	\subsection{displaymath环境}
	\begin{displaymath}
		a+b=b+a
	\end{displaymath}
	\subsection{自动编号公式equation环境}
	交换律见式\ref{eq:commutative}
	\begin{equation}
		a+b=b+a \label{eq:commutative}
	\end{equation}
	\begin{equation}
		ax^2+bx+c=0
	\end{equation}
	\subsection{不编号公式equation*环境}
	% equation*环境需要添加amsmath宏包
	\begin{equation*}
		ax^2+bx+c=0
	\end{equation*}
		
\end{document}
```


### 13. 数学公式的矩阵
需要引入`amsmath`宏包
```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}
\usepackage{amsmath}


% 正文区（文稿区）
\begin{document}
	% 矩阵环境，用&分隔列，用\\分隔行
	\[
	\begin{matrix}
		0 & 1\\
		1 & 0
	\end{matrix} \qquad
	% 带有小括号的矩阵
	\begin{pmatrix}
		0 & 1\\
		1 & 0
	\end{pmatrix} \qquad
	% 矩阵两端加中括号
	\begin{bmatrix}
		0 & -1 \\
		1 & 0
	\end{bmatrix} \qquad
	% 矩阵两端加大括号
	\begin{Bmatrix}
		1 & 0 \\
		0 & -1
	\end{Bmatrix} \qquad
	% 行列式,两端加单竖线
	\begin{vmatrix}
		i & 0 \\
		0 & i
	\end{vmatrix} \qquad
	% 两端加双竖线
	\begin{Vmatrix}
		1 & 2 \\
		3 & 4
	\end{Vmatrix}
	\]
	
	
	\[
	A = \begin{pmatrix}
		a_{11}^2 & a_{12}^2 & a_{13}^2 \\
		a_{21} & a_{22} & a_{23} \\
		a_{31} & a_{32} & a_{33}
	\end{pmatrix}
	\]
	
	% 常用省略号:\dots、\vdots、\ddots
	\[
	A = \begin{bmatrix}
		a_{11} & \dots & a_{1n} \\
		& \ddots & \vdots \\
		0 & & a_{nn}
	\end{bmatrix}_{n \times n}
	\]
	
	% 行内小矩阵（smallmatrix）环境
	复数 $z = (x,y)$ 也可用矩阵
	\begin{math}
		\left(	% 需要手动加上左括号
		\begin{smallmatrix}
			x & -y \\
			y & x
		\end{smallmatrix}
		\right)	% 需要手动加上右括号
	\end{math}来表示。

	% array环境(类似于表格环境tabular)
	\[
	\begin{array}{r|r}
		\frac{1}{2} & 0 \\
		\hline
		o & -\frac{a}{b}c \\
	\end{array}
	\]

\end{document}
```


### 14. 数学公式中的多行公式  
需要引入`amsmath`和`amssymb`宏包
+ 注意数学模式下`\text{text}`命令的使用，该命令可在数学模式下输入中文
```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}
\usepackage{amsmath}
\usepackage{amssymb}  % 输入花体字


% 正文区（文稿区）
\begin{document}
	% gather 和 gather* 环境(可使用\\换行)
	% 代编号
	\begin{gather}
		a + b = b + a \\
		ax^2+bx+c=0
	\end{gather}
	% 不代编号
	\begin{gather*}
		2 \times 8 =  8 \times 2 \\
		3 + 5 = 5 + 3 = 8
	\end{gather*}

	% 在\\前使用\notag 阻止编号
	\begin{gather}
		a + b = b + a \notag \\
		ax^2+bx+c=0 \notag
	\end{gather}

	% align 和align* 环境(用 & 进行对齐)
	% 带编号
	\begin{align}
		x &= t + \cos t + 1 \\
		y &= 2\sin t
	\end{align}
	% 不带编号
	\begin{align*}
		x &= t & x &= \cos t & x &= t\\
		y &= 2t & y &= \sin(t+1) & y &= \sin t
	\end{align*}

	% split 环境(对齐采用 align 环境的方式，编号在中间)
	\begin{equation}
		\begin{split}
			\cos 2x &= \cos^2 x - \sin^2 x \\
			&= 2\cos^2 x - 1
		\end{split}
	\end{equation}

	% cases 环境
	% 每行公式中使用 & 分隔为两部分
	% 通常表示值和后面的条件
	\begin{equation}
		D(x) = \begin{cases}
			1, & \text{if}~x \in \mathbb{Q}; \\
			0, & \text{if}~x \in \mathbb{R}\setminus\mathbb{Q}
		\end{cases}
	\end{equation}

\end{document}
```


### 15. 参考文献BibTex
#### 直接引用参考文献
```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}


% 正文区（文稿区）
\begin{document}
	% 一次管理，一次使用
	% 参考文献格式：
	% \begin{thebibliography}{样本编号}
	%	 \bibitem[记号]{引用标志}文献条目1
	%	 \bibitem[记号]{引用标志}文献条目2
	%	 ......
	% \end{thebibliography}
	% 其中文献条目包括：作者，题目，出版社，年代，版本，页码等。
	% 引用时候可以采用：\cite{引用标志1，引用标志2，...}
	
	引用一篇文章\cite{article1}，引用一篇文章\cite{article2}
	
	\centering
	\begin{thebibliography}{99}
		\bibitem{article1}李颖,李耀辉,王金鑫等.\emph{ SVM 和 ANN 在多光谱遥感影像分类中的比较研究}[J].海洋测绘.2016,36(05):19-22.
		\bibitem{article2}Huang C,Davis L S,Townshend J R G.\emph{An assessment of support vector machines for land cover classification}[J].International Journal of remote sensing.2002, 23(4):725-749.
	\end{thebibliography}
	
	
\end{document}
```
#### 使用 BibTex 管理参考文献
+ 需要选择构建文献管理工具为`BibTeX`


```LaTex
% 引言
\documentclass{article}

\usepackage{ctex}
%\usepackage{natbib} % natbib宏包可以指定更多的排版格式

\bibliographystyle{plain} % plain unsrt alpha abbrv 排版格式


% 正文区（文稿区）
\begin{document}
	这是一个参考文献的引用:\cite{陈绍杰2010boosting}
	
	这是另一个引用:\cite{huang2002assessment}
	% 使用\bibliography{bib file}指定参考文件数据库
	\nocite{*}
	\bibliography{test}
	
\end{document}
```


#### 16. 参考文献BibLaTex
+ 需要在构建中选择文献管理工具`Biber`


```LaTeX
% 引言
\documentclass{article}

\usepackage{ctex}

% biblatex/biber
% 新的TEX参考文献排版引擎
% 样式文件(参考文献样式文件--bbx文件，引用样式文件--cbx)使用LATEX编写
% 支持根据本地化排版，如：
%		biber -l zh_pinyin texfile	用于指定按拼音排序
%		biber -l zh_stroke texfile	用于按笔画排序

% 添加biblatex宏包，指定样式和后端程序
\usepackage[style=numeric,backend=biber]{biblatex}
% 添加参考文献数据库，不可以省略文件后缀名
\addbibresource{test.bib}

% 正文区（文稿区）
\begin{document}
	% 一次管理，多次使用
	无格式化引用\cite{biblatex}
	
	带方括号的引用\parencite{李颖2016svm}
	
	上标引用\supercite{zhao2017object}
	
	\centering
	% \nocite{*}列出未引用文献，*表示所有为未引用文献
	\nocite{*}
	\printbibliography[title = {参考文献}]
	
\end{document}
```


### 17. LaTeX中的自定义命令和环境

#### `\newcommand`命令：
```LaTeX
% 导言区
\documentclass{article}

\usepackage{ctex}

% \newcommand--定义命令
% 命令只能由字母组成，不能以\end 开头
% \newcommand{<命令>}[<参数个数>][<首参数默认值>]{<具体定义>}

% \newcommand可以是简单字符串替换，例如：
% 使用\PRC 相当于 People's Republic of \emph{China} 这一串内容
\newcommand{\PRC}{Peole's Republic of \emph{Chian}}

% \newcommand 也可以使用参数
% 参数个数可以从 1 到 9，使用时用 #1,#2,......,#9 表示
\newcommand{\loves}[2]{#1 喜欢 #2}
\newcommand{\hatedby}[2]{#2 不受 #1 喜欢}

% \newcommand的参数也可以有默认值
% 指定参数个数的同时指定了首个参数的默认值，那么这个命令
% 的第一个参数就成为可选参数（要使用中括号限定）
\newcommand{\love}[3][喜欢]{#2#1#3}

% 正文区（文稿区）
\begin{document}
	\PRC
	
	\loves{猫儿}{鱼}
	
	\hatedby{猫儿}{萝卜}
	
	\love{猫儿}{鱼}
	
	\love[最爱]{猫儿}{鱼}
	
\end{document}
```

#### `\renewcommand`、`\newenvironment`命令：
```LaTeX
% 导言区
\documentclass{article}

\usepackage{ctex}

% \renewcommand--重定义命令
% 与\newcommand 命令作用和用法相同，但只能用于已有命令
% \renewcommand{<命令>}[<参数个数>][<首参数默认值>]{<具体定义>}
\renewcommand{\abstractname}{内容简介}

% 定义和重定义环境
% \newenvironment{<环境名称>}[<参数个数>][<首参数默认值>]{<环境前定义>}{<环境后定义>}
% \renewenvironment{<环境名称>}[<参数个数>][<首参数默认值>]{<环境前定义>}{<环境后定义>}

% 为 book 类中定义摘要（abstract）环境
\newenvironment{myabstract}[1][摘要] %
{\small\begin{center}\bfseries #1\end{center} %
	\begin{quotation}} %
	{\end{quotation}}

% 正文区（文稿区）
\begin{document}
	\begin{abstract}
		这是一段摘要...
	\end{abstract}

	\begin{myabstract}
		这是一段自定义格式的摘要...
	\end{myabstract}

	\begin{myabstract}[我的摘要]
	这是一段自定义格式的摘要...
	\end{myabstract}
	
\end{document}
```
