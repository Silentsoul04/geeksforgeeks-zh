# 检查数组中是否存在两个元素，总和等于数组其余部分的总和

> 原文： [https://www.geeksforgeeks.org/check-exist-two-elements-array-whose-sum-equal-sum-rest-array/](https://www.geeksforgeeks.org/check-exist-two-elements-array-whose-sum-equal-sum-rest-array/)

我们有一个整数数组，我们必须在数组中找到两个这样的元素，以使这两个元素的总和等于数组中其余元素的总和。

**示例**：

```
Input  : arr[] = {2, 11, 5, 1, 4, 7}
Output : Elements are 4 and 11
Note that 4 + 11 = 2 + 5 + 1 + 7

Input  : arr[] = {2, 4, 2, 1, 11, 15}
Output : Elements do not exist

```



**简单解决方案**是逐对考虑每一对，找到其总和，然后将总和与其余元素的总和进行比较。 如果找到一对总和等于其余元素的对，则打印该对并返回`true`。 该解决方案的时间复杂度为`O(n ^ 3)`。

一种有效的**解决方案**是找到所有数组元素的总和。 将该总和设为`sum`。 现在，任务简化为找到总和等于`sum / 2`的一对。

另一个优化方法是，只有在整个数组的和为偶数的情况下，才可以存在一对，因为我们基本上将它分成相等的两个部分。

1.  查找整个数组的总和。 将该总和设为`sum`。

2.  如果总和为奇数，则返回`false`。

3.  使用[这里讨论的基于散列的方法](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)作为方法 2，找到总和等于`sum / 2`的当前对。如果找到一对，请打印并返回`true`。

4.  如果不存在任何对，则返回`false`。

下面是上述步骤的实现。

## C++ 

```cpp

// C++ program to find whether two elements exist 
// whose sum is equal to sum of rest of the elements. 
#include<bits/stdc++.h> 
using namespace std; 

// Function to check whether two elements exist 
// whose sum is equal to sum of rest of the elements. 
bool checkPair(int arr[],int n) 
{ 
    // Find sum of whole array 
    int sum = 0; 
    for (int i=0; i<n; i++) 
        sum += arr[i]; 

    // If sum of array is not even than we can not 
    // divide it into two part 
    if (sum%2 != 0) 
        return false; 

    sum = sum/2; 

    // For each element arr[i], see if there is 
    // another element with vaalue sum - arr[i] 
    unordered_set<int> s; 
    for (int i=0; i<n; i++) 
    { 
        int val = sum-arr[i]; 

        // If element exist than return the pair 
        if (s.find(val) != s.end()) 
        { 
            printf("Pair elements are %d and %d\n", 
                                    arr[i], val); 
            return true; 
        } 

        s.insert(arr[i]); 
    } 

    return false; 
} 

// Driver program. 
int main() 
{ 
    int arr[] = {2, 11, 5, 1, 4, 7}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    if (checkPair(arr, n) == false) 
       printf("No pair found"); 
    return 0; 
} 

```

## Java

```java

// Java program to find whether two elements exist 
// whose sum is equal to sum of rest of the elements. 
import java.util.*; 

class GFG  
{ 

    // Function to check whether two elements exist 
    // whose sum is equal to sum of rest of the elements. 
    static boolean checkPair(int arr[], int n) 
    { 
        // Find sum of whole array 
        int sum = 0; 
        for (int i = 0; i < n; i++) 
        { 
            sum += arr[i]; 
        } 

        // If sum of array is not even than we can not 
        // divide it into two part 
        if (sum % 2 != 0)  
        { 
            return false; 
        } 

        sum = sum / 2; 

        // For each element arr[i], see if there is 
        // another element with vaalue sum - arr[i] 
        HashSet<Integer> s = new HashSet<Integer>(); 
        for (int i = 0; i < n; i++) 
        { 
            int val = sum - arr[i]; 

            // If element exist than return the pair 
            if (s.contains(val) &&  
                val == (int) s.toArray()[s.size() - 1])  
            { 
                System.out.printf("Pair elements are %d and %d\n", 
                        arr[i], val); 
                return true; 
            } 
            s.add(arr[i]); 
        } 
        return false; 
    } 

    // Driver program. 
    public static void main(String[] args) 
    { 
        int arr[] = {2, 11, 5, 1, 4, 7}; 
        int n = arr.length; 
        if (checkPair(arr, n) == false)  
        { 
            System.out.printf("No pair found"); 
        } 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

## Python3

```py

# Python3 program to find whether  
# two elements exist whose sum is 
# equal to sum of rest of the elements.  

# Function to check whether two  
# elements exist whose sum is equal  
# to sum of rest of the elements.  
def checkPair(arr, n): 
    s = set() 
    sum = 0

    # Find sum of whole array  
    for i in range(n): 
        sum += arr[i] 

    # / If sum of array is not  
    # even than we can not  
    # divide it into two part  
    if sum % 2 != 0: 
        return False
    sum = sum / 2

    # For each element arr[i], see if  
    # there is another element with  
    # value sum - arr[i]  
    for i in range(n): 
        val = sum - arr[i] 
        if arr[i] not in s: 
            s.add(arr[i]) 

        # If element exist than  
        # return the pair  
        if val in s: 
            print("Pair elements are",  
                   arr[i], "and", int(val)) 

# Driver Code  
arr = [2, 11, 5, 1, 4, 7] 
n = len(arr) 
if checkPair(arr, n) == False: 
    print("No pair found") 

# This code is contributed  
# by Shrikant13 

```

## C# 

```cs

// C# program to find whether two elements exist 
// whose sum is equal to sum of rest of the elements. 
using System;  
using System.Collections.Generic;  

class GFG  
{ 

    // Function to check whether two elements exist 
    // whose sum is equal to sum of rest of the elements. 
    static bool checkPair(int []arr, int n) 
    { 
        // Find sum of whole array 
        int sum = 0; 
        for (int i = 0; i < n; i++) 
        { 
            sum += arr[i]; 
        } 

        // If sum of array is not even than we can not 
        // divide it into two part 
        if (sum % 2 != 0)  
        { 
            return false; 
        } 

        sum = sum / 2; 

        // For each element arr[i], see if there is 
        // another element with vaalue sum - arr[i] 
        HashSet<int> s = new HashSet<int>(); 
        for (int i = 0; i < n; i++) 
        { 
            int val = sum - arr[i]; 

            // If element exist than return the pair 
            if (s.Contains(val)) 
            { 
                Console.Write("Pair elements are {0} and {1}\n", 
                        arr[i], val); 
                return true; 
            } 
            s.Add(arr[i]); 
        } 
        return false; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int []arr = {2, 11, 5, 1, 4, 7}; 
        int n = arr.Length; 
        if (checkPair(arr, n) == false)  
        { 
            Console.Write("No pair found"); 
        } 
    } 
} 

// This code contributed by Rajput-Ji 

```

## PHP

```php

<?php  
// PHP program to find whether two elements exist 
// whose sum is equal to sum of rest of the elements. 

// Function to check whether two elements exist 
// whose sum is equal to sum of rest of the elements. 
function checkPair(&$arr, $n) 
{ 
    // Find sum of whole array 
    $sum = 0; 
    for ($i = 0; $i < $n; $i++) 
        $sum += $arr[$i]; 

    // If sum of array is not even than we  
    // can not divide it into two part 
    if ($sum % 2 != 0) 
        return false; 

    $sum = $sum / 2; 

    // For each element arr[i], see if there is 
    // another element with vaalue sum - arr[i] 
    $s = array(); 
    for ($i = 0; $i < $n; $i++) 
    { 
        $val = $sum - $arr[$i]; 

        // If element exist than return the pair 
        if (array_search($val, $s)) 
        { 
            echo "Pair elements are " . $arr[$i] . 
                 " and " . $val . "\n"; 

            return true; 
        } 

        array_push($s, $arr[$i]); 
    } 

    return false; 
} 

// Driver Code 
$arr = array(2, 11, 5, 1, 4, 7); 
$n = sizeof($arr); 
if (checkPair($arr, $n) == false) 
    echo "No pair found"; 

// This code is contributed by ita_c 
?> 

```

**输出**：

```
Pair elements are 4 and 11
```

**时间复杂度**：`O(n)`。 [`unordered_set`](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)使用哈希实现。 时间复杂度哈希搜索和插入在这里假定为`O(1)`。

