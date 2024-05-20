<!--yml
category: 未分类
date: 2024-05-18 13:58:08
-->

# Stack/Queue Implementation in Cpp | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2012/11/01/stack-in-cpp/#0001-01-01](https://quantlife.wordpress.com/2012/11/01/stack-in-cpp/#0001-01-01)

### Stack/Queue Implementation in Cpp

```
#include <iostream>
#include <string>
using namespace std;
typedef int Object;

class Node{
    public:
        Object data;
        Node*  next;

        Node (Object item){
            data = item;
            next = NULL;
        }
        ~Node(){ delete next;}
};

class Stack{
public:
    Node* head;

    Object pop(){
        if (head != NULL){
            Object item = head->data;
            head = head->next;
            return item;
        }
        return NULL;
    }

    void push (Object item){
        Node* t = new Node (item);
        t->next = head;
        head     = t;
    }

};

class Queue{
public:
    Node* head;
    Node* tail;

    void push (Object item){
        Node* t = new Node (item);
        if(tail!=NULL){
            tail->next = t;
            tail    = t;
        }
        else{
            head=tail=t;
        }
    }

    Object pop(){
        if (head != NULL){
            Object item = head->data;
            head = head->next;
            return item;
        }
        return NULL;
    }
};

int main()
{
    Stack* st=new Stack();
    Queue* qu=new Queue();
    Object temp;
    while (cin >> temp){
        st->push(temp);
        qu->push(temp);
    }

    cout<<"Stake (FILO): ";
    while(st->head !=NULL){
        cout<< st->pop();
    }
    cout<<endl;

    cout<<"Queue (FIFO): ";
    while(qu->head !=NULL){
        cout<< qu->pop();
    }
    cout<<endl;

    return 0;
}
//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
```

No comments yet.