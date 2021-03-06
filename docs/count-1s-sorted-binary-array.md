# 在排序的二进制数组中计数 1

> 原文： [https://www.geeksforgeeks.org/count-1s-sorted-binary-array/](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/)

给定二进制数组以非递增顺序排序，请计算其中的 1 的数量。

例子：

```
Input: arr[] = {1, 1, 0, 0, 0, 0, 0}
Output: 2

Input: arr[] = {1, 1, 1, 1, 1, 1, 1}
Output: 7

Input: arr[] = {0, 0, 0, 0, 0, 0, 0}
Output: 0

```

一个简单的解决方案是线性遍历数组。 简单解决方案的时间复杂度为`O(n)`。 我们可以使用[二分搜索](http://quiz.geeksforgeeks.org/binary-search/)查找`O(Logn)`时间的计数。 这个想法是使用二分搜索查找 1 的最后一次出现。 一旦找到索引最后一次出现，我们将返回`index +1`作为计数。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to count one's in a boolean array 
#include <bits/stdc++.h> 
using namespace std; 

/* Returns counts of 1's in arr[low..high].  The array is 
   assumed to be sorted in non-increasing order */
int countOnes(bool arr[], int low, int high) 
{ 
  if (high >= low) 
  { 
    // get the middle index 
    int mid = low + (high - low)/2; 

    // check if the element at middle index is last 1 
    if ( (mid == high || arr[mid+1] == 0) && (arr[mid] == 1)) 
      return mid+1; 

    // If element is not last 1, recur for right side 
    if (arr[mid] == 1) 
      return countOnes(arr, (mid + 1), high); 

    // else recur for left side 
    return countOnes(arr, low, (mid -1)); 
  } 
  return 0; 
} 

/* Driver program to test above functions */
int main() 
{ 
   bool arr[] = {1, 1, 1, 1, 0, 0, 0}; 
   int n = sizeof(arr)/sizeof(arr[0]); 
   cout << "Count of 1's in given array is " << countOnes(arr, 0, n-1); 
   return 0; 
}

```

## Python

```py

# Python program to count one's in a boolean array 

# Returns counts of 1's in arr[low..high].  The array is 
# assumed to be sorted in non-increasing order 
def countOnes(arr,low,high): 

    if high>=low: 

        # get the middle index 
        mid = low + (high-low)/2

        # check if the element at middle index is last 1 
        if ((mid == high or arr[mid+1]==0) and (arr[mid]==1)): 
            return mid+1

        # If element is not last 1, recur for right side 
        if arr[mid]==1: 
            return countOnes(arr, (mid+1), high) 

        # else recur for left side 
        return countOnes(arr, low, mid-1) 

    return 0

# Driver function 
arr=[1, 1, 1, 1, 0, 0, 0] 
print "Count of 1's in given array is",countOnes(arr, 0 , len(arr)-1) 

# This code is contributed by __Devesh Agrawal__ 

```

## Java

```java

// Java program to count 1's in a sorted array 
class CountOnes 
{ 
    /* Returns counts of 1's in arr[low..high].  The 
       array is assumed to be sorted in non-increasing 
       order */
    int countOnes(int arr[], int low, int high) 
    { 
      if (high >= low) 
      { 
        // get the middle index 
        int mid = low + (high - low)/2; 

        // check if the element at middle index is last 1 
        if ( (mid == high || arr[mid+1] == 0) && 
             (arr[mid] == 1)) 
          return mid+1; 

        // If element is not last 1, recur for right side 
        if (arr[mid] == 1) 
          return countOnes(arr, (mid + 1), high); 

        // else recur for left side 
        return countOnes(arr, low, (mid -1)); 
      } 
      return 0; 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
       CountOnes ob = new CountOnes(); 
       int arr[] = {1, 1, 1, 1, 0, 0, 0}; 
       int n = arr.length; 
       System.out.println("Count of 1's in given array is " + 
                           ob.countOnes(arr, 0, n-1) ); 
    } 
} 
/* This code is contributed by Rajat Mishra */

```

## C# 

```cs

// C# program to count 1's in a sorted array 
using System; 

class GFG { 

    /* Returns counts of 1's in arr[low..high]. 
    The array is assumed to be sorted in 
    non-increasing order */
    static int countOnes(int []arr, int low, int high) 
    { 
        if (high >= low) 
        { 

            // get the middle index 
            int mid = low + (high - low) / 2; 

            // check if the element at middle  
            // index is last 1 
            if ( (mid == high || arr[mid+1] == 0) 
                               && (arr[mid] == 1)) 
            return mid+1; 

            // If element is not last 1, recur 
            // for right side 
            if (arr[mid] == 1) 
                return countOnes(arr, (mid + 1), high); 

            // else recur for left side 
            return countOnes(arr, low, (mid - 1)); 
        } 

        return 0; 
    } 

    /* Driver program to test above functions */
    public static void Main() 
    { 
        int []arr = {1, 1, 1, 1, 0, 0, 0}; 
        int n = arr.Length; 

        Console.WriteLine("Count of 1's in given "
          + "array is " + countOnes(arr, 0, n-1) ); 
    } 
} 

// This code is contributed by Sam007\. 

```

## PHP

```php

<?php 
// PHP program to count one's in a 
// boolean array 

/* Returns counts of 1's in arr[low..high]. 
The array is assumed to be sorted in  
non-increasing order */
function countOnes( $arr, $low, $high) 
{ 
    if ($high >= $low) 
    { 
        // get the middle index 
        $mid = $low + ($high - $low)/2; 

        // check if the element at middle 
        // index is last 1 
        if ( ($mid == $high or $arr[$mid+1] == 0)  
                           and ($arr[$mid] == 1)) 
            return $mid+1; 

        // If element is not last 1, recur for  
        // right side 
        if ($arr[$mid] == 1) 
            return countOnes($arr, ($mid + 1), 
                                          $high); 

        // else recur for left side 
        return countOnes($arr, $low, ($mid -1)); 
    } 

    return 0; 
} 

/* Driver program to test above functions */
$arr = array(1, 1, 1, 1, 0, 0, 0); 
$n = count($arr); 
echo "Count of 1's in given array is " ,  
                      countOnes($arr, 0, $n-1); 

// This code is contributed by anuj_67\. 
?> 

```

输出：

```
Count of 1's in given array is 4
```

上述解决方案的时间复杂度为`O(Logn)`。

