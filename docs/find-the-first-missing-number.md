# 寻找最小的缺失数字

> 原文： [https://www.geeksforgeeks.org/find-the-first-missing-number/](https://www.geeksforgeeks.org/find-the-first-missing-number/)

给定**排序的**数组，其中包含`n`个不同的整数，其中每个整数的范围为 0 到`m-1`，`m > n`。 查找数组中缺少的最小数字。

示例：

> 输入: `{0,1,2,6,9}, n = 5, m = 10`
> 
> 输出: 3
> 
> 输入: `{4, 5, 10, 11}, n = 4, m = 12`
> 
> 输出: 0
> 
> 输入: `{0, 1, 2, 3}, n = 4, m = 5`
> 
> 输出: 4
> 
> 输入: `{0, 1, 2, 3, 4, 5, 6, 7, 10}, n = 9, m = 11`
> 
> 输出: 8

感谢 Ravichandra 建议采用以下两种方法。



**方法 1（使用二分搜索）**：

对于`i = 0`到`m-1`，对数组中的`i`进行二分搜索。 如果数组中不存在`i`，则返回`i`。

时间复杂度：`O(m log n)`。

**方法 2（线性搜索）**：

如果`arr[0]`不为 0，则返回 0。否则，从索引 0 开始遍历输入数组，并针对元素对`a[i]`和`a[i + 1]`，找出它们之间的区别。 如果差大于 1，则`a[i] +1`是丢失的数字。

时间复杂度：`O(n)`。

**方法 3（使用修改的二分搜索）**：

感谢 yasein 和 **Jams** 提出了此方法。

在标准二分搜索过程中，将要搜索的元素与中间元素进行比较，然后根据比较结果，确定搜索是结束还是移至左半部分或右半部分。

在此方法中，我们修改了标准的二分搜索算法，以比较中间元素及其索引，并在此比较的基础上做出决策。

1.  如果第一个元素与其索引不同，则返回第一个索引。

2.  否则获得中间索引，例如`mid`，

    1.  如果`arr[mid]`大于`mid`则所需元素位于左半部分。

    2.  另外，所需元素位于右半部分。

## C++ 

```cpp

// C++ program to find the smallest elements 
// missing in a sorted array. 
#include<bits/stdc++.h> 
using namespace std; 

int findFirstMissing(int array[],  
                    int start, int end) 
{ 
    if (start > end) 
        return end + 1; 

    if (start != array[start]) 
        return start; 

    int mid = (start + end) / 2; 

    // Left half has all elements  
    // from 0 to mid 
    if (array[mid] == mid) 
        return findFirstMissing(array,  
                            mid+1, end); 

    return findFirstMissing(array, start, mid); 
} 

// Driver code 
int main() 
{ 
    int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << "Smallest missing element is " << 
        findFirstMissing(arr, 0, n-1) << endl; 
} 

// This code is contributed by 
// Shivi_Aggarwal  

```

## C

```c
// C program to find the smallest elements missing
// in a sorted array.
#include<stdio.h>
 
int findFirstMissing(int array[], int start, int end)
{
    if (start  > end)
        return end + 1;
 
    if (start != array[start])
        return start;
 
    int mid = (start + end) / 2;
 
    // Left half has all elements from 0 to mid
    if (array[mid] == mid)
        return findFirstMissing(array, mid+1, end);
 
    return findFirstMissing(array, start, mid);
}
 
// driver program to test above function
int main()
{
    int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 10};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Smallest missing element is %d",
           findFirstMissing(arr, 0, n-1));
    return 0;
}
```

## Java

```java
class SmallestMissing 
{
    int findFirstMissing(int array[], int start, int end) 
    {
        if (start > end)
            return end + 1;
 
        if (start != array[start])
            return start;
 
        int mid = (start + end) / 2;
 
        // Left half has all elements from 0 to mid
        if (array[mid] == mid)
            return findFirstMissing(array, mid+1, end);
 
        return findFirstMissing(array, start, mid);
    }
 
    // Driver program to test the above function
    public static void main(String[] args) 
    {
        SmallestMissing small = new SmallestMissing();
        int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 10};
        int n = arr.length;
        System.out.println("First Missing element is : "
                + small.findFirstMissing(arr, 0, n - 1));
    }
}
```

## Python3

```py
# Python3 program to find the smallest
# elements missing in a sorted array.
 
def findFirstMissing(array, start, end):
 
    if (start > end):
        return end + 1
 
    if (start != array[start]):
        return start;
 
    mid = int((start + end) / 2)
 
    # Left half has all elements
    # from 0 to mid
    if (array[mid] == mid):
        return findFirstMissing(array,
                          mid+1, end)
 
    return findFirstMissing(array, 
                          start, mid)
 
 
# driver program to test above function
arr = [0, 1, 2, 3, 4, 5, 6, 7, 10]
n = len(arr)
print("Smallest missing element is",
      findFirstMissing(arr, 0, n-1))
 
# This code is contributed by Smitha Dinesh Semwal 
```

## C#

```cs
// C# program to find the smallest
// elements missing in a sorted array.
using System;
 
class GFG
{
    static int findFirstMissing(int []array,
                            int start, int end) 
    {
        if (start > end)
            return end + 1;
 
        if (start != array[start])
            return start;
 
        int mid = (start + end) / 2;
 
        // Left half has all elements from 0 to mid
        if (array[mid] == mid)
            return findFirstMissing(array, mid+1, end);
 
        return findFirstMissing(array, start, mid);
    }
 
    // Driver program to test the above function
    public static void Main() 
    {
        int []arr = {0, 1, 2, 3, 4, 5, 6, 7, 10};
        int n = arr.Length;
         
        Console.Write("smallest Missing element is : "
                    + findFirstMissing(arr, 0, n - 1));
    }
}
 
// This code is contributed by Sam007 
```

## PHP

```php
<?php
// PHP program to find the
// smallest elements missing
// in a sorted array.
 
// function that returns 
// smallest elements missing
// in a sorted array.
function findFirstMissing($array, $start, $end)
{
    if ($start > $end)
        return $end + 1;
 
    if ($start != $array[$start])
        return $start;
 
    $mid = ($start + $end) / 2;
 
    // Left half has all 
    // elements from 0 to mid
    if ($array[$mid] == $mid)
        return findFirstMissing($array, 
                                $mid + 1, 
                                $end);
 
    return findFirstMissing($array, 
                            $start, 
                            $mid);
}
 
    // Driver Code
    $arr = array (0, 1, 2, 3, 4, 5, 6, 7, 10);
    $n = count($arr);
    echo "Smallest missing element is " ,
          findFirstMissing($arr, 2, $n - 1);
         
// This code Contributed by Ajit.
?>
```

输出：

```
Smallest missing element is 8
```

注意：如果数组中有重复的元素，则此方法无效。

时间复杂度：`O(log n)`。