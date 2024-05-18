<!--yml
category: 未分类
date: 2024-05-18 13:57:59
-->

# Fibonacci Number: Recursive vs. Iterative | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/01/20/fibonacci-number-recursive-vs-iterative/#0001-01-01](https://quantlife.wordpress.com/2013/01/20/fibonacci-number-recursive-vs-iterative/#0001-01-01)

### Fibonacci Number: Recursive vs. Iterative

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

No comments yet.