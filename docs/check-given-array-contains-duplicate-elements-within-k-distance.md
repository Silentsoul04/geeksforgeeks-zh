# 检查给定数组是否包含彼此之间`k`距离内的重复元素

> 原文： [https://www.geeksforgeeks.org/check-given-array-contains-duplicate-elements-within-k-distance/](https://www.geeksforgeeks.org/check-given-array-contains-duplicate-elements-within-k-distance/)

给定一个未排序的数组，其中可能包含重复项。 还给定一个小于数组大小的数字`k`。 编写一个函数，如果数组包含`k`个距离内的重复项，则返回`true`。

**示例**：

```
Input: k = 3, arr[] = {1, 2, 3, 4, 1, 2, 3, 4}
Output: false
All duplicates are more than k distance away.

Input: k = 3, arr[] = {1, 2, 3, 1, 4, 5}
Output: true
1 is repeated at distance 3.

Input: k = 3, arr[] = {1, 2, 3, 4, 5}
Output: false

Input: k = 3, arr[] = {1, 2, 3, 4, 4}
Output: true
```



**简单解决方案**是要运行两个循环。 外循环选择每个元素`arr[i]`作为起始元素，内循环比较`arr[i]`的`k`距离内的所有元素。 该解决方案的时间复杂度为`O(kn)`。

我们可以使用哈希在`Θ(n)`时间解决此问题。 这个想法是通过向哈希添加元素来实现的。 我们还将删除与当前元素相距`k`个以上距离的元素。 以下是详细的算法。

1.  创建一个空的哈希表。

2.  从左到右遍历所有元素。 令当前元素为`arr[i]`。

    1.  如果哈希表中存在当前元素`arr[i]`，则返回`true`。

    2.  如果`i`大于或等于`k`，则将`arr[i]`添加到哈希并从哈希中删除`arr[i-k]`。

## C++ 

```cpp

#include<bits/stdc++.h> 
using namespace std; 

/* C++ program to Check if a given array contains duplicate 
   elements within k distance from each other */
bool checkDuplicatesWithinK(int arr[], int n, int k) 
{ 
    // Creates an empty hashset 
    unordered_set<int> myset; 

    // Traverse the input array 
    for (int i = 0; i < n; i++) 
    { 
        // If already present n hash, then we found 
        // a duplicate within k distance 
        if (myset.find(arr[i]) != myset.end()) 
            return true; 

        // Add this item to hashset 
        myset.insert(arr[i]); 

        // Remove the k+1 distant item 
        if (i >= k) 
            myset.erase(arr[i-k]); 
    } 
    return false; 
} 

// Driver method to test above method 
int main () 
{ 
    int arr[] = {10, 5, 3, 4, 3, 5, 6}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    if (checkDuplicatesWithinK(arr, n, 3)) 
        cout << "Yes"; 
    else
        cout << "No"; 
} 

//This article is contributed by Chhavi 

```

## Java

```java

/* Java program to Check if a given array contains duplicate  
   elements within k distance from each other */
import java.util.*; 

class Main 
{ 
    static boolean checkDuplicatesWithinK(int arr[], int k) 
    { 
        // Creates an empty hashset 
        HashSet<Integer> set = new HashSet<>(); 

        // Traverse the input array 
        for (int i=0; i<arr.length; i++) 
        { 
            // If already present n hash, then we found  
            // a duplicate within k distance 
            if (set.contains(arr[i])) 
               return true; 

            // Add this item to hashset 
            set.add(arr[i]); 

            // Remove the k+1 distant item 
            if (i >= k) 
              set.remove(arr[i-k]); 
        } 
        return false; 
    } 

    // Driver method to test above method 
    public static void main (String[] args) 
    { 
        int arr[] = {10, 5, 3, 4, 3, 5, 6}; 
        if (checkDuplicatesWithinK(arr, 3)) 
           System.out.println("Yes"); 
        else
           System.out.println("No"); 
    } 
}

```

## Python 3

```py

# Python 3 program to Check if a given array  
# contains duplicate elements within k distance 
# from each other  
def checkDuplicatesWithinK(arr, n, k): 

    # Creates an empty list 
    myset = [] 

    # Traverse the input array 
    for i in range(n): 

        # If already present n hash, then we  
        # found a duplicate within k distance 
        if arr[i] in myset: 
            return True

        # Add this item to hashset 
        myset.append(arr[i]) 

        # Remove the k+1 distant item 
        if (i >= k): 
            myset.remove(arr[i - k]) 
    return False

# Driver Code 
if __name__ == "__main__": 

    arr = [10, 5, 3, 4, 3, 5, 6] 
    n = len(arr) 
    if (checkDuplicatesWithinK(arr, n, 3)): 
        print("Yes") 
    else: 
        print("No") 

# This code is contributed by ita_c 

```

## C# 

```cs

/* C# program to Check if a given 
array contains duplicate elements  
within k distance from each other */
using System; 
using System.Collections.Generic; 

class GFG 
{ 
    static bool checkDuplicatesWithinK(int []arr, int k) 
    { 
        // Creates an empty hashset 
        HashSet<int> set = new HashSet<int>(); 

        // Traverse the input array 
        for (int i = 0; i < arr.Length; i++) 
        { 
            // If already present n hash, then we found  
            // a duplicate within k distance 
            if (set.Contains(arr[i])) 
                return true; 

            // Add this item to hashset 
            set.Add(arr[i]); 

            // Remove the k+1 distant item 
            if (i >= k) 
                set.Remove(arr[i - k]); 
        } 
        return false; 
    } 

    // Driver code 
    public static void Main (String[] args) 
    { 
        int []arr = {10, 5, 3, 4, 3, 5, 6}; 
        if (checkDuplicatesWithinK(arr, 3)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code has been contributed 
// by 29AjayKumar 

```

**输出**：

```
Yes
```

