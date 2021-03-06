# 打印数组`A[]`中的所有字符串，数组`B[]`中的所有字符串都是它的子序列

> 原文：[https://www.geeksforgeeks.org/print-all-strings-from-array-a-having-all-strings-from-array-b-as-subsequence/](https://www.geeksforgeeks.org/print-all-strings-from-array-a-having-all-strings-from-array-b-as-subsequence/)

给定两个由字符串组成的数组`A[]`和`B[]`，任务是从数组`A[]`中打印所有字符串都位于`B[]`作为子序列。

**示例**：

> **输入**：`A[] = {"geeksforgeeks", "mapple", "twitter", "table", "Linkedin"}, B [] = {"e", "l"}`
>
> **输出**：`maplet tablelinkedin`
>
> **说明**：字符串`e`和`l`都是`"mapple"`，`"table"`，`"linkedin"`中的子集。
> 
> **输入**：`A[] = {"geeksforgeeks", "topcoder", "leetcode"}, B [] = {"geek", "ee"}`
>
> **输出**：`geeksforgeeks`
>
> **说明**：`B[] = {"geek", "ee"}`中的每个字符串仅出现在`"geeksforgeeks"`。

**朴素的方法**：

解决该问题的最简单方法是遍历数组`A[]`，对于每个字符串，检查数组`B[]`中的所有字符串是否[都以子序列的形式存在](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)。

**时间复杂度**：`O(N ^ 2 * L)`，其中`length`表示数组`A[]`中字符串的最大长度

**辅助空间**：`O(1)`。

**有效方法**：

要优化上述方法，请按照以下步骤操作：

*   初始化矩阵`A_fre[][]`，其中`A_fre[i]`将存储第`i`个字符串中的每个字符的频率。

*   初始化`B_fre[]`，以将所有字符的频率存储在数组`B[]`中。

*   遍历数组`A[]`，对于每个字符串，检查数组`B[]`的字符串中的字符是否比`A[]`中的字符串`i`的频率更高。

    > 如果`A_fre[i][j] < B_fre[j]`，其中：

    > `A_fre[i][j]`：`A[i]`中 ASCII 值为（`'a' + j`）的字符的频率。

    > `B_fre[i][j]`：`B[i]`中 ASCII 值为（`'a' + j`）的字符的频率。

    那么该字符串在`B[]`中至少有一个字符串，而不是其子序列。

*   如果`A[]`中的任何字符串的所有字符都不满足上述条件，请将该字符串打印为答案。

*   在检查了`A[]`中的所有字符串后，如果没有发现将`B[]`中的所有字符串作为其适当子集的字符串，请打印`-1`。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement the 
// above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find strings from A[] 
// having all strings in B[] as subsequence 
void UniversalSubset(vector<string> A, 
                     vector<string> B) 
{ 
    // Calculate respective sizes 
    int n1 = A.size(); 
    int n2 = B.size(); 

    // Stores the answer 
    vector<string> res; 

    // Stores the frequency of each 
    // character in strings of A[] 
    int A_fre[n1][26]; 

    for (int i = 0; i < n1; i++) { 
        for (int j = 0; j < 26; j++) 
            A_fre[i][j] = 0; 
    } 

    // Compute the frequencies 
    // of characters of all strings 
    for (int i = 0; i < n1; i++) { 
        for (int j = 0; j < A[i].size(); 
             j++) { 
            A_fre[i][A[i][j] - 'a']++; 
        } 
    } 

    // Stores the frequency of each 
    // character in strings of B[] 
    // each character of a string in B[] 
    int B_fre[26] = { 0 }; 

    for (int i = 0; i < n2; i++) { 
        int arr[26] = { 0 }; 
        for (int j = 0; j < B[i].size(); 
             j++) { 

            arr[B[i][j] - 'a']++; 
            B_fre[B[i][j] - 'a'] 
                = max(B_fre[B[i][j] - 'a'], 
                      arr[B[i][j] - 'a']); 
        } 
    } 

    for (int i = 0; i < n1; i++) { 
        int flag = 0; 
        for (int j = 0; j < 26; j++) { 

            // If the frequency of a character 
            // in B[] exceeds that in A[] 
            if (A_fre[i][j] < B_fre[j]) { 

                // A string exists in B[] which 
                // is not a proper subset of A[i] 
                flag = 1; 
                break; 
            } 
        } 

        // If all strings in B[] are 
        // proper subset of A[] 
        if (flag == 0) 
            // Push the string in 
            // resultant vector 
            res.push_back(A[i]); 
    } 

    // If any string is found 
    if (res.size()) { 

        // Print those strings 
        for (int i = 0; i < res.size(); 
             i++) { 
            for (int j = 0; j < res[i].size(); 
                 j++) 
                cout << res[i][j]; 
        } 

        cout << " "; 
    } 

    // Otherwise 
    else
        cout << "-1"; 
} 

// Driver code 
int main() 
{ 
    vector<string> A = { "geeksforgeeks", 
                         "topcoder", 
                         "leetcode" }; 
    vector<string> B = { "geek", "ee" }; 

    UniversalSubset(A, B); 

    return 0; 
} 

```

## Java

```java

// Java program to implement  
// the above approach  
import java.util.*; 

class GFG { 

// Function to find strings from A[]  
// having all strings in B[] as subsequence  
static void UniversalSubset(List<String> A,  
                            List<String> B)  
{  

    // Calculate respective sizes  
    int n1 = A.size();  
    int n2 = B.size();  

    // Stores the answer  
    List<String> res = new ArrayList<>();  

    // Stores the frequency of each  
    // character in strings of A[]  
    int[][] A_fre = new int[n1][26];  

    for(int i = 0; i < n1; i++) 
    {  
        for(int j = 0; j < 26; j++)  
            A_fre[i][j] = 0;  
    }  

    // Compute the frequencies  
    // of characters of all strings  
    for(int i = 0; i < n1; i++) 
    {  
        for(int j = 0; j < A.get(i).length(); j++)  
        {  
            A_fre[i][A.get(i).charAt(j) - 'a']++;  
        }  
    }  

    // Stores the frequency of each  
    // character in strings of B[]  
    // each character of a string in B[]  
    int[] B_fre = new int[26];  

    for(int i = 0; i < n2; i++) 
    {  
        int[] arr = new int[26] ;  
        for(int j = 0; j < B.get(i).length(); j++) 
        {  
            arr[B.get(i).charAt(j) - 'a']++;  
            B_fre[B.get(i).charAt(j) - 'a'] = Math.max( 
            B_fre[B.get(i).charAt(j) - 'a'],  
              arr[B.get(i).charAt(j) - 'a']);  
        }  
    }  

    for(int i = 0; i < n1; i++) 
    {  
        int flag = 0;  
        for(int j = 0; j < 26; j++)  
        {  

            // If the frequency of a character  
            // in B[] exceeds that in A[]  
            if (A_fre[i][j] < B_fre[j]) 
            {  

                // A string exists in B[] which  
                // is not a proper subset of A[i]  
                flag = 1;  
                break;  
            }  
        }  

        // If all strings in B[] are  
        // proper subset of A[]  
        if (flag == 0)  

            // Push the string in  
            // resultant vector  
            res.add(A.get(i));  
    }  

    // If any string is found  
    if (res.size() != 0) 
    {  

        // Print those strings  
        for(int i = 0; i < res.size(); i++)  
        {  
            for(int j = 0;  
                    j < res.get(i).length(); 
                    j++)  
            System.out.print(res.get(i).charAt(j));  
        }  
        System.out.print(" ");  
    }  

    // Otherwise  
    else
    System.out.print("-1");  
} 

// Driver code 
public static void main (String[] args)  
{ 
    List<String> A = Arrays.asList("geeksforgeeks",  
                                   "topcoder",  
                                   "leetcode");  
    List<String> B = Arrays.asList("geek", "ee");  

    UniversalSubset(A, B);  
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to find strings from A[] 
# having all strings in B[] as subsequence 
def UniversalSubset(A, B): 

    # Calculate respective sizes 
    n1 = len(A) 
    n2 = len(B) 

    # Stores the answer 
    res = [] 

    # Stores the frequency of each 
    # character in strings of A[] 
    A_freq = [[0 for x in range(26)] 
                 for y in range(n1)] 

    # Compute the frequencies 
    # of characters of all strings 
    for i in range(n1): 
        for j in range(len(A[i])): 
            A_freq[i][ord(A[i][j]) - ord('a')] += 1

    # Stores the frequency of each 
    # character in strings of B[] 
    # each character of a string in B[] 
    B_freq = [0] * 26

    for i in range(n2): 
        arr = [0] * 26

        for j in range(len(B[i])): 
            arr[ord(B[i][j]) - ord('a')] += 1

            B_freq[ord(B[i][j]) - ord('a')] = max( 
            B_freq[ord(B[i][j]) - ord('a')], 
               arr[ord(B[i][j]) - ord('a')]) 

    for i in range(n1): 
        flag = 0
        for j in range(26): 

            # If the frequency of a character 
            # in B[] exceeds that in A[] 
            if(A_freq[i][j] < B_freq[j]): 

                # A string exists in B[] which 
                # is not a proper subset of A[i] 
                flag = 1
                break

        # If all strings in B[] are 
        # proper subset of A[] 
        if(flag == 0): 

            # Push the string in 
            # resultant vector 
            res.append(A[i]) 

    # If any string is found 
    if(len(res)): 

        # Print those strings 
        for i in range(len(res)): 
            for j in range(len(res[i])): 
                print(res[i][j], end = "") 

    # Otherwise  
    else: 
        print(-1, end = "") 

# Driver code 
if __name__ == '__main__': 

    A = [ "geeksforgeeks", "topcoder",  
          "leetcode" ] 
    B = [ "geek", "ee" ] 

    UniversalSubset(A, B) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find strings from []A 
// having all strings in []B as subsequence 
static void UniversalSubset(List<String> A, 
                            List<String> B) 
{ 

    // Calculate respective sizes 
    int n1 = A.Count; 
    int n2 = B.Count; 

    // Stores the answer 
    List<String> res = new List<String>(); 

    // Stores the frequency of each 
    // character in strings of []A 
    int[,] A_fre = new int[n1, 26]; 

    for(int i = 0; i < n1; i++) 
    { 
        for(int j = 0; j < 26; j++) 
            A_fre[i, j] = 0; 
    } 

    // Compute the frequencies 
    // of characters of all strings 
    for(int i = 0; i < n1; i++) 
    { 
        for(int j = 0; j < A[i].Length; j++) 
        { 
            A_fre[i, A[i][j] - 'a']++; 
        } 
    } 

    // Stores the frequency of each 
    // character in strings of []B 
    // each character of a string in []B 
    int[] B_fre = new int[26]; 

    for(int i = 0; i < n2; i++) 
    { 
        int[] arr = new int[26]; 
        for(int j = 0; j < B[i].Length; j++) 
        { 
            arr[B[i][j] - 'a']++; 
            B_fre[B[i][j] - 'a'] = Math.Max( 
                                   B_fre[B[i][j] - 'a'], 
                                     arr[B[i][j] - 'a']); 
        } 
    } 

    for(int i = 0; i < n1; i++) 
    { 
        int flag = 0; 
        for(int j = 0; j < 26; j++)  
        { 

            // If the frequency of a character 
            // in []B exceeds that in []A 
            if (A_fre[i, j] < B_fre[j]) 
            { 

                // A string exists in []B which 
                // is not a proper subset of A[i] 
                flag = 1; 
                break; 
            } 
        } 

        // If all strings in []B are 
        // proper subset of []A 
        if (flag == 0) 

            // Push the string in 
            // resultant vector 
            res.Add(A[i]); 
    } 

    // If any string is found 
    if (res.Count != 0) 
    { 

        // Print those strings 
        for(int i = 0; i < res.Count; i++) 
        { 
            for(int j = 0; j < res[i].Length; j++) 
                Console.Write(res[i][j]); 
        } 
        Console.Write(" "); 
    } 

    // Otherwise 
    else
        Console.Write("-1"); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    List<String> A = new List<String>(); 
    A.Add("geeksforgeeks"); 
    A.Add("topcoder"); 
    A.Add("leetcode"); 

    List<String> B = new List<String>(); 
    B.Add("geek"); 
    B.Add("ee"); 

    UniversalSubset(A, B); 
} 
} 

// This code is contributed by amal kumar choubey

```

**输出**： 

```
geeksforgeeks

```

**时间复杂度**：`O(N * L)`，其中`length`表示数组`A[]`中字符串的最大长度。

**辅助空间**：`O(n)`。



* * *

* * *



