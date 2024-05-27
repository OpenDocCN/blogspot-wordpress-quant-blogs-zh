<!--yml

类别：未分类

日期：2024 年 05 月 18 日 13:57:59

-->

# 斐波那契数：递归与迭代 | NaN Quantitavity - 量化交易，统计学习，编码和头脑风暴

> 来源：[`quantlife.wordpress.com/2013/01/20/fibonacci-number-recursive-vs-iterative/#0001-01-01`](https://quantlife.wordpress.com/2013/01/20/fibonacci-number-recursive-vs-iterative/#0001-01-01)

### 斐波那契数：递归与迭代

```
#include <iostream>
using namespace std;

// Recursive:
int fibo2(int n){
    if (n<=0) return -1;
    else if (n<=2) return 1;
    else return fibo2(n-1)+fibo2(n-2);
}

// Iterative:
int fibo1(int n){
    if (n<=0) return -1;
    int a=1, b=1, c=2;
    for (int i=3; i<=n; i++){
        c = a+b;
        a = b;
        b = c;
    }
    return b;
}

int main() 
{
    cout<<"Fiboracci Number:\n";
    for (int n=1; n<40; n++){
        cout<<fibo1(n)<<endl;
    }
    return 0;
}

//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
```

还没有评论。
