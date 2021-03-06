# 排序二进制数组所需的最小相邻交换

> 原文： [https://www.geeksforgeeks.org/minimum-swaps-required-sort-binary-array/](https://www.geeksforgeeks.org/minimum-swaps-required-sort-binary-array/)

给定一个二进制数组，任务是使用最少交换对该二进制数组进行排序。 我们只允许交换相邻的元素。

**示例**：

```
Input : [0, 0, 1, 0, 1, 0, 1, 1]
Output : 3
1st swap : [0, 0, 1, 0, 0, 1, 1, 1]
2nd swap : [0, 0, 0, 1, 0, 1, 1, 1]
3rd swap : [0, 0, 0, 0, 1, 1, 1, 1]

Input : Array = [0, 1, 0, 1, 0]
Output : 3

```

**方法**：

这可以通过在每个 1 的右侧找到零个数并将它们相加来完成。 为了对数组进行排序，每个数组总是必须在其右侧的每个零处执行交换操作。 因此，数组中特定 1 的交换操作总数为其右侧的零数目。 找出每一个右边的零的数目，即交换的数目，并将它们全部相加以获得交换的总数。

**实现**：

## C++ 

```cpp

// C++ code to find minimum number of 
// swaps to sort a binary array 
#include <bits/stdc++.h> 

using namespace std; 

// Function to find minimum swaps to 
// sort an array of 0s and 1s. 
int findMinSwaps(int arr[], int n) 
{ 
    // Array to store count of zeroes 
    int noOfZeroes[n]; 
    memset(noOfZeroes, 0, sizeof(noOfZeroes)); 

    int i, count = 0; 

    // Count number of zeroes 
    // on right side of every one. 
    noOfZeroes[n - 1] = 1 - arr[n - 1]; 
    for (i = n - 2; i >= 0; i--) { 
        noOfZeroes[i] = noOfZeroes[i + 1]; 
        if (arr[i] == 0) 
            noOfZeroes[i]++; 
    } 

    // Count total number of swaps by adding number 
    // of zeroes on right side of every one. 
    for (i = 0; i < n; i++) { 
        if (arr[i] == 1) 
            count += noOfZeroes[i]; 
    } 

    return count; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 0, 0, 1, 0, 1, 0, 1, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findMinSwaps(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java code to find minimum number of 
// swaps to sort a binary array 
class gfg { 
      
    static int findMinSwaps(int arr[], int n) 
    { 
        // Array to store count of zeroes 
        int noOfZeroes[] = new int[n]; 
        int i, count = 0; 
  
        // Count number of zeroes 
        // on right side of every one. 
        noOfZeroes[n - 1] = 1 - arr[n - 1]; 
        for (i = n - 2; i >= 0; i--)  
        { 
            noOfZeroes[i] = noOfZeroes[i + 1]; 
            if (arr[i] == 0) 
                noOfZeroes[i]++; 
        } 
  
        // Count total number of swaps by adding number 
        // of zeroes on right side of every one. 
        for (i = 0; i < n; i++)  
        { 
            if (arr[i] == 1) 
                count += noOfZeroes[i]; 
        } 
        return count; 
    } 
      
    // Driver Code 
    public static void main(String args[]) 
    { 
        int ar[] = { 0, 0, 1, 0, 1, 0, 1, 1 }; 
        System.out.println(findMinSwaps(ar, ar.length)); 
    } 
} 
  
// This code is contributed by Niraj_Pandey.
```

## Python3

```py
# Python3 code to find minimum number of 
# swaps to sort a binary array 
  
# Function to find minimum swaps to 
# sort an array of 0s and 1s. 
def findMinSwaps(arr, n) : 
    # Array to store count of zeroes 
    noOfZeroes = [0] * n 
    count = 0
      
    # Count number of zeroes 
    # on right side of every one. 
    noOfZeroes[n - 1] = 1 - arr[n - 1] 
    for i in range(n-2, -1, -1) : 
        noOfZeroes[i] = noOfZeroes[i + 1] 
        if (arr[i] == 0) : 
            noOfZeroes[i] = noOfZeroes[i] + 1
  
    # Count total number of swaps by adding  
    # number of zeroes on right side of  
    # every one. 
    for i in range(0, n) : 
        if (arr[i] == 1) : 
            count = count + noOfZeroes[i] 
  
    return count 
  
# Driver code 
arr = [ 0, 0, 1, 0, 1, 0, 1, 1 ] 
n = len(arr) 
print (findMinSwaps(arr, n)) 
  
# This code is contributed by Manish Shaw 
# (manishshaw1)
```

## C#

```cs
// C# code to find minimum number of 
// swaps to sort a binary array 
using System; 
  
class GFG { 
      
    static int findMinSwaps(int []arr, int n) 
    { 
          
        // Array to store count of zeroes 
        int []noOfZeroes = new int[n]; 
        int i, count = 0; 
  
        // Count number of zeroes 
        // on right side of every one. 
        noOfZeroes[n - 1] = 1 - arr[n - 1]; 
        for (i = n - 2; i >= 0; i--)  
        { 
            noOfZeroes[i] = noOfZeroes[i + 1]; 
            if (arr[i] == 0) 
                noOfZeroes[i]++; 
        } 
  
        // Count total number of swaps by  
        // adding number of zeroes on right 
        // side of every one. 
        for (i = 0; i < n; i++)  
        { 
            if (arr[i] == 1) 
                count += noOfZeroes[i]; 
        } 
          
        return count; 
    } 
      
    // Driver Code 
    public static void Main() 
    { 
        int []ar = { 0, 0, 1, 0, 1, 
                                0, 1, 1 }; 
                                  
        Console.WriteLine( 
              findMinSwaps(ar, ar.Length)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP code to find minimum number of 
// swaps to sort a binary array 
  
// Function to find minimum swaps to 
// sort an array of 0s and 1s. 
function findMinSwaps($arr, $n) 
{ 
    // Array to store count of zeroes 
    $noOfZeroes[$n] = array(); 
    $noOfZeroes = array_fill(0, $n, true); 
    $count = 0; 
  
    // Count number of zeroes 
    // on right side of every one. 
    $noOfZeroes[$n - 1] = 1 - $arr[$n - 1]; 
    for ($i = $n - 2; $i >= 0; $i--) 
    { 
        $noOfZeroes[$i] = $noOfZeroes[$i + 1]; 
        if ($arr[$i] == 0) 
            $noOfZeroes[$i]++; 
    } 
  
    // Count total number of swaps by adding  
    // number of zeroes on right side of every one. 
    for ($i = 0; $i < $n; $i++)  
    { 
        if ($arr[$i] == 1) 
            $count += $noOfZeroes[$i]; 
    } 
  
    return $count; 
} 
  
// Driver code 
$arr = array( 0, 0, 1, 0, 1, 0, 1, 1 ); 
$n = sizeof($arr); 
echo findMinSwaps($arr, $n); 
  
// This code is contributed by Sach_code 
?>
```

输出：

```
3
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。