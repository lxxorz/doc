## 乘法和逆矩阵

### 矩阵乘法
假设 $AB=C$
$$
\begin{pmatrix}
\dots \\
\dots \\
Row_{3} \\
\dots
\end{pmatrix}
\begin{pmatrix} 
\vdots & \vdots & \vdots & Col_{4} & \vdots
\end{pmatrix}
=\begin{pmatrix} \cdots & \cdots & \cdots & \cdots \\ \cdots & \cdots & \cdots & \cdots \\ \cdots & \cdots & \cdots & c_{34} \\ \cdots & \cdots & \cdots & \cdots \\ \end{pmatrix}
$$

显然这里的 $c_{34}=Row_{3}Col_{4}$。一个 $m\times n$ 的矩阵和一个 $n\times p$ 的矩阵，最终得到的矩阵是 $m\times p$
$$
A_{m\times n}B_{n\times p}=C_{m\times p}
$$
### 用行列的视角考虑矩阵乘法
1. C 矩阵是 A 矩阵列的线性组合
$$
AB = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn} \\
\end{pmatrix}
\begin{pmatrix}
b_{11} & b_{12} & \cdots & b_{1p} \\
b_{21} & b_{22} & \cdots & b_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
b_{n1} & b_{n2} & \cdots & b_{np} \\
\end{pmatrix}
$$
可以看成矩阵 A 乘以 B 中每一个列向量然后相加。矩阵 A 乘以 B 中的一个列向量实际就是 A 中列向量的线性组合。
$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn} \\
\end{pmatrix}
\begin{pmatrix}
b_{11}  \\
b_{21} \\ \\
\vdots \\
b_{n1}
\end{pmatrix}
$$
2. C 矩阵是 B 矩阵行的线性组合，
$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
\end{pmatrix}
\begin{pmatrix}
b_{11} & b_{12} & \cdots & b_{1p} \\
b_{21} & b_{22} & \cdots & b_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
b_{n1} & b_{n2} & \cdots & b_{np} \\
\end{pmatrix}

$$
3. 列乘以行
4. 