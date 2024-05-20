<!--yml
category: 未分类
date: 2024-05-18 13:59:11
-->

# Reverse a C-style String | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2012/11/02/reverse-a-c-style-string/#0001-01-01](https://quantlife.wordpress.com/2012/11/02/reverse-a-c-style-string/#0001-01-01)

### Reverse a C-style String

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

No comments yet.