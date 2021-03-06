# 两个数组的偶对的绝对差的最小和

> 原文： [https://www.geeksforgeeks.org/minimum-sum-absolute-difference-pairs-two-arrays/](https://www.geeksforgeeks.org/minimum-sum-absolute-difference-pairs-two-arrays/)

给定两个等长为`n`的数组`a[]`和`b[]`。 任务是将数组`a`的每个元素与数组`b`中的元素配对，以使对的总和`S`的绝对差最小。

假设`a`的两个元素`a[i]`和`a[j]`（`i != j`）与`b`的元素`b[p]`和`b[q]`分别配对，然后`p`不等于`q`。

**示例**：

```
Input :  a[] = {3, 2, 1}
         b[] = {2, 1, 3}
Output : 0

Input :  n = 4
         a[] = {4, 1, 8, 7}
         b[] = {2, 3, 6, 5}
Output : 6

```



解决问题的方法是简单的贪婪方法。 它由**两个**步骤组成。

**步骤 1**：以`O(N log N)`时间对两个数组进行排序。

**步骤 2**：找出两个数组的每对**对应元素**（元素在相同索引处）的绝对差，并将结果加到总和`S`。 该步骤的时间复杂度为`O(n)`。

因此，程序的整体时间复杂度为`O(N log N)`。

## C++ 

```cpp

// C++ program to find minimum sum of absolute 
// differences of two arrays. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns minimum possible pairwise absolute 
// difference of two arrays. 
long long int findMinSum(int a[], int b[], int n) 
{ 
    // Sort both arrays 
    sort(a, a+n); 
    sort(b, b+n); 

    // Find sum of absolute differences 
    long long int sum= 0 ; 
    for (int i=0; i<n; i++) 
        sum = sum + abs(a[i]-b[i]); 

    return sum; 
} 

// Driver code 
int main() 
{ 
    // Both a[] and b[] must be of same size. 
    long long int a[] = {4, 1, 8, 7}; 
    long long int b[] = {2, 3, 6, 5}; 
    int n = sizeof(a)/sizeof(a[0]); 
    printf("%lld\n", findMinSum(a, b, n)); 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum sum of 
// absolute differences of two arrays. 
import java.util.Arrays; 

class MinSum 
{ 
    // Returns minimum possible pairwise  
    // absolute difference of two arrays. 
    static long findMinSum(long a[], long b[], long n) 
    { 
        // Sort both arrays 
        Arrays.sort(a); 
        Arrays.sort(b); 

        // Find sum of absolute differences 
        long sum = 0 ; 
        for (int i = 0; i < n; i++) 
            sum = sum + Math.abs(a[i] - b[i]); 

        return sum; 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        // Both a[] and b[] must be of same size. 
        long a[] = {4, 1, 8, 7}; 
        long b[] = {2, 3, 6, 5}; 
        int n = a.length; 
        System.out.println(findMinSum(a, b, n)); 
    }     
} 

// This code is contributed by Raghav Sharma 

```

## Python3

```py

# Python3 program to find minimum sum  
# of absolute differences of two arrays. 
def findMinSum(a, b, n): 

    # Sort both arrays 
    a.sort() 
    b.sort() 

    # Find sum of absolute differences 
    sum = 0

    for i in range(n): 
        sum = sum + abs(a[i] - b[i]) 

    return sum

# Driver program 

# Both a[] and b[] must be of same size. 
a = [4, 1, 8, 7] 
b = [2, 3, 6, 5] 
n = len(a) 

print(findMinSum(a, b, n)) 

# This code is contributed by Anant Agarwal. 

```

## C# 

```cs

// C# program to find minimum sum of 
// absolute differences of two arrays. 
using System; 

class MinSum { 

    // Returns minimum possible pairwise  
    // absolute difference of two arrays. 
    static long findMinSum(long []a, long []b, 
                           long n) 
    { 

        // Sort both arrays 
        Array.Sort(a); 
        Array.Sort(b); 

        // Find sum of absolute differences 
        long sum = 0 ; 
        for (int i = 0; i < n; i++) 
            sum = sum + Math.Abs(a[i] - b[i]); 

        return sum; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        // Both a[] and b[] must be of same size. 
        long []a = {4, 1, 8, 7}; 
        long []b = {2, 3, 6, 5}; 
        int n = a.Length; 
        Console.Write(findMinSum(a, b, n)); 
    }  
} 

// This code is contributed by parashar... 

```

## PHP

```php

<?php 
// PHP program to find minimum sum  
// of absolute differences of two  
// arrays. 

// Returns minimum possible pairwise 
// absolute difference of two arrays. 
function findMinSum($a, $b, $n) 
{ 

    // Sort both arrays 
    sort($a);  
    sort($a, $n); 
    sort($b);  
    sort($b, $n); 

    // Find sum of absolute  
    // differences 
    $sum= 0 ; 
    for ($i = 0; $i < $n; $i++) 
        $sum = $sum + abs($a[$i] -  
                          $b[$i]); 

    return $sum; 
} 

    // Driver Code 
    // Both a[] and b[] must 
    // be of same size. 
    $a = array(4, 1, 8, 7); 
    $b = array(2, 3, 6, 5); 
    $n = sizeof($a); 
    echo(findMinSum($a, $b, $n)); 

// This code is contributed by nitin mittal. 
?> 

```

Output :

```
6

```

