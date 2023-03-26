## 主向量-特解

接下来主要讨论的是长方形的矩阵，例如
$$
A=\begin{pmatrix}
1 & 2 & 2 & 2 \\
2 & 4 & 6 & 8 \\
3 & 6 & 8 & 10
\end{pmatrix}
$$
观察发现，第二列是第一列的倍数。因此他们是线性相关的。对于行来讲第三行等于第一行加上第二行。对此方程组进行消元。
$$
\begin{pmatrix}
1  & 2 & 2 & 2 \\
0 & 0 & 2 & 4 \\
0 & 0 & 2 & 4 
\end{pmatrix}
\to
\begin{pmatrix}
\boxed{1} & 2 & 2 & 2 \\
0 & 0 & \boxed{2} & 4 \\
0 & 0 & 0 & 0
\end{pmatrix}=U
$$
这里的主元（pivots）分别是 $\boxed{1}$ 和 $\boxed{2}$，主元的数量称之为这个矩阵的秩 (rank)。主元所在的列称之为主列 (pivots column)。其他列则称之为自由列。

这里的自由列在求解 $Ux=0$ 时可以自由分配值
$$
\begin{align}
x_{1}+2x_{2}+2x_{3}+2x_{4}&=0 \\
2x_{3}+4x_{4}&=0
\end{align}
$$
分配 $x_{4}=1$，$x_{2}=0$ 回代得到
$$
\begin{cases}
x_{1}=2 \\
x_{2}=0 \\
x_{3}=-2 \\
x_{4}=1
\end{cases}
$$
也可以分配 $x_{2}=1,x_{4}=0$ 得到
$$
\begin{cases}
x_{1}=-2\\
x_{2}=1 \\
x_{3}=0 \\
x_{4}=0
\end{cases}
$$
基于行阶梯矩阵还可以进一步通过消元得到最简的行阶梯矩阵形式。
$$
\begin{pmatrix}
\boxed{1} & 2 & 2 & 2 \\
0 & 0 & \boxed{2} & 4 \\
0 & 0 & 0 & 0
\end{pmatrix}
\to
\begin{pmatrix}
\boxed{1} & 2 & 0 & -2 \\
0 & 0 & \boxed{1} & 2 \\
0 & 0 & 0 & 0
\end{pmatrix}=R
$$
可以发现主列构成了一个单位矩阵 $I$ 而自由列也构成了一个矩阵 $F$
$$
\begin{pmatrix}
2 & -2 \\
0 & 2
\end{pmatrix}=F
$$
将 R 写作
$$
\begin{pmatrix}
I & F \\
0 & 0
\end{pmatrix}=R
$$
如果要求得 $Rx=0$，则 x 满足
$$
x=\begin{pmatrix}
-F \\
I
\end{pmatrix}
$$
即可。这里 $x$ 构成了零空间向量矩阵，它包含了所有的特解（自由列取 0 和 1）。

$$
\begin{pmatrix}
1 & 0 & 2 & -2 \\
0 & 1 & 0 & 2  \\
0 & 0 & 0 & 0  \\
\end{pmatrix}
\begin{pmatrix}
-2 & 2  \\
0 & -2 \\
1 & 0 \\
0 & 1
\end{pmatrix}
$$