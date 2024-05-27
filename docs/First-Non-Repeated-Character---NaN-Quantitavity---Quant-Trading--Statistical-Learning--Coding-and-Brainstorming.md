<!--yml

category: 未分类

日期：2024 年 05 月 18 日 13:57:54

-->

# 第一个不重复的字符 | NaNQuantitavity - 量化交易，统计学习，编码和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/05/31/68/#0001-01-01`](https://quantlife.wordpress.com/2012/05/31/68/#0001-01-01)

### 第一个不重复的字符

```
#include <iostream>
#include <string>
using namespace std;

// The first 128 code points (0–127) of Unicode correspond to
// the letters and symbols on a standard U.S. keyboard.

// C stype string is an array of char, and ended by '' automatically;
// char x[]="abc"; then strlen(x)=3;
// char x[]="abcdef"; then strlen(x)=3;
// char x[]="abc"; then the real memory is 

bool isUniqueChars(string str) {
    bool char_set[256] = {0};
    for (int i = 0; i < str.size(); i++) {
        int val = str[i];
        if (char_set[val]) return false;
        char_set[val] = true;
    }
    return true;
}

int main()
{
    char str[20] = "abcd", xRepeat = ' ';
    bool iRepeat = false;
    int i = 0, len = strlen(str);

    for (i = 0; i < len;i++)
    {
        iRepeat = false;
        for (int j = 0; j < len; j++)
        {
            if (j!=i && str[j]==str[i])
            {
                iRepeat = true;
                break;
            }
        }
        if(!iRepeat)
        {
            xRepeat = str[i];
            break;
        }    
    }
    cout<<"In the string of "<<str<<endl;
    cout<<"the first nonrepeat char is the "<< i+1 << " th char: "<<xRepeat<<endl<<endl;
    cout<<isUniqueChars(str)<<endl;
    return 0;
}
//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
```

尚无评论。
