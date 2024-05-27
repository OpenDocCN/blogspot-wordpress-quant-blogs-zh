<!--yml

分类：未分类

日期：2024-05-18 13:59:11

-->

# 翻转 C 语言风格的字符串 | NaN 量化 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/11/02/reverse-a-c-style-string/#0001-01-01`](https://quantlife.wordpress.com/2012/11/02/reverse-a-c-style-string/#0001-01-01)

### 翻转 C 语言风格的字符串

```
// Reverse a C-Style String
#include <iostream>
using namespace std;

void reverse(char *str) {
    char * end = str;
    char tmp;
    if (str) {
        while (*end) {
            ++end;
        }
        --end;
        while (str < end) {
            tmp = *str;
            *str++ = *end;
            *end-- = tmp;
        }
    }
} 

int main(){
    char* str = new char[6];
    strcpy(str, "Hello");
    // char* str = "Hello" doesn't work. Cz here str is const type.
    cout<<str<<endl;
    reverse(str);
    cout<<str<<endl;
    delete[] str;

    return 0;
}
//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
```

尚无评论。
