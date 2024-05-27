<!--yml

分类：未分类

日期：2024-05-18 13:58:03

-->

# 链表实现 | 数量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/12/07/implementation-of-linked-list/#0001-01-01`](https://quantlife.wordpress.com/2012/12/07/implementation-of-linked-list/#0001-01-01)

### 链表实现

```
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

// only for the 1st Node
void initNode(Node *head, int n){
    head->data = n;
    head->next =NULL;
}

// apending
void addNode(struct Node *head, int n) {
    Node *newNode = new Node;
    newNode->data = n;
    newNode->next = NULL;

    Node *cur = head;
    while(cur) {
        if(cur->next == NULL) {
            cur->next = newNode;
            return;
        }
        cur = cur->next;
    }
}

// insert at the head
void insertFront(struct Node **head, int n) {
    Node *newNode = new Node;
    newNode->data = n;
    newNode->next = *head;
    *head = newNode;
}

// Traversing the list
/*display*/
void display(struct Node* head) {
    Node *list = head;
    while(list) {
        cout << list->data << "";
        list = list->next;
    }
    cout << endl;
    cout << endl;
}

/*search a node*/
struct Node *searchNode(struct Node* head, int n) {
    while(head) {
        if(head->data == n) return head;
        head = head->next;
    }
    cout << "No Node " << n << " in list.\n";
}

struct Node *searchNode2(struct Node* head, int n) {
    while(head!=NULL & head->data != n) {
        head = head->next;
    }
    return head;
}

/*delete a node*/
bool deleteNode(struct Node **head, Node *ptrDel) {
    Node* cur = *head;
    if(ptrDel == *head) {
        *head = (**head).next;
        delete ptrDel;
        return true;
    }
    while(cur){
        if(cur->next == ptrDel) {
            cur->next = ptrDel->next;
            delete ptrDel;
            return true;
        }
        cur = cur->next;
    }
    return false;
}

// delete 
void deleteLinkedList(struct Node **node)
{
    struct Node* tmpNode;
    while(*node) {
        tmpNode = *node;
        *node = tmpNode->next;
        delete tmpNode;
    }
}

// reverse the list
struct Node* reverse(struct Node** List) 
{
    Node* parent = *List;
    Node* me = parent->next;
    Node* child = me->next;

    /* make parent as tail */
    parent->next = NULL;
    while(child) {
        me->next = parent;
        parent = me;
        me = child;
        child = child->next;
    }
    me->next = parent;
    *List = me;
    return *List;
}

// copy
void copyLinkedList(struct Node *node, struct Node **pNew)
{
    if(node != NULL) {
        *pNew = new Node;
        (*pNew)->data = node->data;
        (*pNew)->next = NULL;
        copyLinkedList(node->next, &((*pNew)->next));
    }
}

// Compare two linked list: return value: same(1), different(0)
int compareLinkedList(struct Node *node1, struct Node *node2)
{
    static int flag;

    /* both lists are NULL */
    if(node1 == NULL && node2 == NULL) {
        flag = 1;
    }
    else {
        if(node1 == NULL || node2 == NULL) 
            flag = 0;
        else if(node1->data != node2->data) 
            flag = 0;
        else
            compareLinkedList(node1->next, node2->next);
    }

    return flag;
}

int main() 
{
    Node* newHead=0;    
    Node* head = new Node;
    initNode(head,10);
    display(head);
    addNode(head,20);
    addNode(head,30);
    display(head);

    insertFront(&head,5);
    display(head);

    int numDel = 5;
    Node* ptrDelete = searchNode(head,numDel);
    if(deleteNode(&head,ptrDelete)) 
        cout << "Node "<< numDel << " deleted!\n";
    display(head);

    cout << "The list is reversed\n";
    reverse(&head);
    display(head);

    cout << "The list is copied\n";
    copyLinkedList(head,&newHead);
    display(newHead);

    cout << "Comparing the two lists...\n";
    cout << "Are the two lists same?\n";
    if(compareLinkedList(head,newHead)) 
        cout << "Yes, they are same!\n";
    else
        cout << "No, they are different!\n";
    cout << endl;

    numDel = 20;
    ptrDelete = searchNode(newHead,numDel);
    if(deleteNode(&newHead,ptrDelete)) {
        cout << "Node "<< numDel << " deleted!\n";
        cout << "The new list after the delete is\n";
        display(newHead);
    }
    cout << "Comparing the two lists again...\n";
    cout << "Are the two lists same?\n";
    if(compareLinkedList(head,newHead)) 
        cout << "Yes, they are same!\n";
    else
        cout << "No, they are different!\n";

    cout << endl;
    cout << "Deleting the copied list\n";
    deleteLinkedList(&newHead);
    cout << "Displaying afer deleting:\n";
    display(newHead);
    cout << "END\n";
    return 0;
}

//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
//http://www.bogotobogo.com/cplusplus/cpptut.php
```

暂无评论。
