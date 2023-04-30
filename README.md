% !Mode:: "TeX:UTF-8"
%!TEX program  = xelatex

%\documentclass{cumcmthesis}
\documentclass[withoutpreface,bwprint]{cumcmthesis} %去掉封面与编号页

\usepackage{subfigure}	%用于排版多张图片
\usepackage{float}	%用于排版图片位置
\bibliographystyle{plain}	%引用样式,参考文献
\usepackage{longtable}
\usepackage{url}
\usepackage{appendix}

\title{关于钢管下料问题的研究}

\begin{document}

\maketitle
\begin{abstract}

应客户要求，某钢厂用两类同规格但不同长度的钢管切割出四种不同长度的成品
钢管。故该原料下料问题为典型的优化模型。钢厂在切割钢管时,又要求每种钢管的
切割模式都不能超过5种，故我们先分别列出两种原料钢管出现频率较高的切割模式，
每一问都需要针对不同钢管节约要求分别求出 5 种切割模式的最佳组合。
第一问，要求余料最少，在切割模式的选择方面，我们尽量要求余料为零，并在
此基础上要求切割得成品钢管除满足客户要求外，多余客户要求的钢管数也要尽可能
的少，运用 MATLAB 软件求出余料最少时，需要 65 根 A 类钢管采用 4 种切割模式切割，
需要 40 根 B 类钢管采用 2 种切割模式切割，总余料为 20 米。
第二问，要求总根数最少，故我们只要求总根数最少，在这里我们分了两种情况：
有余料时，需 A 类钢管 65 根，采用 5 种切割模式，需 B 类钢管 38 根，采用 4 种切割
模式，余料各为 2 米；无余料时，需 A 类钢管 75 根，采用 3 种切割模式，需 B 类钢
管 39 根，采用 4 种切割模式。
第三问我们运用 Lingo 软件求出较优解为当p=0.4 时最大收益MinZa${_3}$ ，具体切割模式见模型求解部分。为了找到替代比例与最大收益的关系，我们分别给 赋p值为 0、10\%、20\%、30\%、40\%时，用 Lingo 解得各自的最大收益，并用四次拟合的方法大致算出了最大收益MinZa${_3} $和替代比例p 的关系。

\keywords{优化模型\quad 整数规划\quad  四次拟合\quad  }

\end{abstract}

%目录
%\tableofcontents

%新的一页
%\newpage

\section{问题重述}

\subsection{问题背景}

某钢厂主要生产两种结构用无缝钢管，两种钢管的外径、壁厚都相同，不同之处
在于 A 类型钢管 10\#钢制成，长度为 19 米；B 类型钢管用 20\#钢制成，长度为 29 米。

\subsection{问题重述}

假设某单位要订购该钢厂的一批钢管，要求钢厂将原料钢管按照订单的要求进行
切割成不同长度，具体如下：

\begin{center}
\begin{tabular}{|l|c|c|c|r|}
	\hline
	订货量&三米&五米&七米&八米\\
	\hline
	A类钢管&30&70&40&60\\
	\hline
	B类钢管&25&35&70&45\\
	\hline
\end{tabular}
\end{center}

钢厂在切割钢管时，要求每种钢管的切割模式都不能超过 5 种，请建立数学模型解决
下列问题：
（1）在满足订单要求的前提下，如何切割才能使余料最省；
（2）在满足订单要求的前提下，如何切割才能使耗费原料钢管的数量最少；
（3）如果 B 类钢管的单价是 A 类钢管的 2.5 倍，目前钢管厂 B 类钢管产量不足，如
果客户要求将 B 类钢管中的 5 米、7 米和 8 米三种长度的订货量必须全部满足，而 B
类 3 米的订货量可以有不超过 40\%的部分用 A 类代替，又该如何切割，才能使钢厂的
收益最大，给出替代比例与最大收益之间的关系
	


\section{问题分析}
对于原料下料问题首先要确定采用哪些合理的切割模式。本题要求每种钢管的切
割模式都不能超过 5 种，于是问题便转化为在满足客户需要的条件下，求出有哪几
种合理的模式，每种模式切割多少根原料钢管最为节省。而所谓节省，可以有两种标
准，一是切割后剩余的总余料量最省，二是切割原料钢管的总根数最省。

\subsection{问题一}

对于原料下料问题首先要确定采用哪些合理的切割模式。本题要求每种钢管的切
割模式都不能超过 5 种，于是问题便转化为在满足客户需要的条件下，求出有哪几
种合理的模式，每种模式切割多少根原料钢管最为节省。而所谓节省，可以有两种标
准，一是切割后剩余的总余料量最省，二是切割原料钢管的总根数最省。

\subsection{问题二}

第二问，即为解决总根数最少的情况。我们还是运用整数规划模型，但以最少原
料根数为目标函数，运用线性规划和非线性规划算法求出最优解。。

\subsection{问题三}

第三问，我们站在钢厂的角度，在考虑成本及实际情况的基础上，用一部分 A 类
钢管替代 B 类钢管生产 3 米的成品钢管。我们计划运用双目标规划模型， 分别以
钢厂收益和 B 类钢管可生产出的长度为 3 米的成品钢管根数为自变量建立目标函
数求解。

%\subsection{问题四}

%为验证问题三所给出的预测方法，在给定数据集下，首先利用问题二所给出的调度模型进行调度，并观察调度后利润与阈值对比图，若绝大多数时间段利润都在阈值上方，说明问题二的模型调度方案合理。并代入问题三预测模型进行预测，若在可接受误差范围，则说明问题三所给的预测模型是正确的。


\section{模型的假设}

本文提出以下合理假设：

\begin{itemize}
\item 假设进行钢管切割时不会出现额外的损耗；

\end{itemize}

假设在问题求解过程中不会出现订货量的更改

假设切割的钢管均为合格品

 假设原料钢管与订单要求所需钢管大小一致

\section{符号说明}
\begin{center}
\begin{tabular}{cc}
 \toprule[1.5pt]
 \makebox[0.3\textwidth][c]{符号}	&  \makebox[0.4\textwidth][c]{意义} \\
 \midrule[1pt]
 $ x_i $	    	& 表示按第 i种模式切割下的原料钢管根数   \\ 
 $ x_ji $	    & 表示第 种模式下一根钢管切割得到的第j种长度钢管根数  \\ 
 $ l_i $	    	& 表示第i 种模式下的余料 \\ 
 $ m_i $	   	& 表示采用表中的第i种切割方式 \\  
 $ n_i $	    & 表示采用表中的第i种切割方式 \\ 
 $ p $	    & 表示用 A 类钢管代替 B 类订货量的比例 \\ 
 $ MinZ $   &表示所求某种量的最小值\\
