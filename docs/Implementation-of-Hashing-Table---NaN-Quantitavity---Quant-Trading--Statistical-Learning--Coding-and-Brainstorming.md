<!--yml

分类：未分类

日期：2024-05-18 13:58:25

-->

# 哈希表的实现 | 统计学习、量化交易、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/12/10/204/#0001-01-01`](https://quantlife.wordpress.com/2012/12/10/204/#0001-01-01)

### 哈希表的实现

```
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

const int TABLE_SIZE = 128;

struct TableList {
    string key;
    int value;
    struct TableList *next;
};

unsigned hash_function(string s)
{
    unsigned hash = 0;

    for (int i = 0; i < s.length(); i++)
        hash = s[i] + 31*hash;
    return hash % TABLE_SIZE;
}

unsigned rehash(unsigned);

class HashMap 
{
private:
    TableList **table;
public:
    HashMap() 
    {
        table = new TableList*[TABLE_SIZE];
        for(int i = 0; i < TABLE_SIZE; i++) table[i] = NULL;
    }

    void showMap() 
    {
        struct TableList *tp;
        for (int i = 0; i < TABLE_SIZE; i++) {
            tp = table[i];
            if(tp){ 
                cout << "table[" << i << "] " << tp->key << "(" << tp->value << ")";
                tp = tp->next;
            }
            else 
                continue;
            while(tp) {
                cout << "->" << tp->key << "(" << tp->value << ")";
                tp = tp->next;
            }
            cout << endl;
        }
    }

    struct TableList* lookup(string s) 
    {
        struct TableList *tp;
        for(tp = table[hash_function(s)]; tp != NULL; tp = tp->next) 
                if((tp->key).compare(s) == 0) return tp;  // found
        return NULL;  // not found
    }

    void put(string key, int value) {
        struct TableList *tp;
        unsigned hash;

        // not found
        if(!(tp = lookup(key))) {
            tp = new TableList;
            tp->key = key;
            tp->value = value;
            hash = hash_function(key);
            tp->next = table[hash];
            table[hash] = tp;
        // it's already there
        } else {
            tp->key = key;
            tp->value = value;
            hash = hash_function(key);
            table[hash] = tp;
        }
    }     

    ~HashMap() 
    {
        for (int i = 0; i < TABLE_SIZE; i++)
            if (table[i] != NULL) delete table[i];
        delete[] table;
    }

};

int main()
{
    HashMap m;
    string line;
    ifstream dict_reader("C:/Temp/linux.words");
    //ifstream dict_reader("C:/Temp/shortlist");
    if( !dict_reader ) {
        cout << "Error opening input file - dict " << endl ;
        exit(1) ;
    }

    int count = 0;
    while(getline(dict_reader,line)) {    
        if((line[0] >= 'x' && line[0] < 'y') || (line[0] >= 'X' && line[0] < 'Y') ) {
            m.put(line,count++);
        }
    }

    m.showMap();
    return 0;
}
//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
//http://www.bogotobogo.com/cplusplus/cpptut.php
```

暂无评论。
