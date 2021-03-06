# 给定字符串中第`K`个最常见的字符

> 原文：[https://www.geeksforgeeks.org/kth-most-frequent-character-in-a-given-string/](https://www.geeksforgeeks.org/kth-most-frequent-character-in-a-given-string/)

给定字符串`str`和整数`K`，任务是找到字符串中第`K`个最频繁出现的字符。 如果有多个字符可以解释为第`K`个最常见的字符，则打印其中的任何一个。

**示例**：

> **输入**：`str = "GeeksforGeeks", K = 3`
>
> **输出**：`f`
>
> **说明**：
>
> `K = 3`，此处`e`出现 4 次。
>
> `'g', 'k', 's'`出现 2 次。
>
> `'o', 'f', 'r'`出现 1 次。
>
> 来自`o`（或）`f`（或`r`）的任何输出都是正确的。
> 
> **输入**：`str = "trichotillomania", K = 2`
>
> **输出**：`l`

**方法**

*   这个想法是在[`Hashmap`](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)中使用字符作为键，并将它们的[出现](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/)存储在字符串中。

*   对[哈希映射](https://www.geeksforgeeks.org/sorting-hashmap-according-key-value-java/)排序并找到第`K`个字符。

下面是上述方法的实现。

## C++

```cpp

// C++ program to find kth most frequent 
// character in a string 
#include <bits/stdc++.h> 
using namespace std; 

// Used for sorting by frequency. 
bool sortByVal(const pair<char, int>& a, 
               const pair<char, int>& b) 
{ 
    return a.second > b.second; 
} 

// function to sort elements by frequency 
char sortByFreq(string str, int k) 
{ 
    // Store frequencies of characters 
    unordered_map<char, int> m; 
    for (int i = 0; i < str.length(); ++i) 
        m[str[i]]++; 

    // Copy map to vector 
    vector<pair<char, int> > v; 
    copy(m.begin(), m.end(), back_inserter(v)); 

    // Sort the element of array by frequency 
    sort(v.begin(), v.end(), sortByVal); 

    // Find k-th most frequent item. Please note 
    // that we need to consider only distinct 
    int count = 0; 
    for (int i = 0; i < v.size(); i++) { 

        // Increment count only if frequency is 
        // not same as previous 
        if (i == 0 || v[i].second != v[i - 1].second) 
            count++; 

        if (count == k) 
            return v[i].first; 
    } 

    return -1; 
} 

// Driver program 
int main() 
{ 
    string str = "geeksforgeeks"; 
    int k = 3; 
    cout << sortByFreq(str, k); 
    return 0; 
} 

```

**输出**：

```
r

```

**时间复杂度**：`O(NlogN)`请注意，这是时间复杂度的上限。 如果我们认为字母大小为常数（例如小写英文字母大小为 26），则可以说时间复杂度为`O(n)`。 向量大小永远不会超过字母大小。

**辅助空间**：`O(n)`。



* * *

* * *



