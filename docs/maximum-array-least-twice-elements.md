# 数组中的最大值，至少是其他元素的两倍

> 原文： [https://www.geeksforgeeks.org/maximum-array-least-twice-elements/](https://www.geeksforgeeks.org/maximum-array-least-twice-elements/)

给定长度为`n`的整数数组。 我们的任务是返回最大元素的索引，如果它的索引至少是数组中每个其他数字的两倍。 如果最大元素不满足条件，则返回 -1。

**示例**：

```
Input : arr = {3, 6, 1, 0}
Output : 1
Here, 6 is the largest integer, and for 
every other number in the array x, 6 is 
more than twice as big as x. The index of
value 6 is 1, so we return 1.

Input : arr = {1, 2, 3, 4}
Output : -1
4 isn't at least as big as twice the value
of 3, so we return -1.

```



**方法**：扫描数组以查找唯一的最大元素`m`，并跟踪其索引`maxIndex`。 再次扫描数组。 如果我们发现`x != m`与`m < 2 * x`，我们应该返回 **-1**。 否则，我们应该返回`maxIndex`。

## C++ 

```cpp

// CPP program for Maximum of 
// the array which is at least 
// twice of other elements of 
// the array. 
#include<bits/stdc++.h> 
using namespace std; 

// Function to find the  
// index of Max element  
// that satisfies the  
// condition 
int findIndex(int arr[], int len) {  

    // Finding index of 
    // max of the array 
    int maxIndex = 0; 
    for (int i = 0; i < len; ++i)  
        if (arr[i] > arr[maxIndex]) 
            maxIndex = i; 

    // Returns -1 if the 
    // max element is not  
    // twice of the i-th 
    // element.  
    for (int i = 0; i < len; ++i)              
        if (maxIndex != i && 
            arr[maxIndex] < 2 * arr[i]) 
            return -1; 

    return maxIndex; 
} 

// Driver function 
int main(){ 
    int arr[] = {3, 6, 1, 0}; 
    int len = sizeof(arr) / sizeof(arr[0]); 

    cout<<(findIndex(arr, len)); 
} 

// This code is contributed by Smitha Dinesh Semwal 

```

## Java

```java

// Java program for Maximum of the array 
// which is at least twice of other elements  
// of the array. 
import java.util.*; 
import java.lang.*; 

class GfG { 

    // Function to find the index of Max element 
    // that satisfies the condition 
    public static int findIndex(int[] arr) {         

        // Finding index of max of the array 
        int maxIndex = 0; 
        for (int i = 0; i < arr.length; ++i)  
            if (arr[i] > arr[maxIndex]) 
                maxIndex = i; 

        // Returns -1 if the max element is not  
        // twice of the i-th element.         
        for (int i = 0; i < arr.length; ++i)              
            if (maxIndex != i && arr[maxIndex] < 2 * arr[i]) 
                return -1; 

        return maxIndex; 
    } 

    // Driver function 
    public static void main(String argc[]){ 
        int[] arr = new int[]{3, 6, 1, 0}; 
        System.out.println(findIndex(arr)); 
    } 
} 

```

## Python3

```py

# Python 3 program for Maximum of  
# the array which is at least twice   
# of other elements of the array. 

# Function to find the index of Max  
# element that satisfies the condition 
def findIndex(arr):  

    # Finding index of max of the array 
    maxIndex = 0
    for i in range(0,len(arr)): 
        if (arr[i] > arr[maxIndex]): 
            maxIndex = i 

    # Returns -1 if the max element is not  
    # twice of the i-th element.      
    for i in range(0,len(arr)):      
        if (maxIndex != i and 
                arr[maxIndex] < (2 * arr[i])): 
            return -1

    return maxIndex 

# Driver code 
arr = [3, 6, 1, 0] 
print(findIndex(arr)) 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# program for Maximum of the array 
// which is at least twice of other elements  
// of the array. 
using System; 

class GfG { 

    // Function to find the index of Max element 
    // that satisfies the condition 
    public static int findIndex(int[] arr) {      

        // Finding index of max of the array 
        int maxIndex = 0; 
        for (int i = 0; i < arr.Length; ++i)  
            if (arr[i] > arr[maxIndex]) 
                maxIndex = i; 

        // Returns -1 if the max element is not  
        // twice of the i-th element.  
        for (int i = 0; i < arr.Length; ++i)          
            if (maxIndex != i && arr[maxIndex] < 2 * arr[i]) 
                return -1; 

        return maxIndex; 
    } 

    // Driver function 
    public static void Main() 
    { 
        int[] arr = new int[]{3, 6, 1, 0}; 
        Console.WriteLine(findIndex(arr)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program for Maximum of 
// the array which is at least 
// twice of other elements of 
// the array. 

// Function to find the  
// index of Max element  
// that satisfies the  
// condition 
function findIndex($arr, $len)  
{  

    // Finding index of 
    // max of the array 
    $maxIndex = 0; 
    for ( $i = 0; $i < $len; ++$i)  
        if ($arr[$i] > $arr[$maxIndex]) 
            $maxIndex = $i; 

    // Returns -1 if the 
    // max element is not  
    // twice of the i-th 
    // element.  
    for ($i = 0; $i < $len; ++$i)              
        if ($maxIndex != $i and
            $arr[$maxIndex] < 2 * $arr[$i]) 
            return -1; 

    return $maxIndex; 
} 

// Driver Code 
$arr = array(3, 6, 1, 0); 
$len = count($arr); 

echo findIndex($arr, $len); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
1

```

**时间复杂度**：`O(n)`。



* * *

* * *



