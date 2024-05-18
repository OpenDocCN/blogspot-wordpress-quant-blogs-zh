<!--yml
category: 未分类
date: 2024-05-18 13:57:08
-->

# Matrix multiplication – Boost | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/04/20/matrix-multiplication-boost/#0001-01-01](https://quantlife.wordpress.com/2013/04/20/matrix-multiplication-boost/#0001-01-01)

### Matrix multiplication – Boost

```
#include <sstream>
#include <fstream>
#include <iostream>
#include <algorithm>
#include <string>
#include <vector>
#include <boost/numeric/ublas/matrix.hpp>
#include <boost/numeric/ublas/operation.hpp>
using namespace std;
using namespace boost::numeric::ublas;
typedef matrix<int> Bmatrix;

void read(string filename, int& n, Bmatrix &A) {
	string line;
	ifstream infile;
	infile.open (filename.c_str());
	int i=0, j=0, a;

	while (getline(infile, line) && !line.empty() && i<n) {
		istringstream iss(line);
		j = 0;
		while (iss >> a) {
			A(i,j) = a;
			j++;
		}
		i++;
	}
	infile.close();
}

void printMatrix(Bmatrix matrix) {
	for (int i=0; i < matrix.size1(); i++) {
		for (int j=0; j < matrix.size2(); j++) {
			cout << matrix(i, j);
			if(j+1 != matrix.size2()) {
				cout << "\t";
			}
		}
		cout << endl;
	}
	cout<<endl;
}

int main (int argc, char* argv[]) {
	string filename = "C:\\Projects\\2000.in";
	int n = 3;
	Bmatrix A(n,n), B(n,n), C(n,n);
	read (filename, n, A);
	read (filename, n, B);
	boost::numeric::ublas::axpy_prod(A, B, C);
	printMatrix(A);	printMatrix(B);	printMatrix(C);

	char tmp; cin>>tmp; return 0;
} // http://martin-thoma.com/matrix-multiplication-python-java-cpp/
// http://www.tohtml.com/cpp/
```

No comments yet.