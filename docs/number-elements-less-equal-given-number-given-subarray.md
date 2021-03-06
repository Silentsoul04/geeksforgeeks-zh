# 给定子数组中小于或等于给定数字的元素数

> 原文： [https://www.geeksforgeeks.org/number-elements-less-equal-given-number-given-subarray/](https://www.geeksforgeeks.org/number-elements-less-equal-given-number-given-subarray/)

给定数组`a[]`和查询数量`q`。 每个查询都可以用`l, r, x`表示。 您的任务是在`l`到`r`表示的子数组中打印小于或等于`x`的元素数。

例子：

```
Input : arr[] = {2, 3, 4, 5}
            q = 2
            0 3 5
            0 2 2 
Output : 4
         1
Number of elements less than or equal to
5 in arr[0..3] is 4 (all elements)

Number of elements less than or equal to
2 in arr[0..2] is 1 (only 2)

```



**朴素方法**每个查询的朴素方法遍历子数组并计算给定范围内的元素数。

**有效方法**的想法是使用[二叉索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)。

请注意，在以下步骤中，`x`是必须根据其查找元素的数字，并且子数组由`l`，`r`表示。

步骤 1：按升序对数组进行排序。

步骤 2：根据`x`对查询升序排序，将位数组初始化为 0。

步骤 3：从第一个查询开始，遍历数组，直到数组中的值小于等于`x`。 对于每个这样的元素，将位更新为等于 1 的值。

步骤 4：查询范围为`l`至`r`的位数组。

```

// C++ program to answer queries to count number 
// of elements smaller tban or equal to x. 
#include<bits/stdc++.h> 
using namespace std; 

// structure to hold queries 
struct Query 
{ 
    int l, r, x, idx; 
}; 

// structure to hold array 
struct ArrayElement 
{ 
    int val, idx; 
}; 

// bool function to sort queries according to k 
bool cmp1(Query q1, Query q2) 
{ 
    return q1.x < q2.x; 
} 

// bool function to sort array according to its value 
bool cmp2(ArrayElement x, ArrayElement y) 
{ 
    return x.val < y.val; 
} 

// updating the bit array 
void update(int bit[], int idx, int val, int n) 
{ 
    for (; idx<=n; idx +=idx&-idx) 
        bit[idx] += val; 
} 

// querying the bit array 
int query(int bit[], int idx, int n) 
{ 
    int sum = 0; 
    for (; idx > 0; idx -= idx&-idx) 
        sum += bit[idx]; 
    return sum; 
} 

void answerQueries(int n, Query queries[], int q, 
                              ArrayElement arr[]) 
{ 
    // initialising bit array 
    int bit[n+1]; 
    memset(bit, 0, sizeof(bit)); 

    // sorting the array 
    sort(arr, arr+n, cmp2); 

    // sorting queries 
    sort(queries, queries+q, cmp1); 

    // current index of array 
    int curr = 0; 

    // array to hold answer of each Query 
    int ans[q]; 

    // looping through each Query 
    for (int i=0; i<q; i++) 
    { 
        // traversing the array values till it 
        // is less than equal to Query number 
        while (arr[curr].val <= queries[i].x && curr<n) 
        { 
            // updating the bit array for the array index 
            update(bit, arr[curr].idx+1, 1, n); 
            curr++; 
        } 

        // Answer for each Query will be number of 
        // values less than equal to x upto r minus 
        // number of values less than equal to x 
        // upto l-1 
        ans[queries[i].idx] = query(bit, queries[i].r+1, n) - 
                              query(bit, queries[i].l, n); 
    } 

    // printing answer for each Query 
    for (int i=0 ; i<q; i++) 
        cout << ans[i] << endl; 
} 

// driver function 
int main() 
{ 
    // size of array 
    int n = 4; 

    // initialising array value and index 
    ArrayElement arr[n]; 
    arr[0].val = 2; 
    arr[0].idx = 0; 
    arr[1].val = 3; 
    arr[1].idx = 1; 
    arr[2].val = 4; 
    arr[2].idx = 2; 
    arr[3].val = 5; 
    arr[3].idx = 3; 

    // number of queries 
    int q = 2; 
    Query queries[q]; 
    queries[0].l = 0; 
    queries[0].r = 2; 
    queries[0].x = 2; 
    queries[0].idx = 0; 
    queries[1].l = 0; 
    queries[1].r = 3; 
    queries[1].x = 5; 
    queries[1].idx = 1; 

    answerQueries(n, queries, q, arr); 

    return 0; 
} 

```

输出：

```
1
4

```

