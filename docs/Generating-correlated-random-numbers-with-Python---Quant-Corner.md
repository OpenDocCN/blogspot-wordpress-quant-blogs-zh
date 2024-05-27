<!--yml

类别: 未分类

日期: 2024-05-18 08:06:58

-->

# 用 Python 生成相关随机数 | 量化角落

> 来源：[`quantcorner.wordpress.com/2018/02/09/generation-of-correlated-random-numbers-using-python/#0001-01-01`](https://quantcorner.wordpress.com/2018/02/09/generation-of-correlated-random-numbers-using-python/#0001-01-01)

(下面有点自言自语。这是对旧博客文章的重写，基于 [Generating correlated random numbers](http://www.sitmo.com/article/generating-correlated-random-numbers/#comment-325 "Generating Correlated Random Numbers")  by Thijs van den Berg)

假设我想要按照以下相关性矩阵生成 3 组相关随机数：

![ \begin{bmatrix} 1.0 & 0.6 & 0.3 \\ 0.6 & 1.0 & 0.5 \\ 0.3 & 0.5 & 1.0 \end{bmatrix} ](img/b75a36f06b49172be659347f8e843aee.png)

```
from scipy.linalg import cholesky

# Correlation matrix
corr_mat= np.array([[1.0, 0.6, 0.3],
                    [0.6, 1.0, 0.5],
                    [0.3, 0.5, 1.0]])

# Compute the (upper) Cholesky decomposition matrix
upper_chol = cholesky(corr_mat)

# Generate 3 series of normally distributed (Gaussian) numbers
rnd = np.random.normal(0.0, 1.0, size=(10**7, 3))

# Finally, compute the inner product of upper_chol and rnd
ans = rnd @ upper_chol

```

如今，可以检查结果是否一致：

```
# One can check results are consistent
from scipy.stats import pearsonr

corr_0_1 , _ = pearsonr(ans[:,0], ans[:,1])
#corr_0_1
#0.60013025775533102

corr_0_2 , _ = pearsonr(ans[:,0], ans[:,2])
#corr_0_2
#0.30049740204791148

corr_1_2 , _ = pearsonr(ans[:,1], ans[:,2])
#corr_1_2
#0.50026641543258898

```
