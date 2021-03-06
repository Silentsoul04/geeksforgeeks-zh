# 从祖先矩阵构造树

> 原文： [https://www.geeksforgeeks.org/construct-tree-from-ancestor-matrix/](https://www.geeksforgeeks.org/construct-tree-from-ancestor-matrix/)

给定祖先矩阵`mat[n][n]`，其中祖先矩阵定义如下。

```
   mat[i][j] = 1 if i is ancestor of j
   mat[i][j] = 0, otherwise 
```

从给定的祖先矩阵构造一个二叉树，其所有节点值都从 0 到`n-1`。

1.  可以假定，如果程序有效，则输入内容可以从中构造出树。

2.  一个输入可以构建许多二叉树。 该程序将构造其中任何一个。

例子：

```
Input: 0 1 1
       0 0 0 
       0 0 0 
Output: Root of one of the below trees.
    0                0
  /   \     OR     /   \
 1     2          2     1

Input: 0 0 0 0 0 0 
       1 0 0 0 1 0 
       0 0 0 1 0 0 
       0 0 0 0 0 0 
       0 0 0 0 0 0 
       1 1 1 1 1 0
Output: Root of one of the below trees.
      5              5               5
   /    \           / \            /   \
  1      2   OR    2   1    OR    1     2  OR ....
 /  \   /        /    /  \       / \    /
0   4  3        3    0    4     4   0  3
There are different possible outputs because ancestor
matrix doesn't store that which child is left and which
is right.

```

该问题主要是以下问题的逆向。

[从给定的二叉树](https://www.geeksforgeeks.org/construct-ancestor-matrix-from-a-given-binary-tree/)构造祖先矩阵。

**我们强烈建议您最小化浏览器，然后自己尝试。**

解决方案中使用的观察结果：

1.  对应于叶子的行全为 0

2.  根目录对应的行最大数量为 1。

3.  第`i`行中的数字 1 表示节点`i`的后代数量。

这个想法是以**自底向上**的方式构造树。

1.  创建一个节点指针数组`node[]`。

2.  存储与给定计数相对应的行号。 为此，我们使用了[多图](http://geeksquiz.com/multimap-associative-containers-the-c-standard-template-library-stl/)。

3.  处理多图的所有条目，从最小计数到最大（注意，可以按排序顺序遍历图和多图中的条目）。 请为每个条目执行以下操作。

    1.  为当前行号创建一个新节点。

    2.  如果此节点不是叶节点，请考虑未设置其父节点的所有后代，将当前节点作为其父节点。

4.  最后处理的节点（具有最大和的节点）是树的根。

下面是上述想法的 C++ 实现。 以下是步骤。

```

// Given an ancestor matrix for binary tree, construct 
// the tree. 
#include <bits/stdc++.h> 
using namespace std; 

# define N 6 

/* A binary tree node */
struct Node 
{ 
    int data; 
    Node *left, *right; 
}; 

/* Helper function to create a new node */
Node* newNode(int data) 
{ 
    Node* node = new Node; 
    node->data = data; 
    node->left = node->right = NULL; 
    return (node); 
} 

// Constructs tree from ancestor matrix 
Node* ancestorTree(int mat[][N]) 
{ 
    // Binary array to determine whether 
    // parent is set for node i or not 
    int parent[N] = {0}; 

    // Root will store the root of the constructed tree 
    Node* root = NULL; 

    // Create a multimap, sum is used as key and row 
    // numbers are used as values 
    multimap<int, int> mm; 

    for (int i = 0; i < N; i++) 
    { 
        int sum = 0; // Initialize sum of this row 
        for (int j = 0; j < N; j++) 
            sum += mat[i][j]; 

        // insert(sum, i) pairs into the multimap 
        mm.insert(pair<int, int>(sum, i)); 
    } 

    // node[i] will store node for i in constructed tree 
    Node* node[N]; 

    // Traverse all entries of multimap.  Note that values 
    // are accessed in increasing order of sum 
    for (auto it = mm.begin(); it != mm.end(); ++it) 
    { 
      // create a new node for every value 
      node[it->second] = newNode(it->second); 

      // To store last processed node. This node will be 
      // root after loop terminates 
      root = node[it->second]; 

      // if non-leaf node 
      if (it->first != 0) 
      { 
        // traverse row 'it->second' in the matrix 
        for (int i = 0; i < N; i++) 
        { 
           // if parent is not set and ancestor exits 
           if (!parent[i] && mat[it->second][i]) 
           { 
             // check for unoccupied left/right node 
             // and set parent of node i 
             if (!node[it->second]->left) 
               node[it->second]->left = node[i]; 
             else
               node[it->second]->right = node[i]; 

             parent[i] = 1; 
           } 
        } 
      } 
    } 
    return root; 
} 

/* Given a binary tree, print its nodes in inorder */
void printInorder(Node* node) 
{ 
    if (node == NULL) 
        return; 
    printInorder(node->left); 
    printf("%d ", node->data); 
    printInorder(node->right); 
} 

// Driver program 
int main() 
{ 
    int mat[N][N] = {{ 0, 0, 0, 0, 0, 0 }, 
        { 1, 0, 0, 0, 1, 0 }, 
        { 0, 0, 0, 1, 0, 0 }, 
        { 0, 0, 0, 0, 0, 0 }, 
        { 0, 0, 0, 0, 0, 0 }, 
        { 1, 1, 1, 1, 1, 0 } 
    }; 

    Node* root = ancestorTree(mat); 

    cout << "Inorder traversal of tree is \n"; 
    printInorder(root); 

    return 0; 
} 

```

输出：

```
Inorder traversal of tree is 
0 1 4 5 3 2 
```

请注意，我们也可以使用向量数组代替多图。 为了简单起见，我们使用了多重映射。 向量数组将提高性能，因为插入和访问元素将花费`O(1)`时间。

