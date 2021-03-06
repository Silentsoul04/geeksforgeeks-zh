# 流中的第`K`个最大元素

> 原文： [https://www.geeksforgeeks.org/kth-largest-element-in-a-stream/](https://www.geeksforgeeks.org/kth-largest-element-in-a-stream/)

给定无限的整数流，请在任何时间点找到第`k`个最大元素。

例：

```
Input:
stream[] = {10, 20, 11, 70, 50, 40, 100, 5, ...}
k = 3

Output:    {_,   _, 10, 11, 20, 40, 50,  50, ...}
```

允许的额外空间为`O(k)`。



在以下文章中，我们讨论了在数组中找到第`k`个最大元素的不同方法。

[未排序数组中第`K`个最小/最大元素 | 系列 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)

[未排序数组中第`K`个最小/最大元素 | 系列 2（预期线性时间）](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)

[未排序数组中第`K`个最小/最大元素 | 系列 3（最差情况的线性时间）](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)

在这里，我们有一个流而不是整个数组，并且只允许存储`k`个元素。

**简单解决方案**是保持大小为`k`的数组。 想法是保持数组排序，以便在`O(1)`时间内找到第`k`个最大元素（如果数组按升序排序，我们只需要返回数组的第一个元素）

如何处理流中的新元素？

对于流中的每个新元素，请检查新元素是否小于当前的第`k`个最大元素。 如果是，则忽略它。 如果否，则从数组中删除最小的元素，并按排序顺序插入新元素。 处理新元素的时间复杂度为`O(k)`。

**更好的解决方案**是使用大小为`k`的自平衡二分搜索树。 可以在`O(Logk)`时间中找到第`k`个最大元素。

如何处理流的新元素？

对于流中的每个新元素，请检查新元素是否小于当前的第`k`个最大元素。 如果是，则忽略它。 如果否，则从树中删除最小的元素并插入新元素。 处理新元素的时间复杂度为`O(Logk)`。

一种有效的**解决方案**是使用大小为`k`的最小堆存储流的`k`个最大元素。 第`k`个最大元素始终位于根，可以在`O(1)`时间找到。

如何处理流的新元素？

将新元素与堆根进行比较。 如果新元素较小，则将其忽略。 否则，将`root`替换为新元素，然后调用建堆作为修改后的堆的根。 找到第`k`个最大元素的时间复杂度是`O(Logk)`。

```

// A C++ program to find k'th smallest element in a stream 
#include<iostream> 
#include<climits> 
using namespace std; 

// Prototype of a utility function to swap two integers 
void swap(int *x, int *y); 

// A class for Min Heap 
class MinHeap 
{ 
    int *harr; // pointer to array of elements in heap 
    int capacity; // maximum possible size of min heap 
    int heap_size; // Current number of elements in min heap 
public: 
    MinHeap(int a[], int size); // Constructor 
    void buildHeap(); 
    void MinHeapify(int i);  //To minheapify subtree rooted with index i 
    int parent(int i)  { return (i-1)/2;  } 
    int left(int i)    { return (2*i + 1);  } 
    int right(int i)   { return (2*i + 2);  } 
    int extractMin();  // extracts root (minimum) element 
    int getMin()       {  return harr[0]; } 

    // to replace root with new node x and heapify() new root 
    void replaceMin(int x) { harr[0] = x; MinHeapify(0); } 
}; 

MinHeap::MinHeap(int a[], int size) 
{ 
    heap_size = size; 
    harr = a;  // store address of array 
} 

void MinHeap::buildHeap() 
{ 
    int i = (heap_size - 1)/2; 
    while (i >= 0) 
    { 
        MinHeapify(i); 
        i--; 
    } 
} 

// Method to remove minimum element (or root) from min heap 
int MinHeap::extractMin() 
{ 
    if (heap_size == 0) 
        return INT_MAX; 

    // Store the minimum vakue. 
    int root = harr[0]; 

    // If there are more than 1 items, move the last item to root 
    // and call heapify. 
    if (heap_size > 1) 
    { 
        harr[0] = harr[heap_size-1]; 
        MinHeapify(0); 
    } 
    heap_size--; 

    return root; 
} 

// A recursive method to heapify a subtree with root at given index 
// This method assumes that the subtrees are already heapified 
void MinHeap::MinHeapify(int i) 
{ 
    int l = left(i); 
    int r = right(i); 
    int smallest = i; 
    if (l < heap_size && harr[l] < harr[i]) 
        smallest = l; 
    if (r < heap_size && harr[r] < harr[smallest]) 
        smallest = r; 
    if (smallest != i) 
    { 
        swap(&harr[i], &harr[smallest]); 
        MinHeapify(smallest); 
    } 
} 

// A utility function to swap two elements 
void swap(int *x, int *y) 
{ 
    int temp = *x; 
    *x = *y; 
    *y = temp; 
} 

// Function to return k'th largest element from input stream 
void kthLargest(int k) 
{ 
    // count is total no. of elements in stream seen so far 
    int count = 0, x;  // x is for new element 

    // Create a min heap of size k 
    int *arr = new int[k]; 
    MinHeap mh(arr, k); 

    while (1) 
    { 
        // Take next element from stream 
        cout << "Enter next element of stream "; 
        cin >> x; 

        // Nothing much to do for first k-1 elements 
        if (count < k-1) 
        { 
            arr[count] = x; 
            count++; 
        } 

        else
        { 
          // If this is k'th element, then store it 
          // and build the heap created above 
          if (count == k-1) 
          { 
              arr[count] = x; 
              mh.buildHeap(); 
          } 

          else
          { 
               // If next element is greater than  
               // k'th largest, then replace the root 
               if (x > mh.getMin()) 
                  mh.replaceMin(x); // replaceMin calls  
                                    // heapify() 
          } 

          // Root of heap is k'th largest element 
          cout << "K'th largest element is "
               << mh.getMin() << endl; 
          count++; 
        } 
    } 
} 

// Driver program to test above methods 
int main() 
{ 
    int k = 3; 
    cout << "K is " << k << endl; 
    kthLargest(k); 
    return 0; 
} 

```

输出：

```
K is 3
Enter next element of stream 23
Enter next element of stream 10
Enter next element of stream 15
K'th largest element is 10
Enter next element of stream 70
K'th largest element is 15
Enter next element of stream 5
K'th largest element is 15
Enter next element of stream 80
K'th largest element is 23
Enter next element of stream 100
K'th largest element is 70
Enter next element of stream
CTRL + C pressed
```

