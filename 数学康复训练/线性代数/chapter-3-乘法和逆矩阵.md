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
```ad-tip
在完成当前章节后，推荐阅读https://github.com/kenjihiranabe/The-Art-of-Linear-Algebra 加强理解
```

1. C 矩阵是 A 矩阵列的线性组合
$$
\begin{pmatrix}
\end{pmatrix}
$$
可以看成矩阵 A 乘以 B 中每一个列向量然后相加。矩阵 A 乘以 B 中的一个列向量实际就是 A 中列向量的线性组合。
$$
\begin{pmatrix}
a_{11} & \ldots & \cdots & a_{1n} \\
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
$$
\begin{pmatrix}
1 \\
2 \\
3
\end{pmatrix}
\begin{pmatrix}
1 & 6
\end{pmatrix}
=
\begin{pmatrix}
1 & 6 \\
2 & 12 \\
3 & 18
\end{pmatrix}
$$
从这个角度看列乘以行生成了一个矩阵，该矩阵是原矩阵的倍数矩阵。现在扩张到两列
$$
\begin{pmatrix}
1 & 2 \\
2  & 3\\
3 & 4
\end{pmatrix}
\begin{pmatrix}
1 & 6 \\
0 & 0
\end{pmatrix}
=\begin{pmatrix}
1 \\
2 \\
3
\end{pmatrix}
\begin{pmatrix}
1 & 6
\end{pmatrix}
+
\begin{pmatrix}
2 \\
3 \\
4
\end{pmatrix}
\begin{pmatrix}
0 & 0
\end{pmatrix}
$$

### 不可逆矩阵
首先回顾一下逆矩阵的定义，存在一个矩阵 $A$，如果
$$
A^{-1}A=I
$$
那么称 $A^{-1}$ 是矩阵 $A$ 的逆矩阵。然后考虑这样一个矩阵
$$
A=\begin{pmatrix}
1 & 2\\
2 & 4
\end{pmatrix}
$$
此矩阵应该显然是不可逆的，下面给出直观的解释。根据定义
$$
A^{-1}A=I
$$
那么能否通过
$$
\begin{align}
\begin{pmatrix}
Row_{1}  \\
\end{pmatrix}
\begin{pmatrix}
1 & 2 \\
2 & 4
\end{pmatrix}
&\to
\begin{pmatrix}
1 \\
0
\end{pmatrix} \\
\begin{pmatrix}
Row_{2}
\end{pmatrix}
\begin{pmatrix}
1 & 2 \\
2 & 4
\end{pmatrix}
&\to \begin{pmatrix}
0 \\
1
\end{pmatrix}
\end{align}
$$
仔细向量这个矩阵代表什么意思，代表对右边的矩阵的行向量线性组合。而向量 $(1,0)^T$ 和向量 $(0,1)^T$ 并不在 $(1,2)^T$ 和 $(2,4)^T$ 生成的向量空间中。你可以非常直观的想象到 $(1,2)^T$ 和 $(2,4)^T$ 他们两个的线性组合始终只能在一条直线之上。显然 $(1,0)^T$ 和 $(0,1)^T$ 并不在这一条直线上。
![[Intuitive-interpretation-of-inverse-matrices.png]]
因此不可能通过这样的线性组合得到单位矩阵。因此也不可能存在逆矩阵。同时也可以得出结论，线性相关的矩阵是不可逆矩阵。因为始终有单位矩阵中的（列或行）向量在他们的向量空间之外

### 高斯-若儿当法求解逆矩阵
在直观的理解了矩阵是否可逆之后，让我们来求解逆矩阵。考虑矩阵
$$
\begin{pmatrix}
1 & 3 \\
2 & 7
\end{pmatrix}
$$
第一步写成增广矩阵
$$
\left(\begin{array}{cc|cc}
  1 & 3 & 1 & 0 \\
  2 & 7 & 0 & 1
\end{array}\right)
$$

然后做行阶梯矩阵变换
$$
\left(\begin{array}{cc|cc}
1 & 3 & 1 & 0 \\
0 & 1 & -2 & 1
\end{array}\right)
\to
\left(\begin{array}{cc|cc}
\boxed{1} & 0 & 7 & -3 \\
0 & \boxed{1} & -2 & 1
\end{array}\right)
$$

左边矩阵已经变成了单位矩阵 $I$ 右边则是我们要求的 $A$ 的逆矩阵。为什么呢？先用消元矩阵 $E$ 来表示我们的一系列消元操作
$$
\left(\begin{array}{c|c}
A & I
\end{array}\right)
\to
\left(\begin{array}{c|c}
EA  & EI
\end{array}\right)
\to
\left(\begin{array}{}
I & E
\end{array}\right)
$$
因为 $EA=I$ 所以这里的 E 就是 A 的逆矩阵 $A^{-1}$ 了