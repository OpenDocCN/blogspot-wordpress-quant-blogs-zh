<!--yml

分类：未分类

日期：2024-05-18 13:58:47

-->

# 删除重复字符 | NaN 量化 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/12/06/remove-duplicate-characters/#0001-01-01`](https://quantlife.wordpress.com/2012/12/06/remove-duplicate-characters/#0001-01-01)

### 删除重复字符

```
// Remove duplicated characters
#include <iostream>
using namespace std;

// Method1: no (large) memory; O(n²)
void rmDuplicated1(char str[]) {
    int nOld = strlen(str);
    if (nOld>1) {
        int nNew = 0;
        int j;
        for (int i=0; i < nOld; ++i){  //iterate for each orignal element
            // check if this element is a nonduplicated one
            for (j=0; j<nNew; ++j){
                if (str[j]==str[i])
                    break;
            }
            // if nonduplicated, add it. 
            if (j==nNew){
                nNew++;
                str[nNew-1] = str[i];
            }
        }

        str[nNew] = 0;
    }
}

// Method2: addtional memory; O(n)
char* rmDuplicated2(char str[]) {
    int nOld = strlen(str);
    if (nOld<2)
        return str;
    else{
        char* newStr = new char[nOld];
        bool check[256] = {0};

        int nNew = 0;
        for (int i=0; i < nOld; ++i){
            if (!check[(int)str[i]]){
                newStr[nNew] = str[i];
                nNew++;
                check[str[i]] = true;
            }
        }

        newStr[nNew] = 0;
        return newStr;
    }
}

int main(){
    char* str = new char[10];
    strcpy(str, "aaaBBB");
    // char* str = "Hello" doesn't work. Cz here str is const type.
    cout<<str<<endl;
    rmDuplicated1(str);
    cout<<str<<endl;
    cout<<rmDuplicated2(str)<<endl;
    delete[] str;

    return 0;
}

//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
```

暂无评论。