\bottomrule[1.5pt]
\end{tabular}
\end{center}

\section{模型建立与求解}

%\subsection{定义高峰和平峰}

%由题注记可以进行一下定义：

%阈值$W_0$：区分高峰和低峰的一个临界值：691；

%高峰：正常时段，定义为运营总收入与运营总成本之差不小于$W_0$的时段；

%平峰：定义为运营总收入与运营总成本之差小于$W_0$的时段。

%\subsection{排队论证明定义合理性}

%(1)模型说明

%为证明上诉定义合理，我们将该定义放入具体的数据中证明。

%假定某条道路一辆车的成本为200元，一人收价为1元，车载人数为84人，发车间隔为5min，则一小时内该线路共有12量正在运行车辆。按照定义阈值$W_0 = 691$，则我们可以计算出此时总人流量$P = 691 + 12 \times 200 = 3091$。进而该问题便转换为排队论中的单服务台混合制模型 \cite{司守奎} ，通过判断在给定条件下计算出的顾客损失率来验证前面阈值的定义是否合理。

%若在该阈值下，顾客损失率刚好小于1，即顾客恰好不用等待下一辆，因此说明此时刚好处于高峰和低峰段的临界值，验证其合理性。

%排队论是专门研究由于随机因素的影响而产生的拥挤现象的科学，凡是要求服务的对象统称为“顾客”，提供服务的统称为“服务台”。 顾客与服务台构成一个随机服务系统或 称排队系统。 我们将需要乘车的人员作为“顾客”，提供乘车服务的车辆作为“服务台”。

%讲解图片点以及引用

首先要确定采用哪种切割模式是可行的。所谓切割模式，是按照实际需要在原料上安排切割组合。确定哪些切割模式是合理的。通常假设一个合理切割模式的余料应该小于客户需要的钢管的最小尺寸。本文使用MATLAB对切割模式进行了求解，得到了初始切割模式如下表所示：

%\begin{figure}[H]
	%\caption{问题一模型示意图}
	%\label{paiduimx}
	%\centering
	%\includegraphics[width=.6\textwidth]{排队论模型.png}
%\end{figure}

%如图\ref{paiduimx}所示，在给定“阈值”的情况下，若此时顾客损失率刚好小于1，说明此时顾客数量处于刚好不拥堵的情况；高于此阈值，顾客只能等待下一辆车，则将会出现高峰现象；同理，低于此阈值，则说明此时的顾客都能乘车，为平峰状态。

%(2)模型建立

%单服务台混合制模型 \cite{司守奎} M/M/1/K 是指：顾客的相继到达时间服从参数为$\lambda$的负指数分布，服务台个数为1，服务时间 V 服从参数为 $\mu$ 的负指数分布，系统的空间为 K ，当 K 个位置已被顾客占用时，新到的顾客自动离去，当系统中有空位置时，新到的顾客进入系统排队等待。在此模型基础上可以得到下列公式：

%讲解公式以及引用

\begin{table}[htbp]
	\centering
	\caption{A类钢管满足条件的初始切割模式}\label{table-score}
	\begin{tabular}{|l| c| c| c| c| r|}
		\hline
		序号&3m钢管根数&5m钢管根数&7米钢管根数&8m钢管根数&余料\\
		\hline
		1&0&1&2&0&0\\
		\hline
		2&0&2&0&1&1\\
		\hline
		3&0&2&1&0&2\\
		\hline
		4&1&0&0&2&0\\
		\hline
		5&1&0&1&1&1\\
		\hline
		6&1&0&2&0&2\\
		\hline
		7&1&1&0&0&1\\
		\hline
		8&2&1&0&1&0\\
		\hline
		9&2&1&1&0&1\\
		\hline
		10&3&0&0&1&2\\
		\hline
		11&3&2&0&0&0\\
		\hline
		12&4&0&1&0&0\\
		\hline
		13&4&1&0&0&2\\
		\hline
		14&6&0&0&0&1\\
		\hline
		\end{tabular}
	\end{table}
%表一

\begin{longtable}{cccccc}
	\caption{B类钢管满足条件的初始切割模式}\label{table-score}\\
	\toprule
	序号&3m钢管根数&5m钢管根数&7米钢管根数&8m钢管根数&余料\\ 
	\midrule
	\endfirsthead
	
	% “后续页面”表头显示内容
	\multicolumn{6}{c}{续B类钢管满足条件的初始切割模式}\\
	\toprule
	序号&3m钢管根数&5m钢管根数&7米钢管根数&8m钢管根数&余料\\
	\midrule
	%\midrule
	\endhead
	
	% 表格“尾页前”，表格最后显示内容
	\bottomrule
	\multicolumn{6}{c}{接下页}\\
	\endfoot
	
	% 表格“尾页”，表格最后显示内容
	\bottomrule
	\endlastfoot
	
	
	
	1&0&0&3&1&0\\
	
	2&0&0&4&0&1\\
	
	3&0&1&0&3&0\\
	
	4&0&1&1&2&1\\
	
	5&0&1&2&1&2\\
	
	6&0&3&2&0&0\\
	
	7&0&4&0&1&1\\
	
	8&0&4&1&0&2\\
	
	9&1&0&0&3&2\\
	
	10&1&1&3&0&0\\
	
	11&1&2&0&2&0\\
	
	12&1&2&1&1&1\\
	
	13&1&2&2&0&2\\
	
	14&1&5&0&0&1\\
	
	15&2&0&1&2&0\\
	
	16&2&0&2&1&1\\
	
	17&2&0&3&0&2\\
	
	18&2&1&0&2&2\\
	
	19&2&3&0&1&0\\
	
	20&2&3&1&0&1\\
	
	21&3&1&1&1&0\\
	
	22&3&1&2&0&1\\
	
	23&3&2&0&1&2\\
	
	24&3&4&0&0&0\\
	
	25&4&0&0&2&1\\
	
	26&4&0&1&1&2\\
	
	27&4&2&1&0&0\\
	
	28&4&3&0&0&2\\
	
	29&5&0&2&0&0\\
	
	30&5&1&0&1&1\\
	
	31&5&1&1&0&2\\
	
	32&6&2&0&0&1\\
	
	33&7&0&0&1&0\\
	
	34&7&0&1&0&1\\
	
	35&8&1&0&0&0\\
	
	36&9&0&0&0&2\\
	
