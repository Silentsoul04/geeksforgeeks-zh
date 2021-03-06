# 最大化总和为`K`的非重叠子数组的数量

> 原文：[https://www.geeksforgeeks.org/maximize-count-of-non-overlapping-subarrays-with-sum-k/](https://www.geeksforgeeks.org/maximize-count-of-non-overlapping-subarrays-with-sum-k/)

给定数组`arr[]`和整数`K`，任务是打印与`K`之和的非重叠子数组的最大数量。

**示例**：

> **输入**：`arr[] = {-2, 6, 6, 3, 5, 4, 1, 2, 8}, K = 10`
>
> **输出**：3
>
> **解释**：所有和为`K = 10`的不重叠子数组都是`{-2, 6, 6}`，`{5, 4, 1}`，`{2, 8}`。 因此，所需的计数为 3。
> 
> **输入**：`arr[] = {1, 1, 1}, K = 2`
>
> **输出**：1

**方法**：可以使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念解决此问题。 请按照以下步骤解决问题：

1.  初始化[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)以存储直到当前元素为止获得的所有前缀和。

2.  初始化变量`prefixSum`和`res`，以存储当前子数组的前缀和和分别等于`K`的子数组的数量。

3.  遍历数组，并为每个数组元素添加当前元素，以更新`prefixSum`。 现在，检查**集合**中是否已经存在`prefixSum – K`值。 如果确定为真，则将`res`递增，清除**集合**，然后重置`prefixSum`的值。

4.  重复上述步骤，直到遍历整个数组。 最后，打印`res`的值。

## C++ 14

```

// C++ Program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to count the maximum 
// number of subarrays with sum K 
int CtSubarr(int arr[], int N, int K) 
{ 

    // Stores all the distinct 
    // prefixSums obtained 
    unordered_set<int> st; 

    // Stores the prefix sum 
    // of the current subarray 
    int prefixSum = 0; 

    st.insert(prefixSum); 

    // Stores the count of 
    // subarrays with sum K 
    int res = 0; 

    for (int i = 0; i < N; i++) { 
        prefixSum += arr[i]; 

        // If a subarray with sum K 
        // is already found 
        if (st.count(prefixSum - K)) { 

            // Increase count 
            res += 1; 

            // Reset prefix sum 
            prefixSum = 0; 

            // Clear the set 
            st.clear(); 
            st.insert(0); 
        } 

        // Insert the prefix sum 
        st.insert(prefixSum); 
    } 
    return res; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { -2, 6, 6, 3, 5, 4, 1, 2, 8 }; 
    int N = sizeof(arr) / sizeof(arr[0]); 
    int K = 10; 
    cout << CtSubarr(arr, N, K); 
}

```

## Java

```java

// Java Program to implement 
// the above approach 
import java.util.*; 
class GFG{ 
    // Function to count the maximum 
    // number of subarrays with sum K 
    static int CtSubarr(int[] arr,  
                        int N, int K) 
    { 
        // Stores all the distinct 
        // prefixSums obtained 
        Set<Integer> st = new HashSet<Integer>(); 

        // Stores the prefix sum 
        // of the current subarray 
        int prefixSum = 0; 

        st.add(prefixSum); 

        // Stores the count of 
        // subarrays with sum K 
        int res = 0; 

        for (int i = 0; i < N; i++)  
        { 
            prefixSum += arr[i]; 

            // If a subarray with sum K 
            // is already found 
            if (st.contains(prefixSum - K))  
            { 
                // Increase count 
                res += 1; 

                // Reset prefix sum 
                prefixSum = 0; 

                // Clear the set 
                st.clear(); 
                st.add(0); 
            } 

            // Insert the prefix sum 
            st.add(prefixSum); 
        } 
        return res; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int arr[] = {-2, 6, 6, 3,  
                     5, 4, 1, 2, 8}; 
        int N = arr.length; 
        int K = 10; 
        System.out.println(CtSubarr(arr, N, K)); 
    } 
} 

// This code is contributed by Chitranayal

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to count the maximum  
# number of subarrays with sum K 
def CtSubarr(arr, N, K): 

    # Stores all the distinct 
    # prefixSums obtained 
    st = set() 

    # Stores the prefix sum 
    # of the current subarray 
    prefixSum = 0

    st.add(prefixSum) 

    # Stores the count of 
    # subarrays with sum K 
    res = 0

    for i in range(N): 
        prefixSum += arr[i] 

        # If a subarray with sum K 
        # is already found 
        if((prefixSum - K) in st): 

            # Increase count 
            res += 1

            # Reset prefix sum 
            prefixSum = 0

            # Clear the set 
            st.clear() 
            st.add(0) 

        # Insert the prefix sum 
        st.add(prefixSum) 

    return res 

# Driver Code 
arr = [ -2, 6, 6, 3, 5, 4, 1, 2, 8 ] 
N = len(arr) 
K = 10

# Function call 
print(CtSubarr(arr, N, K)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to count the maximum 
// number of subarrays with sum K 
static int CtSubarr(int[] arr,  
                    int N, int K) 
{ 

    // Stores all the distinct 
    // prefixSums obtained 
    HashSet<int> st = new HashSet<int>(); 

    // Stores the prefix sum 
    // of the current subarray 
    int prefixSum = 0; 

    st.Add(prefixSum); 

    // Stores the count of 
    // subarrays with sum K 
    int res = 0; 

    for(int i = 0; i < N; i++)  
    { 
        prefixSum += arr[i]; 

        // If a subarray with sum K 
        // is already found 
        if (st.Contains(prefixSum - K))  
        { 

            // Increase count 
            res += 1; 

            // Reset prefix sum 
            prefixSum = 0; 

            // Clear the set 
            st.Clear(); 
            st.Add(0); 
        } 

        // Insert the prefix sum 
        st.Add(prefixSum); 
    } 
    return res; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []arr = { -2, 6, 6, 3,  
                   5, 4, 1, 2, 8}; 
    int N = arr.Length; 
    int K = 10; 

    Console.WriteLine(CtSubarr(arr, N, K)); 
} 
} 

// This code is contributed by 29AjayKumar

```

**输出**： 

```
3

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



