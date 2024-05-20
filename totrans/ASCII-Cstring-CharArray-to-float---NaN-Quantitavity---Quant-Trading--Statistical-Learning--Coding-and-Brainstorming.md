<!--yml
category: 未分类
date: 2024-05-18 13:58:51
-->

# ASCII Cstring/CharArray to float | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2012/06/06/ascii-cstringchararray-to-float/#0001-01-01](https://quantlife.wordpress.com/2012/06/06/ascii-cstringchararray-to-float/#0001-01-01)

### ASCII Cstring/CharArray to float

```
#include <iostream>
using namespace std;

double atofA(char s[]) 
{
    int sign = 1, i = 0, left = 0, power = 10;
    double right = 0.0;

    // Determine the sign:
    if (s[0]=='-')
    {
        sign = -1;
        i++;
    }

    // Calculate the integer part - left:
    while(s[i] && s[i]!='.')
    {
        left = left*10 + (s[i]-'0');
        i++;
    }

    // Calculate the float part - right:
    if (s[i]=='.')
    {
        i++;
        while(s[i])
        {
            right = right + (double)(s[i]-'0')/(power);
            power*=10;
            i++;
        }
    }

    return sign*(left+right);
}

int main()
{
    double d = atofA("-314.1592");
    // double d = atofA("-.1592");
    cout.precision(7);
    cout  << d << endl;
    return 0;
}

// Syntax highlighted at: http://tohtml.com/cpp/
```

No comments yet.