## 旋转矩阵的推导
在线性代数中，旋转是一种线性变换，也就是满足如下性质
	1. $T(\vec{x}+\vec{y}) = T(\vec{x})+T(\vec{y})$
	2. $T(c \vec{x})=cT(\vec{x})$
因此，对向量 $\vec{v}$ 的旋转等价于各分量的旋转，设向量空间 $\mathbf{R}^3$ 的标准基向量是 $(i,j,k)$，如果旋转轴是 z 轴且约定逆时针正方向旋转
![](Pasted%20image%2020231120222331.png)
$$
A(\alpha)\cdot \vec{v}=
\begin{pmatrix}
\cos \alpha & -\sin \alpha & 0  \\
\sin \alpha & \cos \alpha & 0  \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
1 \\
1 \\
1 \\
\end{pmatrix}
=\begin{pmatrix}
\cos \alpha - \sin \alpha\\
\sin \alpha + \cos \alpha\\
1
\end{pmatrix}
$$