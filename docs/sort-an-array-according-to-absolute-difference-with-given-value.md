# 根据给定值的绝对差对数组进行排序

> 原文： [https://www.geeksforgeeks.org/sort-an-array-according-to-absolute-difference-with-given-value/](https://www.geeksforgeeks.org/sort-an-array-according-to-absolute-difference-with-given-value/)

给定一个由`n`个不同元素组成的数组和一个数字`x`，请根据与`x`，`i`的绝对差来排列数组元素。 例如，具有最小差异的元素排在第一位，依此类推。

注意：如果两个或多个元素的距离相等，则按照与给定数组相同的顺序排列它们。

例子 ：

```
Input : arr[] : x = 7, arr[] = {10, 5, 3, 9, 2}
Output : arr[] = {5, 9, 10, 3, 2}
Explanation:
7 - 10 = 3(abs)
7 - 5 = 2
7 - 3 = 4 
7 - 9 = 2(abs)
7 - 2 = 5
So according to the difference with X, 
elements are arranged as 5, 9, 10, 3, 2.

Input : x = 6, arr[] = {1, 2, 3, 4, 5}   
Output :  arr[] = {5, 4, 3, 2, 1}

Input : x = 5, arr[] = {2, 6, 8, 3}   
Output :  arr[] = {6, 3, 2, 8}

```



想法是使用自平衡二分搜索树。 我们遍历输入数组，对于每个元素，我们找到它与`x`的差异，并将差异作为键存储，并将元素存储为自平衡二叉搜索树中的值。 最后，我们遍历树并打印其顺序遍历，这是必需的输出。

**C++ 实现**：

在 C++ 中，通过[集合](http://quiz.geeksforgeeks.org/set-associative-containers-the-c-standard-template-library-stl/)，[映射](http://quiz.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和[多重映射](http://quiz.geeksforgeeks.org/multimap-associative-containers-the-c-standard-template-library-stl/)实现自平衡二叉搜索树。 我们拥有键值对（不仅是键），因此无法在这里使用集合。 我们也不能直接使用映射，因为单个键可以属于多个值，而映射则允许键具有单个值。 因此，我们使用多图存储键值对，并且键可以有多个值。

1.  以`x`为键，以差异为值，将其存储在多图中。

2.  在多重映射中，值已经根据键进行排序，即与`x`的差异，因为它在内部实现了自平衡二叉树。

3.  用映射的值更新数组的所有值，以便该数组具有所需的输出。

## C++ 

```cpp

// C++ program to sort an array according absolute 
// difference with x. 
#include<bits/stdc++.h> 
using namespace std; 

// Function to sort an array according absolute 
// difference with x. 
void rearrange(int arr[], int n, int x) 
{ 
    multimap<int, int> m; 
    multimap<int ,int >:: iterator it; 
    // Store values in a map with the difference 
    // with X as key 
    for (int i = 0 ; i < n; i++) 
        m.insert(make_pair(abs(x-arr[i]),arr[i])); 

    // Update the values of array 
    int i = 0; 
    for (it = m.begin(); it != m.end(); it++) 
        arr[i++] = (*it).second ; 
} 

// Function to print the array 
void printArray(int arr[] , int n) 
{ 
    for (int i = 0 ; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {10, 5, 3, 9 ,2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 7; 
    rearrange(arr, n, x); 
    printArray(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to sort an array according absolute  
// difference with x.  
import java.io.*; 
import java.util.*; 

class GFG  
{ 

    // Function to sort an array according absolute  
    // difference with x. 
    static void rearrange(int[] arr, int n, int x) 
    { 
            TreeMap<Integer, ArrayList<Integer>> m = new TreeMap<>(); 

            // Store values in a map with the difference  
            // with X as key 
            for (int i = 0; i < n; i++) 
            { 
                int diff = Math.abs(x - arr[i]); 
                if (m.containsKey(diff))  
                { 
                    ArrayList<Integer> al = m.get(diff); 
                    al.add(arr[i]); 
                    m.put(diff, al); 
                } 
                else 
                { 
                        ArrayList<Integer> al = new ArrayList<>(); 
                        al.add(arr[i]); 
                        m.put(diff,al); 
                } 
            } 

            // Update the values of array 
            int index = 0; 
            for (Map.Entry entry : m.entrySet())  
            { 
                ArrayList<Integer> al = m.get(entry.getKey()); 
                for (int i = 0; i < al.size(); i++) 
                        arr[index++] = al.get(i);  
            } 
    } 

    // Function to print the array 
    static void printArray(int[] arr, int n) 
    { 
            for (int i = 0; i < n; i++) 
                System.out.print(arr[i] + " "); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
            int[] arr = {10, 5, 3, 9 ,2}; 
            int n = arr.length; 
            int x = 7; 
            rearrange(arr, n, x);  
            printArray(arr, n);  
    } 
} 

// This code is contributed by rachana soma 

```

**输出**：

```
5 9 10 3 2

```

**时间复杂度**：`O(N log N)`。

**辅助空间**：`O(n)`。