\end{longtable}


本文经过合理性假设，对两类钢管的切割模式进行优化，优化后的切割模式情况
如下表所示。问题就转化为在满足客户需要的条件下，按照哪几种合理的模式，切
割多少根钢管最为节省。而所谓节省，可以有两种标准：切割后剩余的总余料量最
少或切割原料钢管的总根数最少。下面将对这两个目标分别讨论。


%\begin{equation}
	%\label{gkssl}
	%p_{n} =\rho^{n} p_{0}, \quad n=1,2, \cdots, K 
%\end{equation}

%其中：
%\begin{align*}
%	p_{0} &=\frac{1}{1+\sum_{n=1}^{K} \rho^{n}}=\left\{\begin{array}{ll}
		%\frac{1-\rho}{1-\rho^{K+1}}, & \rho \neq 1 \\
		%\frac{1}{K+1}, & \rho=1
	%\end{array}\right. \\
	%\lambda_{n} &=\left\{\begin{array}{ll}
		%\lambda, & n=0,1,2, \cdots, K-1 \\
		%0, & n \geq K
	%\end{array}\right. \\
%	\mu_{n} &=\mu, \quad n=1,2, \cdots, K
%\end{align*}

%(3)模型求解

%在$W_0 = 691 \quad W = 3091$ 的条件下，查阅相关文献\cite{__2018}可得此时一站台最高人数大约为总人数的$\frac{1}{3}$，即K=1020，最终计算此时的顾客损失率。排队论计算各参数值如表\ref{table_gk}：

%这里讲述一下普通表格的引用以及改变

\begin{table}[H]
	\centering
	\caption{优化后A 类钢管满足条件的切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		1&1&0&0&2&0	\\ 		
		2&0&2&0&1&1	\\ 
		3&0&1&2&0&0  \\
		4&3&2&0&0&0	\\ 
		5&0&2&1&0&2\\
		6&1&3&0&0&1\\
		7&2&1&0&1&0\\
		8&3&0&0&1&1\\
		9&1&0&1&1&2\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}

%可以得到此时的顾客损失率为：$ 0.0118 $。说明当$W_0 = 691$，此时一辆车载人数为84人，顾客损失率刚好不超过一个人，不会出现乘客无法乘车的现象。若高于此阈值，顾客损失率大于一，将会出现高峰；若小于此阈值，顾客损失率小于一，处于平峰区，说明此阈值定义合理。




\begin{table}[H]
	\centering
	\caption{ 优化后B 类钢管满足条件的切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		1&0&0&3&1&0	\\ 		
		2&0&1&0&3&0	\\ 
		3&7&0&0&1&0  \\
		4&3&4&0&0&0	\\ 
		5&8&1&0&0&0\\
		6&1&1&3&0&0\\
		7&2&3&0&1&0\\
		8&0&3&2&0&0\\
		9&1&2&0&2&0\\
		10&3&1&1&1&0\\
		11&4&2&1&0&0\\
		12&5&0&2&0&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}
%\section{问题一}

\subsection{问题一：余料最省的问题}

为方便表示方程，

可设：$ x_i $为按第
i种模式切割下的原料钢管根数（i=1，2，3，4，5）

$r_ji$为第i种模式切割下得到的第j种长度钢管根数（i=1，2，3，4，5）

$l_i$为第i种模式下的余料（i=1,2,3,4,5）

$m_i$为采用上述表3中的第i种切割方式(i=1,2,3,...,9)

$n_i$为采用上述表 4 中的第i种切割方式(i=1,2,3,...,12)

%\begin{table}[H]
%	\centering
%	\caption{该路段不同时间的人流量}
%	\label{table_rll}
%	\begin{tabular}{cccccccc}
%		\toprule[1.5pt]
%		时间段         & 6:00-7:00   & 7:00-8:00   & 8:00-9:00   & 9:00-10:00  & 10:00-11:00 \\
%		线路所有站的总上车人数P & 3279        & 4271        & 4513        & 3589        & 2512        \\
%		\midrule[1pt]
%		时间段         & 11:00-12:00 & 12:00-13:00 & 13:00-14:00 & 14:00-15:00 & 15:00-16:00 \\
%		线路所有站的总上车人数P & 2457        & 2212        & 1895        & 1923        & 2278        \\
%		\midrule[1pt]
%		时间段         & 16:00-17:00 & 17:00-18:00 & 18:00-19:00 &  \quad           &  \quad          \\
%		线路所有站的总上车人数P & 2457        & 3151        & 4176        &  \quad          & \quad   \\
%		\bottomrule[1.5pt]
%	\end{tabular}
%\end{table}

分析题目可列出两类钢管的约束方程组如下：

A 类钢管的约束条件方程组
%\begin{figure}[H]
%	\caption{调度前该路段车辆运行示意图}
%	\label{diaoduqian}
%	\centering
%	\includegraphics[width=.6\textwidth]{调度前.png}
%\end{figure}
\begin{gather}
\left\{\begin{array}{l}
	r_{11} x_{1}+r_{12} x_{2}+r_{13} x_{3}+r_{14} x_{4}+r_{15} x_{5} \geq 30 \\
	r_{21} x_{1}+r_{22} x_{2}+r_{23} x_{3}+r_{24} x_{4}+r_{25} x_{5} \geq 70 \\
	r_{31} x_{1}+r_{32} x_{2}+r_{33} x_{3}+r_{34} x_{4}+r_{35} x_{5} \geq 40 \\
	r_{41} x_{1}+r_{42} x_{2}+r_{43} x_{3}+r_{44} x_{4}+r_{45} x_{5} \geq 60
\end{array}\right.
\end{gather}
B 类钢管的约束条件方程组
%\begin{align*}
%	& \text{阈值为：} W_0 = 691 \text{元} \\
%	& \text{高峰： }  W \geq W_0  \\
%	& \text{低峰： }  W < W_0 
%\end{align*}
\begin{gather}
\left\{\begin{array}{l}
	r_{11} x_{1}+r_{12} x_{2}+r_{13} x_{3}+r_{14} x_{4}+r_{15} x_{5} \geq 25 \\
	r_{21} x_{1}+r_{22} x_{2}+r_{23} x_{3}+r_{24} x_{4}+r_{25} x_{5} \geq 35 \\
	r_{31} x_{1}+r_{32} x_{2}+r_{33} x_{3}+r_{34} x_{4}+r_{35} x_{5} \geq 70 \\
	r_{41} x_{1}+r_{42} x_{2}+r_{43} x_{3}+r_{44} x_{4}+r_{45} x_{5} \geq 45
\end{array}\right.
\end{gather}

%未调度之前，我们通过拟合每个时段的利润W，并与阈值$W_0$进行对比，可得到图\ref{ddqyz}：
%\begin{figure}[H]
%	\caption{调度前该路段各时间段利润与阈值对比图}
%	\label{ddqyz}
%	\centering
%	\includegraphics[scale=0.4]{未调度前分布.png}
%\end{figure}
%从图中我们可以看出各时间段的W分布在阈值上下，而在阈值下方的时间段，无论是从乘客上车率角度还是车辆收益角度，我们应该对此时的车辆分配方案做出适当调整，使得在平峰段的W尽可能在$W_0$界限上方。

分析题目可列出线性规划的目标函数如下：
\begin{gather}
\operatorname{Min} Z_{1}=l_{1} x_{1}+l_{2} x_{2}+l_{3} x_{3}+l_{4} x_{4}+l_{5} x_{5}
\end{gather}

将上述条件转化为矩阵运算如下:
\begin{gather}
\left\{\begin{array}{l}
	{[x]_{4 \times 9} \cdot\left[\begin{array}{l}
			m_{1} \\
			m_{2} \\
			\cdots \\
			m_{9}
		\end{array}\right]_{9 \times 1} \geq\left[\begin{array}{c}
			30 \\
			70 \\
			40 \\
			60
		\end{array}\right]} \\
	{[y]_{4 \times 12}\left[\begin{array}{l}
			n_{1} \\
			n_{2} \\
			\cdots \\
			n_{9}
		\end{array}\right]_{12 \times 1} \geq\left[\begin{array}{c}
			25 \\
			35 \\
			70 \\
			45
		\end{array}\right]}
\end{array}\right.
\end{gather}
其中  m, n  全为整数且  
\begin{gather}
m, n \geq 0 
\end{gather}

编写 MATLAB 代码并运行得到线性规划方案如下表所示：

\begin{table}[H]
	\centering
	\caption{A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{A类}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		第一种&1&0&0&2&0	\\ 		
		第二种&0&2&0&1&1	\\ 
		第三种&0&1&2&0&0  \\
		第四种&3&2&0&0&0	\\ 
		第五种&0&2&1&0&2\\
	\bottomrule[1.5pt]		
	\end{tabular}
\end{table}


\begin{table}[H]
	\centering
	\caption{A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{B类}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		第一种&0&0&3&1&0	\\ 		
		第二种&1&1&3&0&	\\ 
		第三种&0&1&0&3&0  \\
		第四种&8&1&0&0&0	\\ 
		第五种&3&1&1&1&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}

即需 A 类钢管 65 根，采用第一种切割模式切割 20 根、第二种 20 根，第三种 20 根，第四种 5 根，第五种 0 根，余料共 20 米;即需 B 类钢管 40 根，采用第一种切割模式切割 0 根、第二种 25 根，第三种15 根，
第四种 0 根，第五种 0 根，无余料。
\subsection{问题二：耗费钢管数最少的问题}

为方便表示方程，

可设：$ x_i $为按第
i种模式切割下的原料钢管根数（i=1，2，3，4，5）

$r_ji$为第i种模式切割下得到的第j种长度钢管根数（i=1，2，3，4，5）

$l_i$为第i种模式下的余料（i=1,2,3,4,5）

$m_i$为采用上述表3中的第i种切割方式(i=1,2,3,...,9)

$n_i$为采用上述表 4 中的第i种切割方式(i=1,2,3,...,12)

A 类钢管的约束条件方程组
\begin{gather}
	\left\{\begin{array}{l}
		r_{11} x_{1}+r_{12} x_{2}+r_{13} x_{3}+r_{14} x_{4}+r_{15} x_{5} \geq 30 \\
		r_{21} x_{1}+r_{22} x_{2}+r_{23} x_{3}+r_{24} x_{4}+r_{25} x_{5} \geq 70 \\
		r_{31} x_{1}+r_{32} x_{2}+r_{33} x_{3}+r_{34} x_{4}+r_{35} x_{5} \geq 40 \\
		r_{41} x_{1}+r_{42} x_{2}+r_{43} x_{3}+r_{44} x_{4}+r_{45} x_{5} \geq 60
	\end{array}\right.
\end{gather}
B 类钢管的约束条件方程组

\begin{gather}
	\left\{\begin{array}{l}
		r_{11} x_{1}+r_{12} x_{2}+r_{13} x_{3}+r_{14} x_{4}+r_{15} x_{5} \geq 25 \\
		r_{21} x_{1}+r_{22} x_{2}+r_{23} x_{3}+r_{24} x_{4}+r_{25} x_{5} \geq 35 \\
		r_{31} x_{1}+r_{32} x_{2}+r_{33} x_{3}+r_{34} x_{4}+r_{35} x_{5} \geq 70 \\
		r_{41} x_{1}+r_{42} x_{2}+r_{43} x_{3}+r_{44} x_{4}+r_{45} x_{5} \geq 45
	\end{array}\right.
\end{gather}


分析题目可列出线性规划的目标函数如下：
\begin{gather}
	\operatorname{Min} Z_{2}=\sum_{i=1}^{5} x_i
\end{gather}

将上述条件转化为矩阵运算如下:
\begin{gather}
	\left\{\begin{array}{l}
		{[x]_{4 \times 9} \cdot\left[\begin{array}{l}
				m_{1} \\
				m_{2} \\
				\cdots \\
				m_{9}
			\end{array}\right]_{9 \times 1} \geq\left[\begin{array}{c}
				30 \\
				70 \\
				40 \\
				60
			\end{array}\right]} \\
		{[y]_{4 \times 12}\left[\begin{array}{l}
				n_{1} \\
				n_{2} \\
				\cdots \\
				n_{9}
			\end{array}\right]_{12 \times 1} \geq\left[\begin{array}{c}
				25 \\
				35 \\
				70 \\
				45
			\end{array}\right]}
	\end{array}\right.
\end{gather}
其中  m, n  全为整数且  
\begin{gather}
	m, n \geq 0 
\end{gather}

在模型的求解过程中，由于可行解较多，考虑到钢厂的实际生产模式和收支平衡，故
我们在原有模型的基础上增加了约束条件：即分成有预料和无余料两种情况求的较优
解。
编写 MATLAB 代码并运行得到线性规划方案如下表所示：

有余料时：
\begin{table}[H]
	\centering
	\caption{有余料A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{A类}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		第一种&0&1&2&0&0	\\ 		
		第二种&1&0&1&1&1	\\ 
		第三种&6&0&0&0&1  \\
		第四种&0&2&0&1&1	\\ 
		第五种&1&0&0&2&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}

\begin{table}[H]
	\centering
	\caption{有余料B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{A类}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		第一种&7&0&0&1&0	\\ 		
		第二种&0&1&0&3&0	\\ 
		第三种&0&0&4&0&1  \\
		第四种&1&1&3&0&0	\\ 
		第五种&5&0&2&0&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}
需 A 类钢管 65 根，采用第一种切割模式切割 20 根、第二种 1 根，第三种 2
根，第四种 25 根，第五种 17 根，余料共 2 米。
需 B 类钢管 38 根，采用第一种切割模式切割 0 根，第二种 15 根，第三种 2
根，第四种 20 根，第五种 1 根，余料共 2 米。

无余料时

\begin{table}[H]
	\centering
	\caption{无余料A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{A类}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		第一种&2&1&0&1&0	\\ 		
		第二种&1&0&0&2&0	\\ 
		第三种&2&1&0&1&0  \\
		第四种&2&1&0&1&0	\\ 
		第五种&0&1&2&0&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}

\begin{table}[H]
	\centering
	\caption{无余料B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{A类}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 余料（米）} 
		\\ 
		\midrule[1pt]		
		第一种&2&130&1&0	\\ 		
		第二种&0&3&2&0&0	\\ 
		第三种&1&2&0&2&0  \\
		第四种&0&0&3&1&0	\\ 
		第五种&4&2&1&0&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}
需 A 类钢管 75 根，采用第一种切割模式切割 0 根、第二种 5 根、第三种或第四
种 50 根、第五种 20 根，无余料。
需 B 类钢管 39 根，采用第一种切割模式切割 1 根、第二种 12 根、第三种
21 根、第四种 5 根、第五种 0 根，无余料。
%为使得在乘客数下降和恢复的过程中，通过相应地减少和恢复投入运营的车辆数量来保证这个“阈值”界限不被突破，而盈利的“上界”是不受限的。在从高峰段到低峰段的调度时，选择5min间隔发车-->5/10min间隔交替发车-->10min间隔发车；在从低峰段到高峰段的调度时，则选择与之相反调度。具体调度时刻点如下图 \ref{diaoduhou1} 和 图 \ref{diaoduhou2} 所示：
%多个图片排版问题 以及小标题与大标题还有引用的注意点


%\begin{figure}[H]
%	\caption{高峰区到低峰区的调度示意图}
%	\label{diaoduhou1}
%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
%			\centering
%			\includegraphics[scale=0.25]{调度1.png}
%		\end{minipage}
%	} \quad \quad \quad \quad \quad \quad \quad 
%	\subfigure
	{
%		\begin{minipage}[b]{.3\linewidth}
%			\includegraphics[scale=0.25]{调度2.png}
%		\end{minipage}
%	}

%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
			
%			\includegraphics[scale=0.25]{调度3.png}
%		\end{minipage}
%	} \quad \quad \quad \quad \quad \quad \quad
%	\subfigure
%	{
%	\begin{minipage}[b]{.3\linewidth}
%		\includegraphics[scale=0.25]{调度4.png}
%	\end{minipage}
%	}
%\end{figure}

%\begin{figure}[H]
%	\caption{低峰区到高峰区的示意图}
%	\label{diaoduhou2}
%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
%			\centering
%			\includegraphics[scale=0.25]{调度5.png}
%		\end{minipage}
%	} \quad \quad \quad \quad \quad \quad \quad 
%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
%			\includegraphics[scale=0.25]{调度6.png}
%		\end{minipage}
%	}
%	
%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
			
%			\includegraphics[scale=0.25]{调度7.png}
%		\end{minipage}
%	} \quad \quad \quad \quad \quad \quad \quad
%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
%			\includegraphics[scale=0.25]{调度8.png}
%		\end{minipage}
%	}

%	\subfigure
%	{
%		\begin{minipage}[b]{.3\linewidth}
%			\includegraphics[scale=0.25]{调度9.png}
%		\end{minipage}
%	}
%\end{figure}

%上图\ref{diaoduhou1}和图\ref{diaoduhou2}中的线段间隔代表5min，高峰区到低峰区的调度如下：


\subsection{问题三：收益最大的问题}
为方便表示方程，

可设：$ x_i $为按第
i种模式切割下的原料钢管根数（i=1，2，3，4，5）

$r_ji$为第i种模式切割下得到的第j种长度钢管根数（i=1，2，3，4，5）

$m_i$为采用上述表3中的第i种切割方式(i=1,2,3,...,9)

$n_i$为采用上述表 4 中的第i种切割方式(i=1,2,3,...,12)

P为用A类钢管代替B类订货量的比例（$p\leq0.4$）
分析题目可列出两类钢管的约束方程组如下：

A 类钢管的约束条件方程组

\begin{gather}
	\left\{\begin{array}{l}
		r_{11} x_{1}+r_{12} x_{2}+r_{13} x_{3}+r_{14} x_{4}+r_{15} x_{5} \geq 55p \\
		r_{21} x_{1}+r_{22} x_{2}+r_{23} x_{3}+r_{24} x_{4}+r_{25} x_{5} \geq 70 \\
		r_{31} x_{1}+r_{32} x_{2}+r_{33} x_{3}+r_{34} x_{4}+r_{35} x_{5} \geq 40 \\
		r_{41} x_{1}+r_{42} x_{2}+r_{43} x_{3}+r_{44} x_{4}+r_{45} x_{5} \geq 60
	\end{array}\right.
\end{gather}
B 类钢管的约束条件方程组

\begin{gather}
	\left\{\begin{array}{l}
		r_{11} x_{1}+r_{12} x_{2}+r_{13} x_{3}+r_{14} x_{4}+r_{15} x_{5} \geq 25-25p \\
		r_{21} x_{1}+r_{22} x_{2}+r_{23} x_{3}+r_{24} x_{4}+r_{25} x_{5} \geq 35 \\
		r_{31} x_{1}+r_{32} x_{2}+r_{33} x_{3}+r_{34} x_{4}+r_{35} x_{5} \geq 70 \\
		r_{41} x_{1}+r_{42} x_{2}+r_{43} x_{3}+r_{44} x_{4}+r_{45} x_{5} \geq 45
	\end{array}\right.
\end{gather}



分析题目可列出线性规划的目标函数如下：
\begin{gather}
	\operatorname{Min} Z_{3}=q_1+2.5q_2
\end{gather}

编写 Lingo 代码并运行得到线性规划方案如下表所示：

(1)p=0.4时，$MinZ_3$=159

\begin{table}[H]
	\centering
	\caption{p = 0.4时A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&2&1&1&0&0	\\ 		
		2&1&3&0&0&13	\\ 
		3&0&2&0&1&6  \\
		4&1&0&0&2&27	\\ 
		5&0&1&2&0&20\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}


\begin{table}[H]
	\centering
	\caption{p=0.4  B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&1&2&1&1&0	\\ 		
		2&1&1&3&0&3\\ 
		3&0&3&2&0&2  \\
		4&1&2&0&2&13	\\ 
		5&0&0&3&1&19\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}
为了求出替代比例与最大收益之间的关系，我们分别给p赋值， 运用 Lingo 软件求得：

(2)p=0时，$MinZ_3$=160


\begin{table}[H]
	\centering
	\caption{p = 0时A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&0&2&0&1&12	\\ 		
		2&1&1&3&0&8	\\ 
		3&1&0&0&2&24  \\
		4&0&1&2&0&20	\\ 
		5&3&2&0&0&1\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}


\begin{table}[H]
	\centering
	\caption{p=0时B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&0&1&0&3&14	\\ 		
		2&1&1&3&0&20\\ 
		3&3&1&1&1&0  \\
		4&5&1&1&0&1	\\ 
		5&0&0&3&1&3\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}

(3)p=0.1时，$MinZ_3$=160


\begin{table}[H]
	\centering
	\caption{p = 0.1时A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&1&0&0&2&19	\\ 		
		2&0&2&0&1&20	\\ 
		3&0&1&2&0&20  \\
		4&1&0&0&2&1	\\ 
		5&3&2&0&0&5\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}


\begin{table}[H]
	\centering
	\caption{p=0.1时B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&2&0&2&1&2	\\ 		
		2&1&2&0&2&14\\ 
		3&0&0&3&1&0  \\
		4&1&1&3&0&7	\\ 
		5&0&0&3&1&15\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}
(4)p=0.2时，$MinZ_3$=160


\begin{table}[H]
	\centering
	\caption{p = 0.2时A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&0&1&2&0&0	\\ 		
		2&2&1&0&1&10	\\ 
		3&0&2&0&1&20  \\
		4&0&1&2&0&20	\\ 
		5&1&0&0&2&15\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}


\begin{table}[H]
	\centering
	\caption{p=0.2时B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&0&0&3&1&15	\\ 		
		2&0&0&4&0&3\\ 
		3&0&1&2&1&0  \\
		4&1&2&0&2&15	\\ 
		5&1&1&3&0&5\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}
(5)p=0.3时，$MinZ_3$=160


\begin{table}[H]
	\centering
	\caption{p = 0.3时A 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&3&2&0&0&6	\\ 		
		2&0&1&2&0&20	\\ 
		3&1&0&0&2&21  \\
		4&0&2&0&1&19	\\ 
		5&6&0&0&0&0\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}


\begin{table}[H]
	\centering
	\caption{p=0.3时B 类钢管的 5 种切割模式}
	\label{table_gk}
	\begin{tabular}{cccccc}
		\toprule
		\makebox{序号}	&  \makebox{3m钢管根数} &
		\makebox{5m钢管根数}	&  \makebox{7m钢管根数} &
		\makebox{8m钢管根数}	&  \makebox{ 根数）} 
		\\ 
		\midrule[1pt]		
		1&0&3&2&0&2	\\ 		
		2&0&0&3&1&22\\ 
		3&2&3&0&1&5 \\
		4&0&0&4&0&9	\\ 
		5&1&2&0&2&9\\
		\bottomrule[1.5pt]		
	\end{tabular}
\end{table}

结合上面几个表，对p与 $MinZ_3$进行多项式拟合，最总得出四次拟合较合适，得下图
\begin{figure}[H]
	\caption{拟合函数}
	\label{yd}
	\centering
	\includegraphics[scale=0.4]{HLY.png}
\end{figure}
由上图我们可以得出p与$MinZ_3$的关系如下：
$MinZ_3$=-20.83.3$p^4$+1416.7$p^3$-279.17$P^2$=15.833P+160
%(2)最优性分析

%对所给数据进行步长为1的遍历，并将遍历得到的可行域与调度方案后的分布曲线进行分析，如下图：

%\begin{figure}[H]
%	\caption{可行域示意图}
%	\label{kxy}
%	\centering
%	\includegraphics[scale=0.4]{可行域.png}
%\end{figure}

%上图中，蓝色区域为可行域，红色曲线为给定数据，在该可行域内该调度方案都是可行且最优的。

%\subsection{调度方案灵敏性与敏感性分析}

%由于利润与总人流量间满足$W = P - x \times 200$，分析人流量对某时间段利润的敏感程度$S(P,W)$。

%\begin{equation}
%	S(P,W) =\frac{d P}{d W} \cdot \frac{W}{P}=\frac{W}{P}
%\end{equation}

%带入表\ref{table_rll}可得$S(P,W) = 0.33 $，则说明调度之后人流量对利润不敏感，进一步说明了调度方案对人流量是比较稳定的。


%\section{问题三的模型建立与求解}

%\subsection{模型建立}

%根据所选择数据的特点，采取时间时序模型的简单移动平均法。其模型示意图如下图：

%\begin{figure}[H]
%	\caption{移动平均法示意图}
%	\label{yd}
%	\centering
%	\includegraphics[scale=0.4]{问题三模型图.png}
%\end{figure}

%(1)高峰预测

%在第一次平峰到高峰时间段的数据为研究对象，依次计算在此基础上，以间隔上一起始点5min的点作为下一起始点，计算往后一个小时的上车人数。随后采用移动平均法，直到预测到某个时刻第一次出现$W \geq W_0$，则说明到达下一个高峰。

%(2)低峰预测

%以高峰到平峰时间段的数据为研究对象，依次计算在此基础上，以间隔上一起始点5min的点作为下一起始点，计算往后一个小时的上车人数。随后采用移动平均法，直到预测到某个时刻第一次出现$W \leq W_0$，则说明到达下一个低峰。

%\subsection{模型求解}

%由于到达站点的人群时平均到达，因此我们将观测序列设为$y_1,y_2,\dots,y_T$，取移动平均的项数N<T。则一次简单移动的平均值为$M_t^{(1)}$：

%\begin{equation}
%	\label{1}
%	\begin{aligned}
%		M_{t}^{(1)} &=\frac{1}{N}\left(y_{t}+y_{t-1}+\cdots+y_{t-N+1}\right) \\
%		&=\frac{1}{N}\left(y_{t-1}+\cdots+y_{t-N}\right)+\frac{1}{N}\left(y_{t}-y_{t-N}\right)=M_{t-1}^{(1)}+\frac{1}{N}\left(y_{t}-y_{t-N}\right)
%\end{aligned}
%\end{equation}

%建立预测模型 $\hat{y}_{t+1}$ ：

%\begin{equation}
%	\label{2}
%	\hat{y}_{t+1}=M_{t}^{(1)}=\frac{1}{N}\left(y_{t}+\cdots+y_{t-N+1}\right), t=N, N+1, \cdots, T
%\end{equation}

%其预测标准差为S：

%\begin{equation}
%	\label{3}
%	S=\sqrt{\frac{\sum_{t=N+1}^{T}\left(\hat{y}_{t}-y_{t}\right)^{2}}{T-N}}
%\end{equation}

%\section{问题四}

%(1)数据调度化

%采取有关文件中一组实际数据(见附件一)带入问题二所建立的调度模型，对该数据进行调度，使得每一时间段的利润都高于阈值，并得到调度后的利润与阈值对比图如下图\ref{wtsddh}：

%\begin{figure}[H]
%	\caption{实际数据调度后各时间段利润与阈值对比图}
%	\label{wtsddh}
%	\centering
%	\includegraphics[scale=0.4]{问题三调度后分布图.png}
%\end{figure}

%如上图所示，可以看到绝大多数时间段的利润都高于阈值，则证明调度方案是合理的。

%(2)问题三基础上的高低峰预测结果

%将调度后的分布情况，带入\ref{1}、\ref{2}、\ref{3}可得到：

%$$ \text{预测值：高峰时间点：} 6:30 \quad \text{平峰时间点：} 18:50$$

%(3)预测值与实际值比较

%$$ \text{实际值：高峰时间点：} 7:00 \quad \text{平峰时间点：} 19:00$$
%
%可以看到预测方法得出的数据基本符合实际数据，说明问题三所给的预测方法是合理的。


%\section{优缺点分析}

%\subsection{优点}

%(1)问题二所给的调度方案是分步调度，相较于一步调度，更难提高利润和乘客上车率。

%(2)问题二所给出的调度方案很好的将每个时间段的收益都调度到了阈值界限上方。

%\subsection{缺点}

%(1)优化区域求解采用遍历法，求解效率低。

%(2)论文结论仅局限于此环境。

%最后采用的是外面导入bib文件形式
%\bibliography{book}

\section{模型评价}

在处理问题的时候我们采用合理的假设舍去了较多的方法极大的简化了问题，
为我们求解答案提供了便利。
\subsection{模型缺点}
1．在处理问题的时候我们采用合理的假设舍去了较多的方法极大的简化了问题，但因此实验结果也存在可信度降低的问题。

2．由于问题的可行解非常多，我们在处理问题的时候，自行添加了一些条件，虽然就实际情况而言相对合理，但是就本问题而言，实验结果还是存在一定偏差。
\newpage
%附录
\appendix
\renewcommand{\appendixpagename}{附录}
\renewcommand{\appendixtocname}{附录}
\appendixpage
\addappheadtotoc
\begin{appendices}
	\section[第一个附录]{第一个附录}
	\begin{figure}[H]
		%\caption{拟合函数}
		\label{yd}
		\centering
		\includegraphics[scale=0.4]{MAT1.png}
		
		\begin{figure}[H]
			%\caption{拟合函数}
			\label{yd}
			\centering
			\includegraphics[scale=0.4]{MAT2.png}
		\end{figure}
	\end{figure}
	\section{第二个附录}
	model:
	min=(x1+x2+x3+x4+x5)+2.5*(y1+y2+y3+y4+y5);
	
	r11*x1+r12*x2+r13*x3+r14*x4+r15*x5>=30+25*m;
	
	r11*x1+r12*x2+r13*x3+r14*x4+r15*x5<=55;
	
	r21*x1+r22*x2+r23*x3+r24*x4+r25*x5>=70;
	
	r31*x1+r32*x2+r33*x3+r34*x4+r35*x5>=40;
	
	r41*x1+r42*x2+r43*x3+r44*x4+r45*x5>=60;
	
	3*r11+5*r21+7*r31+8*r41<=19;
	
	3*r12+5*r22+7*r32+8*r42<=19;
	
	3*r13+5*r23+7*r33+8*r43<=19;
	
	3*r14+5*r24+7*r34+8*r44<=19;
	
	3*r15+5*r25+7*r35+8*r45<=19;
	
	
	3*r11+5*r21+7*r31+8*r41>=17;
	
	3*r12+5*r22+7*r32+8*r42>=17;
	
	3*r13+5*r23+7*r33+8*r43>=17;
	
	3*r14+5*r24+7*r34+8*r44>=17;
	
	3*r15+5*r25+7*r35+8*r45>=17;
	
	s11*y1+s12*y2+s13*y3+s14*y4+s15*y5>=25*(1-m);

	s11*y1+s12*y2+s13*y3+s14*y4+s15*y5<=25;
	
	s21*y1+s22*y2+s23*y3+s24*y4+s25*y5>=35;
	
	s31*y1+s32*y2+s33*y3+s34*y4+s35*y5>=70;
	
	s41*y1+s42*y2+s43*y3+s44*y4+s45*y5>=45;
	
	3*s11+5*s21+7*s31+8*s41<=29;
	
	3*s12+5*s22+7*s32+8*s42<=29;
	
	3*s13+5*s23+7*s33+8*s43<=29;
	
	3*s14+5*s24+7*s34+8*s44<=29;
	
	3*s15+5*s25+7*s35+8*s45<=29;
	
	3*s11+5*s21+7*s31+8*s41>=27;
	
	3*s12+5*s22+7*s32+8*s42>=27;
	
	3*s13+5*s23+7*s33+8*s43>=27;
	
	3*s14+5*s24+7*s34+8*s44>=27;
	
	3*s15+5*s25+7*s35+8*s45>=27;
	
	m<=0.4;

	m>=0;
	
	@gin(x1);@gin(x2);@gin(x3);@gin(x4);@gin(x5);
	
	@gin(y1);@gin(y2);@gin(y3);@gin(y4);@gin(y5);
	
	@gin(r11);@gin(r12);@gin(r13);@gin(r14);@gin(r
	15);
	
	@gin(r21);@gin(r22);@gin(r23);@gin(r24);@gin(r
	25);
	
	@gin(r31);@gin(r32);@gin(r33);@gin(r34);@gin(r
	35);
	
	@gin(r41);@gin(r42);@gin(r43);@gin(r44);@gin(r
	45);
	
	@gin(s11);@gin(s12);@gin(s13);@gin(s14);@gin(s
	15);
	
	@gin(s21);@gin(s22);@gin(s23);@gin(s24);@gin(s
	25);
	
	@gin(s31);@gin(s32);@gin(s33);@gin(s34);@gin(s
	35);
	
	@gin(s41);@gin(s42);@gin(s43);@gin(s44);@gin(s
	45); 
	
	end
\end{appendices}

\end{document}
%\section{排队论源代码}
%\begin{lstlisting}[language=lingo]
%	{\colortbl ;\red0\green0\blue255;\red0\green0\blue0;
%	\viewkind4\uc1\pard\cf1\lang2052\f0\fs20 model\cf2 :\par
%	\cf1 sets\cf2 :\par
%	state/1..1020/:p;\par
%	\cf1 endsets\cf2\par
%	lamda=1020/12;mu=84;rho=lamda/mu;k=1020;\par
%	lamda*p0=mu*p(1);\par
%	(lamda+mu)*p(1)=lamda*p0+mu*p(2);\par
%	\cf1 @for\cf2 (state(i)|i #gt#1 #and# i #lt#\par
%	k:(lamda+mu)*p(i)=lamda*p(i-1)+mu*p(i+1));\par
%	lamda*p(k-1)=mu*p(k);\par
%	p0+\cf1 @sum\cf2 (state:p)=1;\par
%	P_lost=p(k);lamda_e=lamda*(1-P_lost);\par
%	L_s=\cf1 @sum\cf2 (state(i)|i #le#k:i*p(i));\par
%	L_q=L_s-(1-p0);\par
%	W_s=L_s/lamda_e;\par
%	W_q=W_s-1/mu;\par
%	\cf1 end\cf2\par
}
% \end{lstlisting}
% \section{未调度利润与阈值对比图}
%\begin{lstlisting}[language=matlab]
%	clear,clc
%	给每个小时间段的人数赋值
%	a=5;b=10;j=0;m=1; %a，b分别为不同的时间间隔
%	s=[3589 2512 2457 2212 1895 1923 2278 2457 3151 4176]; %整点时间的人数
%	A=zeros(1,108);%初始化小时间段人数
%	for i=1:1:9
%	k=1;
%	while j<60
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+a;m=m+1;k=k+1;
%	end
%	j=0;
%	end
	%车辆数
%	c=ones(1,108)*12;
%	c=200*c;
%	x=A-c; %成本-利润
%	B=ones(1,108)*691;
%	plot(x,'b')
%	hold on
%	plot(B,'r')
% \end{lstlisting}
%\section{调度利润与阈值对比图}
%\begin{lstlisting}[language=matlab]
%	function A=dd(s)
	%给每个小时间段的人数赋值
%	a=5;b=10;j=30;m=1; %a，b分别为不同的时间间隔
%	A=zeros(1,58);%初始化小时间段人数
%	for i=1:1:3
%	k=1;
%	while j<60
%	if mod(k,2)==0
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+b;k=k+1;m=m+1;
%	else
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+a;m=m+1;k=k+1;
%	end
%	if (i==3 && j==30)
%	break;
%	end
%	end
%	j=0;
%	end
%	j=30;
%	for i=3:1:6
%	while j<60
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+b;m=m+1;
%	if (i==6 && j==30)
%	break;
%	end
%	end
%	j=0;
%	end
%	j=30;
%	for i=6:1:7
%	k=1;
%	while j<60
%	if mod(k,2)==0
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+b;m=m+1;k=k+1;
%	else
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+a;m=m+1;k=k+1;
%	end
%	end
%	j=0;
%	end
%	j=0;
%	for i=8
%	while j<=60
%	A(m)=s(i)*(60-j)/60+s(i+1)*j/60;
%	j=j+a;m=m+1;
%	end
%	j=0;
%	end
%	车辆数
%	c=[11 11 10 10 9 9 8 8 8 8 8 8 8 8 8 8 8 8 7 7 7 6 6 6 6 6 6 6 6 6 6 6 6 6 6 7 7 7 7 8 8 8 8 8 8 8 8 8 9 9 9 10 10 10 11 11 11 12 12];
%	c=200*c;
%	x=A-c; %成本-利润
%	for i=1:1:59
%	if x(i)>=0
%	minp=x(i);
%	end
%	break
%	end
%	for i=1:1:59
%	l=x(i);
%	if (l<minp && l>=0)
%	minp=l;
%	end
%	end
%	B=ones(1,59)*691;
%	plot(A,'b')
%	 hold on
%	 plot(B,'r')
%	end
%\end{lstlisting}
%\section{灵敏度分析}
%\begin{lstlisting}[language=matlab]
%	clear,clc
%	s1=[3589 2499 2457 2204 1891 1921 2273 2453 3150];
%	s2=[3650 2512 2475 2212 1897 1932 2279 2461 3156];
%	s3=[3598 2512 2457 2212 1895 1923 2278 2457 3151];
%	[y2,x2]=dd(s2);
%	[y1,x1]=dd(s1);
%	dx=x2-x1;
%	dy=y2-y1;
%	s=dy/y2/(dx/x2)
%\end{lstlisting}
%\section{最优解}
%\begin{lstlisting}[language=matlab]
%	clear,clc
%	s1=[3589 2499 2457 2204 1891 1921 2273 2453 3150];
%	s2=[3650 2512 2475 2212 1897 1932 2279 2461 3156];
%	s3=[3598 2512 2457 2212 1895 1923 2278 2457 3151];
%	y1=dd(s1);
%	hold on
%	y2=dd(s2);
%	hold on
%	dd(s3)
%	x1=1:1:59;
%	x2=x1;
%	fill([x1,x2],[y1 y2],'b')
%\end{lstlisting}
