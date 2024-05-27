<!--yml

分类：未分类

日期：2024-05-18 08:10:38

-->

# Matrix decomposition with QuantLib | Quant Corner

> 来源：[`quantcorner.wordpress.com/2011/02/20/matrix-decomposition-with-quantlib/#0001-01-01`](https://quantcorner.wordpress.com/2011/02/20/matrix-decomposition-with-quantlib/#0001-01-01)

**QuantLib** 包括了几种**矩阵分解**工具以及**特征值/特征向量**的寻找工具。如果你的记忆需要在这方面线性代数做一个简单的刷新，你应该访问维基百科上关于[矩阵分解](http://en.wikipedia.org/wiki/Matrix_decomposition#Decompositions_based_on_eigenvalues_and_related_concepts)的页面。对于更高级的讨论和其他与矩阵相关的主题，Math World 有许多有价值的页面可供阅读。

在下方的代码中，我们将实现这些工具的一部分。正如您将看到的，这是相当直接的。我们工作的矩阵是标准的**方形矩阵**：

![标准矩阵](https://quantcorner.wordpress.com/wp-content/uploads/2011/02/standard_matrix_b1.jpg)

```
#include<ql\quantlib.hpp>
using namespace QuantLib;

using std::endl;
using std::cout;

int main(int, char*[]){

	// Matrix declaration and population
	Matrix A(3,3);
	A[0][0] = 1.0; A[0][1] = 0.5; A[0][2] = 0.2;
	A[1][0] = 0.5; A[1][1] = 1.0; A[1][2] = 0.3;
	A[2][0] = 0.2; A[2][1] = 0.3; A[2][2] = 1.0;

	SymmetricSchurDecomposition schurDec(A);
	SVD SVDDec(A);

	// Outputting
	cout << "Matrix A : " << endl << A << endl;
	cout << "Eigen values (Schur): " << endl;
	schurDec.eigenvalues() << endl;
	cout << "Eigen vector (Schur) : " << endl;
	schurDec.eigenvectors() << endl;
	cout << "Cholesky decomposition : " << endl;
	CholeskyDecomposition(A) << endl;
	cout << "SVD U-matrix : " << endl;
	SVDDec.U() << endl;
	cout << "SVD V-matrix : ";
	endl << SVDDec.V() << endl;

	return 0;
}
```
