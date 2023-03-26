## 矩阵消元和逆矩阵
### 消元法
#### 高斯消元法
考虑一组方程式
$$
\begin{align}
x+2y+z&=2 \\
3x+8y+z&=12 \\
4y+z &=2
\end{align}
$$
用矩阵表示就是
$$
\begin{bmatrix}
1 & 2 & 1  \\
3 & 8 & 1 \\
0 & 4 & 1
\end{bmatrix}
$$
我们的目的是求解 x, y, z 的值。怎么求解呢？答案就是消元。通过消去一个等式中的未知量，然后递归回代求出所有的未知量的值。

第一个步骤消元，通过 $-3\times(1)$ 式加上 $(2)$ 式就消去了 $x$。
$$
\begin{bmatrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 4 & 1
\end{bmatrix}
$$
继续通过 $-2\times(2)$ 加上 $(3)$ 得到
$$
\begin{bmatrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 0 & 5
\end{bmatrix}
$$
#### 增广矩阵
想象整个过程我们只对左侧式子做了操作，同样的右侧式子也要**同步**做对应的变换。将右侧式子带入矩阵，这样的矩阵称为“增广矩阵”
$$
\begin{bmatrix}
1 & 2 & 1  & 2 \\
3 & 8 & 1  & 12\\
0 & 4 & 1 & 2
\end{bmatrix}
$$
矩阵中增加的一列也要经过同样操作。
$$
\begin{bmatrix}
1 & 2 & 1  & 2 \\
3 & 8 & 1  & 12\\
0 & 4 & 1 & 2
\end{bmatrix}
\to
\begin{bmatrix}
1 & 2 & 1  & 2 \\
0 & 2 & -2  & 6\\
0 & 4 & 1 & 2
\end{bmatrix}
\to
\begin{bmatrix}
1 & 2 & 1  & 2 \\
0 & 2 & -2  & 6\\
0 & 0 & 5 & -10
\end{bmatrix}
$$
最后就是回代的过程
$$
\begin{align}
x+2y+z&=2 \\
2y-2z&=6 \\
5z&=-10
\end{align}
$$
通过 $(3)$ 带入 $(2)$ 求得 y, $(2),(3)$ 结果带入 $(1)$ 求得 z最后结果就是
$$
\begin{cases}
x=2\\
y=1 \\
z=-2
\end{cases}
$$
### 矩阵表示
> 虽说矩阵乘法就是矩阵列的 「线性组合」，但是这里还是运用的行变换。行变换也有其意义。

考虑下面矩阵的乘法
$$
\begin{bmatrix}
1 & 2 & 7
\end{bmatrix}
\begin{bmatrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1
\end{bmatrix}
$$
得到的最终结果实际上就是 $row_{1}+2\times row_{2}+7\times row_{3}$。如果乘以一个单位矩阵呢?
$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1
\end{bmatrix}

$$
得到的结果是保持原样，乘以一个单位矩阵等于什么也不做。为了描述我们之前的消元操作，需要修改一下左边的矩阵，以便达到消元的目的。
$$
\begin{bmatrix}
1 & 0 & 0 \\
-3 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1
\end{bmatrix}
=
\begin{bmatrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 4 & 1
\end{bmatrix}
$$
上面的矩阵乘法就描述消元的第一步，将第 2 行变成第一行乘以 $-3$ 加上原本的第二行
同理，继续下一步操作
$$
\begin{bmatrix}
1 & 0 & 0  \\
0 & 1 & 0 \\
0 & -2 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 4 & 1
\end{bmatrix}
=
\begin{bmatrix}
1 &  2 & 1 \\
0 & 2 & -2 \\
0 & 0 & 5
\end{bmatrix}

$$
结合起来就是
$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & -2 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 \\
-3 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1
\end{bmatrix}
$$
我们将左边两个矩阵分别记作 $M_{32}$ 和 $M_{21}$ ，就可以简化为 $M_{32}(M_{23}E)=U$
由于矩阵的结合律，这里括号就随便啦。

### 置换矩阵
通过上面的知识，想一想，如果我们想要交换矩阵的两行。应该使用什么矩阵来相乘呢？假设矩阵 $$
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
\to
\begin{bmatrix}
c & d \\
a & b
\end{bmatrix}
$$
这个矩阵非常显而易见
$$
\begin{bmatrix}
0 & 1 \\
1 & 0
\end{bmatrix}
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
\to
\begin{bmatrix}
c & d \\
a & b
\end{bmatrix}
$$
再进一步，如果我们相对列进行交换呢，应该怎么办呢？

前面提到，「矩阵乘法是对矩阵列的线性组合」。这里就体现了这句话。
$$
\begin{bmatrix}
a & b  \\
c & d
\end{bmatrix}
\begin{bmatrix}
0 & 1 \\
1 & 0
\end{bmatrix}
$$

### 矩阵的逆变换
如果想要将对矩阵的消元操作变换回去，那么必然需要做反向操作。我们把这个反向操作的矩阵称为逆矩阵记作 $M^{-1}$。并且可知 $M^{-1}ME=E$ 由于矩阵的结合律。
$$
\begin{align}
(M^{-1}M)E&=E \\
M^{-1}M=I
\end{align}
$$
