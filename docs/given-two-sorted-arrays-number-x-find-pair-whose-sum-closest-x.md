# 从两个排序的数组中找到最接近`x`的偶对

> 原文： [https://www.geeksforgeeks.org/given-two-sorted-arrays-number-x-find-pair-whose-sum-closest-x/](https://www.geeksforgeeks.org/given-two-sorted-arrays-number-x-find-pair-whose-sum-closest-x/)

给定两个已排序的数组和一个数字`x`，请找到总和最接近`x`的对，**该对具有每个数组中的元素**。

给定两个数组`ar1[0…m-1]`和`ar2[0..n-1]`以及一个数字`x`，我们需要找到对`ar1[i] + ar2[j]`，使得`ar1[i] + ar2[j] – x`最小。

例：

```
Input:  ar1[] = {1, 4, 5, 7};
        ar2[] = {10, 20, 30, 40};
        x = 32      
Output:  1 and 30

Input:  ar1[] = {1, 4, 5, 7};
        ar2[] = {10, 20, 30, 40};
        x = 50      
Output:  7 and 40

```

**我们强烈建议您最小化您的浏览器，然后自己尝试。**

一个**简单解决方案**是运行两个循环。 外循环考虑第一个数组的每个元素，内循环检查第二个数组中的对。 我们跟踪`ar1[i] + ar2[j]`与`x`之间的最小差。

我们可以使用以下步骤在`O(n)`时间中完成。

1.  使用归并排序的[合并过程](http://geeksquiz.com/merge-sort/)，将给定的两个数组合并为大小为`m + n`的辅助数组。 合并时，请保留另一个大小为`m + n`的布尔数组，以指示合并数组中的当前元素是来自`ar1[]`还是`ar2[]`。

2.  考虑合并数组，并使用[线性时间算法](http://geeksquiz.com/given-sorted-array-number-x-find-pair-array-whose-sum-closest-x/)找到总和最接近`x`的对。 我们还需要考虑仅具有`ar1[]`中一个元素和`ar2[]`中另一个元素的那些对，为此我们使用了布尔数组。

**我们可以一次通过并增加`O(1)`空间吗？**

想法是从一个数组的左侧开始，然后从另一数组的右侧开始，并使用与上述方法的步骤 2 相同的算法。 以下是详细的算法。

```
1) Initialize a variable diff as infinite (Diff is used to store the 
   difference between pair and x).  We need to find the minimum diff.
2) Initialize two index variables l and r in the given sorted array.
       (a) Initialize first to the leftmost index in ar1:  l = 0
       (b) Initialize second  the rightmost index in ar2:  r = n-1
3) Loop while  l = 0
       (a) If  abs(ar1[l] + ar2[r] - sum) < diff  then 
           update diff and result 
       (b) If (ar1[l] + ar2[r] <  sum )  then l++
       (c) Else r--    
4) Print the result. 
```

以下是此方法的实现。

## C++ 

```cpp

// C++ program to find the pair from two sorted arays such 
// that the sum of pair is closest to a given number x 
#include <iostream> 
#include <climits> 
#include <cstdlib> 
using namespace std; 

// ar1[0..m-1] and ar2[0..n-1] are two given sorted arrays 
// and x is given number. This function prints the pair  from 
// both arrays such that the sum of the pair is closest to x. 
void printClosest(int ar1[], int ar2[], int m, int n, int x) 
{ 
    // Initialize the diff between pair sum and x. 
    int diff = INT_MAX; 

    // res_l and res_r are result indexes from ar1[] and ar2[] 
    // respectively 
    int res_l, res_r; 

    // Start from left side of ar1[] and right side of ar2[] 
    int l = 0, r = n-1; 
    while (l<m && r>=0) 
    { 
       // If this pair is closer to x than the previously 
       // found closest, then update res_l, res_r and diff 
       if (abs(ar1[l] + ar2[r] - x) < diff) 
       { 
           res_l = l; 
           res_r = r; 
           diff = abs(ar1[l] + ar2[r] - x); 
       } 

       // If sum of this pair is more than x, move to smaller 
       // side 
       if (ar1[l] + ar2[r] > x) 
           r--; 
       else  // move to the greater side 
           l++; 
    } 

    // Print the result 
    cout << "The closest pair is [" << ar1[res_l] << ", "
         << ar2[res_r] << "] \n"; 
} 

// Driver program to test above functions 
int main() 
{ 
    int ar1[] = {1, 4, 5, 7}; 
    int ar2[] = {10, 20, 30, 40}; 
    int m = sizeof(ar1)/sizeof(ar1[0]); 
    int n = sizeof(ar2)/sizeof(ar2[0]); 
    int x = 38; 
    printClosest(ar1, ar2, m, n, x); 
    return 0; 
} 

```

## Java

```java
// Java program to find closest pair in an array 
class ClosestPair 
{ 
    // ar1[0..m-1] and ar2[0..n-1] are two given sorted 
    // arrays/ and x is given number. This function prints 
    // the pair from both arrays such that the sum of the 
    // pair is closest to x. 
    void printClosest(int ar1[], int ar2[], int m, int n, int x) 
    { 
        // Initialize the diff between pair sum and x. 
        int diff = Integer.MAX_VALUE; 
  
        // res_l and res_r are result indexes from ar1[] and ar2[] 
        // respectively 
        int res_l = 0, res_r = 0; 
  
        // Start from left side of ar1[] and right side of ar2[] 
        int l = 0, r = n-1; 
        while (l<m && r>=0) 
        { 
           // If this pair is closer to x than the previously 
           // found closest, then update res_l, res_r and diff 
           if (Math.abs(ar1[l] + ar2[r] - x) < diff) 
           { 
               res_l = l; 
               res_r = r; 
               diff = Math.abs(ar1[l] + ar2[r] - x); 
           } 
  
           // If sum of this pair is more than x, move to smaller 
           // side 
           if (ar1[l] + ar2[r] > x) 
               r--; 
           else  // move to the greater side 
               l++; 
        } 
  
        // Print the result 
        System.out.print("The closest pair is [" + ar1[res_l] + 
                         ", " + ar2[res_r] + "]"); 
    } 
  
    // Driver program to test above functions 
    public static void main(String args[]) 
    { 
        ClosestPair ob = new ClosestPair(); 
        int ar1[] = {1, 4, 5, 7}; 
        int ar2[] = {10, 20, 30, 40}; 
        int m = ar1.length; 
        int n = ar2.length; 
        int x = 38; 
        ob.printClosest(ar1, ar2, m, n, x); 
    } 
} 
/*This code is contributed by Rajat Mishra */
```

## Python3

```py
# Python3 program to find the pair from 
# two sorted arays such that the sum  
# of pair is closest to a given number x 
import sys 
  
# ar1[0..m-1] and ar2[0..n-1] are two  
# given sorted arrays and x is given  
# number. This function prints the pair  
# from both arrays such that the sum  
# of the pair is closest to x. 
def printClosest(ar1, ar2, m, n, x): 
  
    # Initialize the diff between  
    # pair sum and x. 
    diff=sys.maxsize 
  
    # res_l and res_r are result  
    # indexes from ar1[] and ar2[] 
    # respectively. Start from left 
    # side of ar1[] and right side of ar2[] 
    l = 0
    r = n-1
    while(l < m and r >= 0): 
      
    # If this pair is closer to x than  
    # the previously found closest, 
    # then update res_l, res_r and diff 
        if abs(ar1[l] + ar2[r] - x) < diff: 
            res_l = l 
            res_r = r 
            diff = abs(ar1[l] + ar2[r] - x) 
      
  
    # If sum of this pair is more than x, 
    # move to smaller side 
        if ar1[l] + ar2[r] > x: 
            r=r-1
        else: # move to the greater side 
            l=l+1
      
  
    # Print the result 
    print("The closest pair is [", 
         ar1[res_l],",",ar2[res_r],"]") 
  
# Driver program to test above functions 
ar1 = [1, 4, 5, 7] 
ar2 = [10, 20, 30, 40] 
m = len(ar1) 
n = len(ar2) 
x = 38
printClosest(ar1, ar2, m, n, x) 
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find closest pair in 
// an array 
using System; 
  
class GFG { 
      
    // ar1[0..m-1] and ar2[0..n-1] are two 
    // given sorted arrays/ and x is given 
    // number. This function prints the  
    // pair from both arrays such that the 
    // sum of the pair is closest to x. 
    static void printClosest(int []ar1, 
            int []ar2, int m, int n, int x) 
    { 
          
        // Initialize the diff between pair 
        // sum and x. 
        int diff = int.MaxValue; 
  
        // res_l and res_r are result  
        // indexes from ar1[] and ar2[] 
        // respectively 
        int res_l = 0, res_r = 0; 
  
        // Start from left side of ar1[] 
        // and right side of ar2[] 
        int l = 0, r = n-1; 
        while (l < m && r >= 0) 
        { 
              
            // If this pair is closer to 
            // x than the previously 
            // found closest, then update 
            // res_l, res_r and diff 
            if (Math.Abs(ar1[l] +  
                       ar2[r] - x) < diff) 
            { 
                res_l = l; 
                res_r = r; 
                diff = Math.Abs(ar1[l] 
                            + ar2[r] - x); 
            } 
      
            // If sum of this pair is more 
            // than x, move to smaller 
            // side 
            if (ar1[l] + ar2[r] > x) 
                r--; 
            else // move to the greater side 
                l++; 
        } 
  
        // Print the result 
        Console.Write("The closest pair is [" 
                          + ar1[res_l] + ", "
                         + ar2[res_r] + "]"); 
    } 
  
    // Driver program to test above functions 
    public static void Main() 
    { 
        int []ar1 = {1, 4, 5, 7}; 
        int []ar2 = {10, 20, 30, 40}; 
        int m = ar1.Length; 
        int n = ar2.Length; 
        int x = 38; 
          
        printClosest(ar1, ar2, m, n, x); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// PHP program to find the pair  
// from two sorted arays such 
// that the sum of pair is  
// closest to a given number x 
  
// ar1[0..m-1] and ar2[0..n-1]  
// are two given sorted arrays 
// and x is given number. This 
// function prints the pair from 
// both arrays such that the sum 
// of the pair is closest to x. 
function printClosest($ar1, $ar2, 
                      $m, $n, $x) 
{ 
      
    // Initialize the diff between 
    // pair sum and x. 
    $diff = PHP_INT_MAX; 
  
    // res_l and res_r are result 
    // indexes from ar1[] and ar2[] 
    // respectively 
    $res_l;  
    $res_r; 
  
    // Start from left side of  
    // ar1[] and right side of ar2[] 
    $l = 0; 
    $r = $n - 1; 
    while ($l < $m and $r >= 0) 
    { 
          
        // If this pair is closer to  
        // x than the previously 
        // found closest, then  
        // update res_l, res_r and 
        // diff 
        if (abs($ar1[$l] + $ar2[$r] -  
                       $x) < $diff) 
        { 
            $res_l = $l; 
            $res_r = $r; 
            $diff = abs($ar1[$l] + 
                    $ar2[$r] - $x); 
        } 
      
        // If sum of this pair is  
        // more than x, move to smaller 
        // side 
        if ($ar1[$l] + $ar2[$r] > $x) 
            $r--; 
              
        // move to the greater side 
        else 
            $l++; 
    } 
  
    // Print the result 
    echo "The closest pair is [" , $ar1[$res_l] , ", "
                               , $ar2[$res_r] , "] \n"; 
} 
  
    // Driver Code 
    $ar1 = array(1, 4, 5, 7); 
    $ar2 = array(10, 20, 30, 40); 
    $m = count($ar1); 
    $n = count($ar2); 
    $x = 38; 
    printClosest($ar1, $ar2, $m, $n, $x); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
 The closest pair is [7, 30] 
```


[两个未排序数组之间的最小差值对](https://www.geeksforgeeks.org/smallest-difference-pair-values-two-unsorted-arrays/)。
