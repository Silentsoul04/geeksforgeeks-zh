# 乘积小于`k`的子集数

> 原文： [https://www.geeksforgeeks.org/number-subsets-product-less-k/](https://www.geeksforgeeks.org/number-subsets-product-less-k/)

给定`n`个元素的数组，您必须找到其元素乘积小于或等于给定整数`k`的子集数。

**示例**：

```
Input : arr[] = {2, 4, 5, 3}, k = 12
Output : 8
Explanation : All possible subsets whose 
products are less than 12 are:
(2), (4), (5), (3), (2, 4), (2, 5), (2, 3), (4, 3)

Input : arr[] = {12, 32, 21 }, k = 1
Output : 0
Explanation : there is not any subset such 
that product of elements is less than 1

```



**方法**：如果我们通过基本方法来解决此问题，则必须生成所有可能的`2^n`子集，然后对于每个子集，我们必须计算子集元素的乘积，并比较给定的乘积值。 但是这种方法的缺点是其时间复杂度太高，即`O(n * 2^n)`。 现在，我们可以看到它将是指数时间复杂性，在竞争性编码的情况下应避免这种情况。

**进阶方法**：我们将在中间使用 [MEET](https://www.geeksforgeeks.org/meet-in-the-middle/) 的概念。 通过使用这个概念，我们可以降低我们求解`O(n * 2^(n / 2))`的复杂性。

**如何在中间方法中使用 MEET**：首先，我们将给定数组简单地分为两个相等的部分，然后我们为数组的两个部分生成所有可能的子集，并为每个子集将元素乘积的值分别存储为两个向量（例如，`subset1 & subset2`）。 现在，这将花费`O(2^(n/2))`时间复杂度。 现在，如果我们对这两个向量（`subset1 & subset2`）进行排序，每个向量具有`2^(n/2)`个元素，那么这将花费`O(2^(n/2) * log2^(n/2) ≈ O(n * 2^(n/2))`时间复杂度。 在下一步中，我们遍历一个具有`2^(n/2)`个元素的向量`subset1`，并在第二个向量中找到`k / subset1[i]`的上限，这将告诉我们乘积小于或等于`k`。 因此，对于子集 1 中的每个元素，我们将尝试在子集 2 中以`upper_bound`的形式执行二分搜索，从而再次导致时间复杂度为`O(n * (2^(n/2)))`。 因此，如果我们尝试计算此方法的总体复杂度，则将有`O(n * 2^(n/2) + n  *2^(n/2) + n * 2^(n/2)) ≈ O(n * 2^(n/2))`作为我们的时间复杂度，这比暴力法效率高得多。

**算法**：

1.  将数组分为两个相等的部分。

2.  生成所有子集，并为每个子集计算元素的乘积并将其推入向量。 尝试数组的两个部分。

3.  对两个新向量进行排序，这些向量包含每个可能子集的元素乘积。

4.  遍历任何一个向量并找到元素`k / vector [i]`的上限，以找到元素乘积小于`k`的`vector[i]`有多少个子集。

**一些提高复杂性的关键点**：

*   如果大于`k`，则忽略数组中的元素。

*   如果大于`k`，则忽略元素乘积以推入向量（子集 1 或子集 2）。

## C++ 

```cpp

// CPP to find the count subset having product  
// less than k 
#include <bits/stdc++.h> 
using namespace std; 

int findSubset(long long int arr[], int n,  
                              long long int k) 
{ 
    // declare four vector for dividing array into  
    // two halves and storing product value of   
    // possible subsets for them 
    vector<long long int> vect1, vect2, subset1, subset2; 

    // ignore element greater than k and divide 
    // array into 2 halves 
    for (int i = 0; i < n; i++) { 

        // ignore element if greater than k 
        if (arr[i] > k) 
            continue; 
        if (i <= n / 2) 
            vect1.push_back(arr[i]); 
        else
            vect2.push_back(arr[i]); 
    } 

    // generate all subsets for 1st half (vect1) 
    for (int i = 0; i < (1 << vect1.size()); i++) { 
        long long value = 1; 
        for (int j = 0; j < vect1.size(); j++) { 
            if (i & (1 << j)) 
                value *= vect1[j]; 
        } 

        // push only in case subset product is less  
        // than equal to k 
        if (value <= k) 
            subset1.push_back(value); 
    } 

    // generate all subsets for 2nd half (vect2) 
    for (int i = 0; i < (1 << vect2.size()); i++) { 
        long long value = 1; 
        for (int j = 0; j < vect2.size(); j++) { 
            if (i & (1 << j)) 
                value *= vect2[j]; 
        } 

        // push only in case subset product is 
        // less than equal to k 
        if (value <= k) 
            subset2.push_back(value); 
    } 

    // sort subset2 
    sort(subset2.begin(), subset2.end()); 

    long long count = 0; 
    for (int i = 0; i < subset1.size(); i++) 
        count += upper_bound(subset2.begin(), subset2.end(),  
                         (k / subset1[i])) - subset2.begin(); 

    // for null subset decrement the value of count 
    count--; 

    // return count 
    return count; 
} 

// driver program 
int main() 
{ 
    long long int arr[] = { 4, 2, 3, 6, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    long long int k = 25; 
    cout << findSubset(arr, n, k); 
    return 0; 
} 

```

## Python3

```py

# Python3 to find the count subset  
# having product less than k  
import bisect 

def findSubset(arr, n, k):  

    # declare four vector for dividing  
    # array into two halves and storing  
    # product value of possible subsets 
    # for them  
    vect1, vect2, subset1, subset2 = [], [], [], []  

    # ignore element greater than k and  
    # divide array into 2 halves  
    for i in range(0, n):  

        # ignore element if greater than k  
        if arr[i] > k:  
            continue
        if i <= n // 2:  
            vect1.append(arr[i])  
        else: 
            vect2.append(arr[i])  

    # generate all subsets for 1st half (vect1)  
    for i in range(0, (1 << len(vect1))):  
        value = 1
        for j in range(0, len(vect1)):  
            if i & (1 << j):  
                value *= vect1[j]  

        # push only in case subset product  
        # is less than equal to k  
        if value <= k: 
            subset1.append(value)  

    # generate all subsets for 2nd half (vect2)  
    for i in range(0, (1 << len(vect2))):  
        value = 1
        for j in range(0, len(vect2)):  
            if i & (1 << j):  
                value *= vect2[j]  

        # push only in case subset product  
        # is less than equal to k  
        if value <= k: 
            subset2.append(value)  

    # sort subset2  
    subset2.sort()  

    count = 0
    for i in range(0, len(subset1)):  
        count += bisect.bisect(subset2, (k // subset1[i])) 

    # for null subset decrement the  
    # value of count  
    count -= 1

    # return count  
    return count  

# Driver Code 
if __name__ == "__main__":  

    arr = [4, 2, 3, 6, 5]  
    n = len(arr)  
    k = 25
    print(findSubset(arr, n, k))  

# This code is contributed by Rituraj Jain 

```

**输出**：

```
15

```



* * *

* * *



