## A 的 LU 分解
考虑 $2\times2$ 矩阵
$$
\begin{pmatrix}
2 & 1 \\
8 & 7 
\end{pmatrix}=A
$$
对它做行变换消元
$$
\begin{pmatrix}
2 & 1 \\
8 & 7 
\end{pmatrix}
\to
\begin{pmatrix}
2 & 1 \\
0 & 3
\end{pmatrix}=U
$$
用矩阵乘法表示就是
$$
\begin{pmatrix}
1 & 0 \\
-4 & 1
\end{pmatrix}
\begin{pmatrix}
2 & 1  \\
8 & 7
\end{pmatrix}
=
\begin{pmatrix}
2 & 1 \\
0 & 3
\end{pmatrix}
$$
这里 $$
\begin{pmatrix}
1 & 0 \\
-4 & 1
\end{pmatrix}=E_{21}
$$
$E_{21}A=U$，我们想要让 $A$ 单独在一侧。
$A=LU$ 这里的 $L$ 如何求解？显然 $L$ 和 $E_{21}$ 存在关系
$$
\begin{cases}
A=LU \\
E_{21}A=U
\end{cases}
$$
如果在第二等式两边同时乘上 $E_{21}^{-1}$ 则得到 $A=E_{21}^{-1}U$，所以这里也就明白了，原来 $L=E_{21}^{-1}$
$$

\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
\begin{pmatrix} 
\vec{u} & \vec{v} \\
\end{pmatrix}
=
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
$$
$$
\begin{pmatrix}

\end{pmatrix}
$$
