<!--yml

分类：未分类

日期：2024-05-18 13:58:56

-->

# Static members and functions | NaN Quantitavity - 量化交易，统计学习，编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/06/14/79/#0001-01-01`](https://quantlife.wordpress.com/2012/06/14/79/#0001-01-01)

### Static members and 函数

```
// A static member is shared by all objects of the class.
// All static data is initialized to zero when the first object is created, if no other initialization is present.
// We can't put it in the class definition but it can be initialized outside the class
// http://tohtml.com/cpp/ 
#include <iostream>
using namespace std;

class MyClass
{
public:
      MyClass(){std::cout << "default constructor" << ++count <<endl;}
      static int count;
};

int MyClass::count = 0;

int main(int argc, char** argv)
{
     MyClass* myObjArray = new MyClass[5];
     cout<<MyClass::count<<endl;
}

// A static member function can be called even if no objects of the class exist,
// and the static functions are accessed using only the class name and the scope resolution operator ::.
```

暂无评论。
