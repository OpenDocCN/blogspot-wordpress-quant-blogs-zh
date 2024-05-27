<!--yml

分类：未分类

日期：2024-05-18 13:58:21

-->

# 二叉搜索树的实现 | 数量未知 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2012/12/11/implementation-of-binary-search-tree/#0001-01-01`](https://quantlife.wordpress.com/2012/12/11/implementation-of-binary-search-tree/#0001-01-01)

### 二叉搜索树的实现

```
#include <iostream>
#include <vector>
using namespace std;

struct Tree
{
    char data;
    Tree *left, *right, *parent;

    Tree(char a){
        data = a;
        left = NULL; right = NULL; parent = NULL;
    }
};

Tree* insertTreeNode(Tree* node, char data){
    if(node == NULL){
        Tree* newNode = new Tree(data);
        return newNode;        
    }
    else if(data <= node->data){
        node->left = insertTreeNode(node->left, data);
        node->left->parent = node;
    }
    else{
        node->right = insertTreeNode(node->right, data);
        node->right->parent = node;
    }
    return node;
}

bool isBST(Tree* root){
    if (root == NULL)
        return 1;
    else if (!isBST(root->left) || !isBST(root->right))
        return 0;
    else if(root->left){
        if(root->left->data > root->data)
            return 0;
    }
    else if(root->right){
        if(root->data >= root->right->data)
            return 0;    
    }
        return 1;
}

int main ()
{
    char ch, ch1, ch2;
    Tree *found=NULL, *succ=NULL, *pred=NULL, *ancestor=NULL;
    char charArr[9] = {'A','B','C','D','E','F','G','H','I'};

    Tree* root=NULL;
//    for (int i=0;i<sizeof(charArr)/sizeof(char);++i)
//        insertTreeNode(root,charArr[i]);
    root = insertTreeNode(root,'B');
    root->left = insertTreeNode(root->left,'A');

    /* is the tree BST? */
    cout<< "Binary Search Tree?: "<< ( isBST(root) ? 'Y':'N') <<endl;

    return 0;
}

//Highlighted at http://tohtml.com/cpp/
//Bred 3 + C++
//http://www.bogotobogo.com/cplusplus/cpptut.php
```

暂无评论。
