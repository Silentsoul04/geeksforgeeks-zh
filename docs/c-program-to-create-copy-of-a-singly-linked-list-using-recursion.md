# C 程序：使用递归创建单链表的副本

> 原文：[https://www.geeksforgeeks.org/c-program-to-create-copy-of-a-singly-linked-list-using-recursion/](https://www.geeksforgeeks.org/c-program-to-create-copy-of-a-singly-linked-list-using-recursion/)



给定指向[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)的**头**节点的指针，任务是[递归](http://www.geeksforgeeks.org/recursion/)创建链表的副本。 

**示例**：：

> **输入**：以下链表的头部
>
> `1 -> 2 -> 3 -> 4 -> NULL`
>
> **输出**：
>
> 原始列表：`1 -> 2 -> 3 -> 4 -> NULL`
>
> 副本列表：`1 -> 2 -> 3 -> 4 -> NULL`
> 
> **输入**：以下链表的头部
>
> `1 -> 2 -> 3 -> 4 -> 5 -> NULL`
>
> **输出**：
>
> 原始列表：`1 -> 2 -> 3 -> 4 -> 5 -> NULL`
>
> 副本列表：`1 -> 2 -> 3 -> 4 -> 5 -> NULL`

**方法**：请按照以下步骤解决问题：

1.  **基本情况**：如果`head == NULL`，则返回`NULL`。

2.  使用[`malloc()`](https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/)在[堆](https://www.geeksforgeeks.org/heap-data-structure/)中分配新节点并设置其数据。

3.  通过在其余节点上递归，设置新节点的下一个指针。

4.  返回副本节点的`head`指针。

5.  最后，同时打印原始链表和副本链表。

下面是上述方法的实现：

## C

```c

// C program for the above approach 
#include <stdio.h> 
#include <stdlib.h> 

// Node for linked list 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to print given linked list 
void printList(struct Node* head) 
{ 
    struct Node* ptr = head; 
    while (ptr) { 

        printf("%d -> ", ptr->data); 
        ptr = ptr->next; 
    } 

    printf("NULL"); 
} 

// Function to create a new node 
void insert(struct Node** head_ref, int data) 
{ 
    // Allocate the memory for new Node 
    // in the heap and set its data 
    struct Node* newNode 
        = (struct Node*)malloc( 
            sizeof(struct Node)); 

    newNode->data = data; 

    // Set the next node pointer of the 
    // new Node to point to the current 
    // node of the list 
    newNode->next = *head_ref; 

    // Change the pointer of head to point 
    // to the new Node 
    *head_ref = newNode; 
} 

// Function to create a copy of a linked list 
struct Node* copyList(struct Node* head) 
{ 
    if (head == NULL) { 
        return NULL; 
    } 
    else { 

        // Allocate the memory for new Node 
        // in the heap and set its data 
        struct Node* newNode 
            = (struct Node*)malloc( 
                sizeof(struct Node)); 

        newNode->data = head->data; 

        // Recursively set the next pointer of 
        // the new Node by recurring for the 
        // remaining nodes 
        newNode->next = copyList(head->next); 

        return newNode; 
    } 
} 

// Function to create the new linked list 
struct Node* create(int arr[], int N) 
{ 
    // Pointer to point the head node 
    // of the singly linked list 
    struct Node* head_ref = NULL; 

    // Construct the linked list 
    for (int i = N - 1; i >= 0; i--) { 

        insert(&head_ref, arr[i]); 
    } 

    // Return the head pointer 
    return head_ref; 
} 

// Function to create both the lists 
void printLists(struct Node* head_ref, 
                struct Node* dup) 
{ 

    printf("Original list: "); 

    // Print the original linked list 
    printList(head_ref); 

    printf("\nDuplicate list: "); 

    // Print the duplicate linked list 
    printList(dup); 
} 

// Driver Code 
int main(void) 
{ 
    // Given nodes value 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int N = sizeof(arr) / sizeof(arr[0]); 

    // Head of the original Linked list 
    struct Node* head_ref = create(arr, N); 

    // Head of the duplicate Linked List 
    struct Node* dup = copyList(head_ref); 

    printLists(head_ref, dup); 

    return 0; 
}

```

**输出**：

```
Original list: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
Duplicate list: 1 -> 2 -> 3 -> 4 -> 5 -> NULL

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。