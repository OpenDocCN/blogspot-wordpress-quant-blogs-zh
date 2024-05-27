<!--yml

category: 未分类

date: 2024-05-18 13:58:34

-->

# Replace a char by a string | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[`quantlife.wordpress.com/2012/12/06/replace-a-char-by-a-string/#0001-01-01`](https://quantlife.wordpress.com/2012/12/06/replace-a-char-by-a-string/#0001-01-01)

### Replace a char by a string

```
// Replace all spaces in a string with '%20'
#include <iostream>
#include <string>
using namespace std;

//Method 1: use STL::string
string repUsestring(string str){
    string newStr;
    for (int i=0; i<str.length(); i++){
        if (str[i]==' ')
            newStr += "%20";
        else
            newStr += str[i];
    }
    return newStr;
}

//Method 2: use C-stype array

char* repUsearray(char* str){
    int length = strlen(str), newLength=length;
    for (int i=0;i<length;i++){
        if (str[i]== ' ')
            newLength+=2;
    }
    char* newStr = new char[newLength];

    int j = 0;
    for (int i=0; i<length; i++){
        if (str[i]!=' '){
            newStr[j] = str[i];
            j++;
        }
        else{
            newStr[j] = '%';
            j++;
            newStr[j] = '2';
            j++;
            newStr[j] = '0';
            j++;
        }
    }
    newStr[newLength]=0; //ALWAYS REMEMBER TO ADD THE END OF ARRAY
    return newStr;
}

int main(){
    string str1("test a test b test c ");
    char* str2 = "ai ni ai wo ai ta ";
    cout<<str1<<endl;
    cout<<repUsestring(str1)<<endl;
    cout<<str2<<endl;
    cout<<repUsearray(str2)<<endl;

    return 0;
}

//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
//http://www.bogotobogo.com/cplusplus/cpptut.php
```

No comments yet.
