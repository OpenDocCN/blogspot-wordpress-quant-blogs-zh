<!--yml

分类：未分类

日期：2024-05-18 13:57:03

-->

# 矩阵乘法 – 简单 | NaN 量化 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2013/04/20/matrix-multiplication-trivial/#0001-01-01`](https://quantlife.wordpress.com/2013/04/20/matrix-multiplication-trivial/#0001-01-01)

### 矩阵乘法 – 简单

```
#include <sstream>
#include <string>
#include <fstream>
#include <iostream>
#include <vector>

using namespace std;
typedef vector< vector<int> > Intmatrix;

void read(string filename, int& n, Intmatrix &A) {
	string line;
	ifstream infile;
	infile.open (filename.c_str());
	int i=0, j=0, a;

	while (getline(infile, line) && !line.empty() && i<n) {
		istringstream iss(line);
		j = 0;
		while (iss >> a) {
			A[i][j] = a;
			j++;
		}
		i++;
	}
	infile.close();
}

Intmatrix ijkalgorithm(Intmatrix A, Intmatrix B) {
	int n = A.size();

	// initialise C with 0s
	vector<int> tmp(n, 0);
	Intmatrix C(n, tmp);

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			for (int k = 0; k < n; k++) {
				C[i][j] += A[i][k] * B[k][j];
			}
		}
	}
	return C;
}

void printMatrix(Intmatrix matrix) {
	Intmatrix::iterator it;
	vector<int>::iterator inner;
	for (it=matrix.begin(); it != matrix.end(); it++) {
		for (inner = it->begin(); inner != it->end(); inner++) {
			cout << *inner;
			if(inner+1 != it->end()) {
				cout << "\t";
			}
		}
		cout << endl;
	}
}

int main (int argc, char* argv[]) {
	string filename = "C:\\Projects\\2000.in";
	int n = 3;
	Intmatrix A(n,n), B(n,n), C(n,n);
	read (filename, n, A);
	read (filename, n, B);
	C = ijkalgorithm(A, B);
	printMatrix(A);	printMatrix(B);	printMatrix(C);

	char tmp; cin>>tmp; return 0;
}
// https://github.com/MartinThoma/matrix-multiplication
// http://www.tohtml.com/cpp/
```

还没有评论。
