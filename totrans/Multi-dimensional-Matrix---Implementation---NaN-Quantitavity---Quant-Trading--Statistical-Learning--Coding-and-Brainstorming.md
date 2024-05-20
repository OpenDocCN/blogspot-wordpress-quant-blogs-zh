<!--yml
category: 未分类
date: 2024-05-18 13:56:58
-->

# Multi-dimensional Matrix – Implementation | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/04/20/multi-dimensional-matrix-implementation/#0001-01-01](https://quantlife.wordpress.com/2013/04/20/multi-dimensional-matrix-implementation/#0001-01-01)

### Multi-dimensional Matrix – Implementation

```
/* Three Dimensional (3 by 5 by 2) Matrix dynamic memeory allocation */
#include <iostream>
#include <vector>
#include <boost/numeric/ublas/matrix.hpp>
#include "boost/multi_array.hpp"
using namespace std;

template <class Type> class Mymatrix
{
private:
  size_t mWidth, mHeight, mDepth;
  std::vector<Type> mArray;

public:
  Mymatrix(const size_t inWidth, const size_t inHeight, const size_t inDepth) :
   mWidth(inWidth), mHeight(inHeight), mDepth(inDepth)
   {
       mArray.resize(mWidth * mHeight * mDepth);
	   mArray = std::vector<Type>(mWidth * mHeight * mDepth,9.9);
   }

  Type Get(const size_t inX, const size_t inY, const size_t inZ) {
     return mArray[(inX * mHeight * mDepth) + (inY * mDepth) + inZ];
  }

  void Set(const size_t inX, const size_t inY, const size_t inZ, Type val) {
     mArray[(inX * mHeight * mDepth) + (inY * mDepth) + inZ] = val;
  }

};

int main (int argc, char* argv[]) {
	// Method 1: pointer to pointer to pointer
	double*** M1 = new double** [3];
	for (int i=0;i<3;++i){
		M1[i] = new double* [5];
		for (int j=0;j<5;j++){
			M1[i][j] = new double [2];
			for (int k=0;k<2;k++)
				M1[i][j][k]=i*100+j*10+k;
		}
	}
	cout<<M1[2][2][0]<<endl;
	for (int i=0;i<3;++i){
		for (int j=0;j<5;j++){
			delete[] M1[i][j];
		}
		delete[] M1[i];
	}
	delete[] M1;

	// Method 2 - matrix notation in C
	double (*M2)[5][2];
	M2 = new double[3][5][2];
	cout<<M2[2][2][0]<<endl;
	delete[] M2;

	// Method 3 - Boost :: matrix for 2-dim
	typedef boost::numeric::ublas::matrix<double> Bmatrix;
	Bmatrix M3(3,5);
	for (int i=0;i<3;i++)
		for (int j=0;j<5;j++)
				M3(i,j)=i*100+j*10;
	cout<<M3(2,2)<<endl;

	// Method 4 - Boost :: multi_array
	typedef boost::multi_array<double, 3> Trmatrix;
	typedef Trmatrix::index index;
	Trmatrix M4(boost::extents[3][5][2]);
	for (int i=0;i<3;i++)
		for (int j=0;j<5;j++)
				for (int k=0;k<2;k++)
					M4[i][j][k]=i*100+j*10+k;
	cout<<M4[2][3][1]<<endl;

	// Method 5 - Self-defined class
	Mymatrix<double> M5(3,5,2);
	M5.Set(2,4,1, 352.22);
	cout<<M5.Get(2,4,1)<<endl;

	char tmp; cin>>tmp; return 0;
}
// http://www.tohtml.com/cpp/
```

No comments yet.