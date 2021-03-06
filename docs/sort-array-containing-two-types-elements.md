# 对包含两种类型元素的数组进行排序

> 原文： [https://www.geeksforgeeks.org/sort-array-containing-two-types-elements/](https://www.geeksforgeeks.org/sort-array-containing-two-types-elements/)

给我们一个随机顺序为 0 和 1 的数组。 分隔数组左侧的 0 和右侧的 1。 遍历数组仅一次。

**示例**：

```
Input :  arr[] = [0, 1, 0, 1, 0, 0, 1, 1, 1, 0] 
Output : arr[] = [0, 0, 0, 0, 0, 1, 1, 1, 1, 1] 

Input :  arr[] = [1, 1, 1, 0, 1, 0, 0, 1, 1, 1, 1] 
Output : arr[] = [0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1] 

```



我们已经讨论了[将数组的 0 和 1 分离](https://www.geeksforgeeks.org/segregate-0s-and-1s-in-an-array-by-traversing-array-once)的解决方案。

在这篇文章中，讨论了一个新的解决方案。

**步骤 1**：在这里，我们可以采用两个指针，即类型 0（对于元素 0）从开头（索引 0）开始，以及类型 1（对于元素 1）从结束索引开始。

**步骤 2**：我们打算将 1 放置在数组的右侧。 一旦完成此操作，则将向数组的左侧肯定为 0 即可完成此操作。

我们比较索引类型为 0 的元素。

1.  如果为 1，则应将其移到右侧，因此一旦交换，我们需要将其与索引类型 1 交换，我们确定索引类型 1 的元素为 1，因此我们需要递减索引`type1`。

2.  否则它将是 0，那么我们需要简单地递增索引`type0`。

## C++ 

```cpp

// CPP program to sort an array with two types 
// of values in one traversal. 
#include <bits/stdc++.h> 
using namespace std; 

/* Method for segregation 0 and 1 given  
   input array */
void segregate0and1(int arr[], int n) 
{ 
    int type0 = 0; 
    int type1 = n - 1; 

    while (type0 < type1) { 
        if (arr[type0] == 1) { 
            swap(arr[type0], arr[type1]); 
            type1--; 
        } 
        else { 
            type0++; 
        } 
    } 
} 

// Driver program 
int main() 
{ 
    int arr[] = { 1, 1, 1, 0, 1, 0, 0, 1, 1, 1, 1 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    segregate0and1(arr, n); 
    for (int a : arr) 
        cout << a << " "; 
} 

```

## Java

```java

// Java program to sort an array with two types 
// of values in one traversal.public class GFG { 
    /* Method for segregation 0 and 1  
         given input array */
    static void segregate0and1(int arr[], int n) { 
        int type0 = 0; 
        int type1 = n - 1; 

        while (type0 < type1) { 
            if (arr[type0] == 1) { 

                // swap type0 and type1 
                arr[type0] = arr[type0] + arr[type1]; 
                arr[type1] = arr[type0]-arr[type1]; 
                arr[type0] = arr[type0]-arr[type1]; 
                type1--; 
            } else { 
                type0++; 
            } 
        } 
    } 

    // Driver program 
    public static void main(String[] args) { 
          int arr[] = { 1, 1, 1, 0, 1, 0, 0, 1, 1, 1, 1 }; 

          segregate0and1(arr, arr.length); 
          for (int a : arr) 
              System.out.print(a+" "); 
      } 
} 

```

## Python3

```py

# Python3 program to sort an array with  
# two types of values in one traversal. 

# Method for segregation 0 and  
# 1 given input array  
def segregate0and1(arr, n): 

    type0 = 0; type1 = n - 1

    while (type0 < type1):  
        if (arr[type0] == 1):  
            arr[type0], arr[type1] = arr[type1], arr[type0] 
            type1 -= 1

        else:  
            type0 += 1

# Driver Code 
arr = [1, 1, 1, 0, 1, 0, 0, 1, 1, 1, 1]  
n = len(arr) 
segregate0and1(arr, n) 
for i in range(0, n): 
    print(arr[i], end = " ") 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# program to sort an array with two types 
// of values in one traversal. 
using System; 

class GFG { 

    static void segregate0and1(int []arr, int n) 
    { 
        int type0 = 0; 
        int type1 = n - 1; 

        while (type0 < type1) 
        { 

            if (arr[type0] == 1) 
            { 

                // swap type0 and type1 
                arr[type0] = arr[type0] + arr[type1]; 
                arr[type1] = arr[type0]-arr[type1]; 
                arr[type0] = arr[type0]-arr[type1]; 
                type1--; 
            }  
            else { 
                type0++; 
            } 
        } 
    } 

    // Driver program 
    public static void Main() 
    { 

        int []arr = { 1, 1, 1, 0, 1, 0, 0, 
                             1, 1, 1, 1 }; 

        segregate0and1(arr, arr.Length); 

        for (int i = 0; i < arr.Length; i++) 
            Console.Write(arr[i] + " "); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to sort an array with two  
// types of values in one traversal. 

/* Method for segregation 0 and 1  
given input array */
function segregate0and1($arr, $n) 
{ 
    $type0 = 0; 
    $type1 = $n - 1; 

    while ($type0 < $type1) 
    { 
        if ($arr[$type0] == 1) 
        { 
            $temp = $arr[$type0]; 
            $arr[$type0] = $arr[$type1]; 
            $arr[$type1] = $temp; 

            $type1--; 
        } 
        else 
        { 
            $type0++; 
        } 
    } 
    return $arr; 
} 

// Driver Code 
$arr = array( 1, 1, 1, 0, 1, 0,  
                 0, 1, 1, 1, 1 ); 
$n = count($arr); 
$arr1 = segregate0and1($arr, $n); 
for($i = 0; $i < $n ; $i++ ) 
echo $arr1[$i] . " "; 

// This code is contributed by Rajput-Ji 
?> 

```

时间复杂度：`O(n)`。

**输出**：

```
0 0 0 1 1 1 1 1 1 1 1

```



* * *

* * *



