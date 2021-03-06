# Python 程序：使用一次遍历来查找链表的中间

> 原文：[https://www.geeksforgeeks.org/python-program-to-find-middle-of-a-linked-list-using-one-traversal/](https://www.geeksforgeeks.org/python-program-to-find-middle-of-a-linked-list-using-one-traversal/)

给定一个单链表，找到链表的中间。 给定一个单链表，找到链表的中间。 例如，如果给定的链表为`1 -> 2 -> 3 -> 4 -> 5`，则输出应为 3。

**方法 1**：

遍历整个链表并计算节点数量。 现在再次遍历列表，直到`count / 2`并返回`count / 2`处的节点。

**方法 2**：

使用两个指针遍历链表。 将一个指针移动一个，另一个指针移动两个。 当快速指针到达末尾时，慢速指针将到达链表的中间。

```

# Python 3 program to find the middle of a   
# given linked list  

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None 

class LinkedList: 

    def __init__(self): 
        self.head = None

    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Function to get the middle of  
    # the linked list 
    def printMiddle(self): 
        slow_ptr = self.head 
        fast_ptr = self.head 

        if self.head is not None: 
            while (fast_ptr is not None and fast_ptr.next is not None): 
                fast_ptr = fast_ptr.next.next
                slow_ptr = slow_ptr.next
            print("The middle element is: ", slow_ptr.data) 

# Driver code 
list1 = LinkedList() 
list1.push(5) 
list1.push(4) 
list1.push(2) 
list1.push(3) 
list1.push(1) 
list1.printMiddle() 

```

**输出**：

```
The middle element is:  2

```

**方法 3**：

初始化临时变量为`head`，初始化计数为零。

循环执行，直到`head`变为`Null`（即列表的末尾），并仅在`count`为奇数时增加临时节点，以这种方式`temp`将遍历到元素的中部，并且`head`将遍历所有链表。 打印临时数据。

```

# Python 3 program to find the middle of a   
# given linked list  

class Node: 
    def __init__(self, value): 
        self.data = value 
        self.next = None

class LinkedList: 

    def __init__(self): 
        self.head = None

    # create Node and and make linked list 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    def printMiddle(self): 
        temp = self.head  
        count = 0

        while self.head: 

            # only update when count is odd 
            if (count & 1):  
                temp = temp.next
            self.head = self.head.next

            # increment count in each iteration  
            count += 1 

        print(temp.data)      

# Driver code 
llist = LinkedList()  
llist.push(1) 
llist.push(20)  
llist.push(100)  
llist.push(15)  
llist.push(35) 
llist.printMiddle() 
# code has been contributed by - Yogesh Joshi 

```

**输出**：

```
100

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。