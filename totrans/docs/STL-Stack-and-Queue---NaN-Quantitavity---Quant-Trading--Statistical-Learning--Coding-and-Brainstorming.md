<!--yml
category: 未分类
date: 2024-05-18 13:59:01
-->

# STL Stack and Queue | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2012/11/02/stl-stack-and-queue/#0001-01-01](https://quantlife.wordpress.com/2012/11/02/stl-stack-and-queue/#0001-01-01)

### STL Stack and Queue

```
// Read words and print them in reverse order;
// Using STL Stack or Queue;
// http://www.cplusplus.com/reference/stl/stack/
//Highlighted at http://tohtml.com/cpp/

#include <iostream>
#include <stack>
#include <queue>
#include <string>
using namespace std;

int main() {

    // stack<string> allWords;
    queue<string> allWords;
    string word;

    while (cin >> word) {
        allWords.push(word);
    }

    cout << "Number of words = " << allWords.size() << endl;

    while (!allWords.empty()) {
       // cout << allWords.top() << endl;
       cout << allWords.front() << endl;
       allWords.pop();
    }
    return 0;
}
```

No comments yet.