```

分类：未分类

日期：2024-05-18 13:57:50

```

# 删除指定字符 | NaN 量化 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/05/31/73/#0001-01-01`](https://quantlife.wordpress.com/2012/05/31/73/#0001-01-01)

### 删除指定字符

```
#include <iostream>
using namespace std;

int main()
{
    char s[] = "Battle of the Vowels: Hawaii vs. Grozny";
    char r[] = "aeiou";

    int *flags = new int[128]; // assumes ASCII!
    int src, dst;

    // Set flags for characters to be removed
    for( src = 0; src < strlen(r); ++src )
    {
        flags[(int)r[src]] = 1;
    }

    src = 0; dst = 0;

    while(src<strlen(s))
    {
        if(flags[(int)s[src]]!=1)
        {
            s[dst++] = s[src];
        }
        src++;
    }

    delete[] flags;

    char* res = new char[dst+1];
    strncpy(res, s, dst);
    res[dst] = '';
    cout<<res<<endl;

    delete[] res;
    return 0;
}
/*
int main(){
    char s[] = "Battle of the Vowels: Hawaii vs. Grozny";
    char r[] = "aeiou";
    char* sNew = new char[strlen(s)];

    int* flag = new int[128];
    for (int i=0; i < strlen(r); i++){
        flag[(int)r[i]]=1;
    }

    int iNew = 0;
    for (int i=0; i < strlen(s); i++){
        if (flag[(int)s[i]]!=1){
            sNew[iNew++] = s[i];
        }
    }
    sNew[iNew]='';

    cout<<sNew<<endl;
    delete[] flag;
    delete[] sNew;

    return 0;
}
*/
//Highlighted at http://tohtml.com/cpp/
```

尚无评论。
