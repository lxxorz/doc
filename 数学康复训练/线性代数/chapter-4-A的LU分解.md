## A 的 LU 分解

### 转置矩阵和逆矩阵
考虑一下矩阵乘法的顺序，如果要对矩阵做逆变换，比如
$$
AB=U
$$
想要 「撤销」AB 的变换应该分别乘上他们的逆矩阵，但是这里乘法的顺序就有点讲究了。
$$
B^{-1}A^{-1}AB=I
$$
这里可以把顺序理解为 $B\to A\to A^{-1}\to B^{-1}$ 用通俗易懂的例子来讲，就相当于这四个步骤：
1. $B$ 👉脱鞋
2. $A$ 👉脱袜子
3. $A^{-1}$ 👉穿袜子
4. $B^{-1}$ 👉穿鞋

如果转置某个可你矩阵，那么其转置的逆是多少？
$$
AA^{-1}=I
$$
对两边同时转置，单位矩阵转置仍然还是单位矩阵，它是对称的， $(A^{-1})^TA^T=I$
```ad-summary
对于单个矩阵，其转置的逆等于逆的转置
```


### LU 分解
假设有一个二维矩阵 $A$， $EA=U$ 这里对矩阵进行消元，如果要得到 $A=LU$ 的形式。则 $A=E^{-1}U$。

再考虑一下多个消元矩阵的情况。假设不进行「行变换」。
$$
\boxed{E_{32}E_{31}E_{21}A=U}
\to
\boxed{A=(E_{21})^{-1} (E_{31})^{-1} (E_{32})^{-1}U}
$$



考虑下列二维矩阵，然后对它做行变换
$$
E_{21}A=
\begin{pmatrix}
1 & 0 \\
-4 & 1
\end{pmatrix}
\begin{pmatrix}
2 & 3  \\
8 & 7
\end{pmatrix}=
\begin{pmatrix}
2 & 3 \\
0 & -5
\end{pmatrix}=U
$$
对矩阵 $A$ 做逆乘变换，可以发现确实 $E_{21}$ 的逆矩阵是 $L$，这是为了抵消消元矩阵产生的 「减法效应」
$$
A=\begin{pmatrix}
2 & 3  \\
8 & 7
\end{pmatrix}=
\begin{pmatrix}
1 & 0 \\
4 & 1
\end{pmatrix}
\begin{pmatrix}
2 & 3  \\
0 & -5
\end{pmatrix}=E_{21}^{-1}U
$$
再考虑一个更加复杂一点的三维矩阵, （为了简单消元时这里不考虑交换行）
$$
\begin{align}
U&=E_{32}E_{21}U \\
&=\begin{pmatrix}
2 & 1 & 0 \\
1 & 2 & 1 \\
0 & 1 & 2
\end{pmatrix} \\
&= \begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & -\frac{2}{3} & 1
\end{pmatrix}
\begin{pmatrix}
1 & 0 & 0 \\
-\frac{1}{2} & 1 & 0 \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
2 & 1 & 0 \\
1 & 2 & 1 \\
0 & 1 & 2
\end{pmatrix} \\
&=\begin{pmatrix}
2 & 1 & 0 \\
0 & \frac{3}{2} & 1 \\
0 & 0 & \frac{4}{3}
\end{pmatrix}
\end{align}

$$
$$
\begin{align}
A&=\begin{pmatrix}
1 & 2 & 0 \\
2 & 1 & 0 \\
0 & 2 & 1
\end{pmatrix} \\
&= \begin{pmatrix}
1 & 0 & 0 \\
\frac{1}{2} & 1 & 0 \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & \frac{2}{3} & 1
\end{pmatrix}
\begin{pmatrix}
2 & 1 & 0 \\
0 & \frac{3}{2} & 1 \\
0 & 0 & \frac{4}{3}
\end{pmatrix} \\
&=E_{21}^{-1}E_{32}^{-1}U
\end{align}

$$
在形式上，通过观察，这里的 L 矩阵和 U 矩阵分别是下三角矩阵和上三角矩阵。为了保持某种形式上的统一可以再增加一个矩阵让 U 主对角线都是 1.
$$
\begin{pmatrix}
2 & 0 & 0 \\
0 & \frac{2}{3} & 0 \\
0 & 0 & \frac{4}{3}
\end{pmatrix}
\begin{pmatrix}
1 & 0 & 0 \\
\frac{1}{2} & 1 & 0 \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & \frac{2}{3} & 1
\end{pmatrix}
\begin{pmatrix}
1 & 1 & 0 \\
0 & 1 & 1 \\
0 & 0 & 1
\end{pmatrix} 
$$


> [!attention] 注意
> 这里都是没有行交换的消元


> [!important] important
> 主元行被下方行减去时，他们是不是 A
的原始行? 不是！消元的过程可能会改变他们。

