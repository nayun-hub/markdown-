# 奇异值分解和Moore-Penrose伪逆

## 奇异值分解(singular value decomposition,SVD)

可将矩阵分解为**奇异向量**和**奇异值**。

在用特征分解去分析矩阵A时，得到特征向量构成的矩阵V和特征值构成的向量$\lambda$ ，此时A可以写作：
$$
A=Vdiag(\lambda)V^{-1}
$$
奇异值分解类似，只不过此时将A分解成三个矩阵相乘。
$$
A=UDV^{T}
$$
假设A是一个$m\times n$的矩阵，那么U是一个$m\times m$ 的矩阵，D是一个$m\times n$的矩阵，V是一个$n\times n$的矩阵。

其中，矩阵U和V都定义为正交矩阵，而矩阵D定义为对角矩阵。对角矩阵D对角线上的元素被称为矩阵A的奇异值，矩阵U的列向量被称为左奇异向量，矩阵V的列向量被称为右奇异向量。

## Moore-Penrose伪逆

实际算法：$A^+=VD^+ U^T$ 

