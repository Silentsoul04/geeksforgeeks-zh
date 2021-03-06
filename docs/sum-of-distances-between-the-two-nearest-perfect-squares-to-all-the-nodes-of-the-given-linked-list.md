# 与给定链表所有节点最接近的两个完全平方之间的距离总和

> 原文：[https://www.geeksforgeeks.org/sum-of-distances-between-the-two-nearest-perfect-squares-to-all-the-nodes-of-the-given-linked-list/](https://www.geeksforgeeks.org/sum-of-distances-between-the-two-nearest-perfect-squares-to-all-the-nodes-of-the-given-linked-list/)



给定一个链表，任务是为给定链表的所有节点找到两个最接近的完全平方之间的距离之和。

**示例**：

> **输入**：`3 -> 15 -> 7 -> NULL`
>
> **输出**：15
>
> 对于 3：最接近的左侧完全平方为 1，最接近的右侧为 4，即`4 - 1 = 3`
>
> 对于 15：`16 – 9 = 7`
>
> 对于 7：`9 – 4 = 5`
>
> `3 + 7 + 5 = 15`
> 
> **输入**：`1 -> 5 -> 10 -> 78 -> 23 -> NULL`
>
> **输出**：38

**方法**：初始化`sum = 0`，对于每个节点，如果当前节点的值本身是一个理想平方，则左，右最接近的理想平方将成为该值本身，而距离为 0。否则，找到左和右最接近的完全平方，例如`leftPS`和`rightPS`，然后更新`sum = sum + (rightPS – leftPS)`。

下面是上述方法的实现：

```

# Python3 implementation of the approach 
import sys 
import math 

# Structure for a node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to find the total distance sum 
def distanceSum(head): 

    # If head is null 
    if not head: 
        return

    # To store the required sum 
    tsum = 0
    temp = head 

    # Traversing through all the nodes one by one 
    while(temp): 
        sq_root = math.sqrt(temp.data) 

    # If current node is not a perfect square  
    # then find left perfect square and  
    # right perfect square 
        if sq_root<temp.data: 
            left_ps = math.floor(sq_root)**2
            right_ps = math.ceil(sq_root)**2
            tsum+=(right_ps - left_ps) 

        # Get to the next node 
        temp = temp.next
    return tsum 

# Driver code 
if __name__=='__main__': 
    head = Node(3) 
    head.next = Node(15) 
    head.next.next = Node(7) 
    head.next.next.next = Node(40) 
    head.next.next.next.next = Node(42) 

    result = distanceSum(head) 
    print("{}".format(result)) 

```

**输出**：

```
41

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。