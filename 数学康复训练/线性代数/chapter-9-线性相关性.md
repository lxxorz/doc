## 线性相关性、基、维数
### 线性相关性
线性相关性是针对**向量组**的一个概念。一个向量组什么时候是线性无关的呢。考虑 $(\vec{x}_{1},\vec{x}_{2},\vec{x}_{3}, \dots,\vec{x}_{n})$ 这一个向量组，如果对它进行线性组合。$(c_{1}\vec{x}_{1},c_{2}\vec{x}_{2},c_{3}\vec{x}_{3}, \dots,c_{n}\vec{x}_{n})$ 在 $c_{i}\neq 0$ 的情况下，如果至少存在一个组合使得结果是零向量。那么就称这个向量组是线性相关的。反之如果不存在一个线性组合的向量是零向量。那么就是**线性无关**的。
![[linearly-dependent.png]]
比如这两个向量就是线性相关的。因为可以通过取向量 $(1,2)$ 的两倍减去向量 $(2,4)$ 得到零向量。


如果向量组中存在一个零向量呢？
![[null-vector-linear-dependent.png]]
如果向量当中存在一个零向量。$c(2,4)^T+(0,0)^T=$ 显然，只要让常数 c 始终是 0，那么就能得到零向量。得出结论，只要向量组中存在零向量，那么该向量组始终是线性相关的。

再考虑另外一种情况。存在向量
![[linearly-dependent-in-subspace.png]]
红蓝向量显然是线性无关的，那么如果再加入第三个向量呢

![[linearly-dependent-in-subspace-2.png]]
可以发现，向量 $(2,2)^T$ 落在加入的第三个向量 $(2,0)^T$ 和 $(2,4)^T$ 生成的向量空间中，也就是可以通过图示中蓝色和灰色向量的线性组合来得到红色向量。所以它们是线性相关的。也就是下面这个等式是有解的。
$$
\begin{pmatrix}
2 & 2 \\
4 & 0
\end{pmatrix}
\begin{pmatrix}
c_{1} \\
c_{2}
\end{pmatrix}
=
\begin{pmatrix}
2 \\
2
\end{pmatrix}
$$
$$
\begin{cases}
c_{1}=\frac{1}{2} \\
c_{2}=\frac{1}{2}
\end{cases}
$$
![[linearly-dependent-addition.png]]