# 将两个连续的相等值替换为一个更大的值

> 原文： [https://www.geeksforgeeks.org/replace-two-consecutive-equal-values-one-greater/](https://www.geeksforgeeks.org/replace-two-consecutive-equal-values-one-greater/)

系统会为您提供大小为`n`的数组。 您必须每次用单个值`x + 1`替换每对连续的值`x`，直到不再有这样的重复，然后再打印新数组。

> 输入：`5, 2, 1, 1, 2, 2`
> 
> 输出：`5 4`
> 
> 说明：
> 
> 步骤 1：遍历时遇到一对 1（取为 2）。 我们得到`5, 2, 2, 2, 2`
> 
> 步骤 2：将第一个遇到的 2 对替换为 3。我们得到`5, 3, 2, 2`
> 
> 步骤 3：再次将 2 对替换为 3，我们得到`5, 3, 3`
> 
> 步骤 4：将最近形成的 3 对换成 4。我们得到`5, 4`
> 
> 这是我们所需要的答案。
> 
> 输入：`4, 5, 11, 2, 5, 7, 2`
> 
> 输出：`4 5 11 2 5 7 2`


**方法**：在此问题中，您必须遍历整数数组并检查是否有两个连续的整数具有相同的值`X`。然后必须用单个整数`X + 1`替换该对整数。 之后，您必须通过重新遍历数组并执行相同的操作来开始新的步骤。

## C++ 

```cpp

// C++ program to replace two elements with equal 
// values with one greater. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to replace consecutive equal  
// elements 
void replace_elements(int arr[], int n) 
{ 
    int pos = 0;  // Index in result 

    for (int i = 0; i < n; i++) { 
        arr[pos++] = arr[i]; 

        while (pos > 1 && arr[pos - 2] ==  
                          arr[pos - 1]) { 
            pos--; 
            arr[pos - 1]++; 
        } 
    } 

    // to print new array 
    for (int i = 0; i < pos; i++) 
        cout << arr[i] << " "; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 6, 4, 3, 4, 3, 3, 5 }; 
    int n = sizeof(arr) / sizeof(int); 
    replace_elements(arr, n); 
    return 0; 
} 

```

## Java

```java

// java program to replace two elements 
// with equal values with one greater. 
public class GFG { 

    // Function to replace consecutive equal  
    // elements 
    static void replace_elements(int arr[], int n) 
    { 
        int pos = 0; // Index in result 

        for (int i = 0; i < n; i++) { 
            arr[pos++] = arr[i]; 

            while (pos > 1 && arr[pos - 2] ==  
                                  arr[pos - 1]) 
            { 
                pos--; 
                arr[pos - 1]++; 
            } 
        } 

        // to print new array 
        for (int i = 0; i < pos; i++) 
            System.out.print( arr[i] + " "); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 6, 4, 3, 4, 3, 3, 5 }; 
        int n = arr.length; 
        replace_elements(arr, n); 
    } 
} 

// This code is contributed by Sam007 

```

## Python3

```py

# python program to replace two elements 
# with equal values with one greater. 
from __future__ import print_function 

# Function to replace consecutive equal  
# elements 
def replace_elements(arr, n): 

    pos = 0 # Index in result 

    for i in range(0, n): 
        arr[pos] = arr[i] 
        pos = pos + 1
        while (pos > 1 and arr[pos - 2] 
                        == arr[pos - 1]): 
            pos -= 1
            arr[pos - 1] += 1

    # to print new array 
    for i in range(0, pos): 
        print(arr[i], end=" ") 

# Driver Code 
arr = [ 6, 4, 3, 4, 3, 3, 5 ] 
n = len(arr) 
replace_elements(arr, n) 

# This code is contributed by Sam007 

```

## C# 

```cs

// C# program to replace two elements 
// with equal values with one greater. 
using System; 

class GFG { 

    // Function to replace consecutive equal  
    // elements 
    static void replace_elements(int []arr, int n) 
    { 
        int pos = 0; // Index in result 

        for (int i = 0; i < n; i++) { 
            arr[pos++] = arr[i]; 

            while (pos > 1 && arr[pos - 2] ==  
                                  arr[pos - 1]) 
            { 
                pos--; 
                arr[pos - 1]++; 
            } 
        } 

        // to print new array 
        for (int i = 0; i < pos; i++) 
            Console.Write( arr[i] + " "); 
    } 

    // Driver code 
    static void Main() 
    { 
        int []arr = { 6, 4, 3, 4, 3, 3, 5 }; 
        int n = arr.Length; 
        replace_elements(arr, n); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP program to replace two  
// elements with equal 
// values with one greater. 

// Function to replace consecutive 
// equal elements 
function replace_elements($arr,$n) 
{ 
    // Index in result 
    $pos = 0;  

    for ($i = 0; $i < $n; $i++)  
    { 
        $arr[$pos++] = $arr[$i]; 

        while ($pos > 1 && $arr[$pos - 2] ==  
                        $arr[$pos - 1]) 
        { 
            $pos--; 
            $arr[$pos - 1]++; 
        } 
    } 

    // to print new array 
    for ($i = 0; $i < $pos; $i++) 
        echo $arr[$i] . " "; 
} 

    // Driver Code 
    $arr = array(6, 4, 3, 4, 3, 3, 5); 
    $n = count($arr); 
    replace_elements($arr, $n); 

// This code is contributed by Sam007\. 
?> 

```

**输出**：

```
6 4 3 6

```



* * *

* * *



