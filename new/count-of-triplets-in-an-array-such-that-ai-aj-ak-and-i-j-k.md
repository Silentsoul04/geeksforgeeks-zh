# 数组中三元组的计数，使得 A [i] * A [j] = A [k]且 i < j < k

> 原文：[https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/)

给定由 **N** 个正整数组成的数组 **A []** ，任务是查找三元组 **A [i]，A [j] & A [ k]** 在数组中，这样 **i < j < k** 和 **A [i] * A [j] = A [k]** 。

**示例**：

> **输入**：N = 5，A [] = {2，3，4，6，12}
> **输出**：3
> **说明**：
> 来自给定数组的有效三元组为：
> （A [0]，A [1]，A [3]）=（2、3、6）其中（2 * 3 = 6）
> （A [0]，A [3]，A [4]）=（2，6，12）其中（2 * 6 = 12）
> （A [1]，A [2]，A [4] ）=（3，4，12）其中（3 * 4 = 12）
> 因此，总共存在 3 个满足给定条件的三元组。
> **输入**：N = 3，A [] = {1，1，1}
> **输出**：1
> **说明**：HTG22]唯一有效的三元组是（A [0]，A [1]，A [2]）=（1、1、1）。

**天真的方法**：

解决该问题的最简单方法是生成所有可能的三元组，并为每个三元组检查是否满足所需条件。 如果发现是真的，则增加三胞胎的**计数**。 在完成数组遍历并生成所有可能的三元组之后，打印最终的**计数**。

***时间复杂度**：O（N <sup>3</sup> ）*

***辅助空间**：O（1）*

**有效方法**：

可以使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)和 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 优化上述方法。

请按照以下步骤解决问题：

*   初始化[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以存储阵列元素的频率。

*   反向迭代数组，即使用 **[N – 2、1]** 范围内的变量 **j** 循环。

*   对于每个 **j** ，增加图中的 **A [j + 1]** 的数量。 使用变量 **i** 迭代 **[0，j – 1]** 范围，并检查**中是否存在 **A [i] * A [j]** ]是否映射**。

*   如果在地图中找到 **A [i] * A [j]** ，则按照地图中存储的 **A [i] * A [j]** 的频率增加三元组的数量 。

*   遍历数组后，打印最终的**计数**。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Returns total number of
// valid triplets possible
int countTriplets(int A[], int N)
{
    // Stores the count
    int ans = 0;

    // Map to store frequency
    // of array elements
    map<int, int> map;

    for (int j = N - 2; j >= 1; j--) {

        // Increment the frequency
        // of A[j+1] as it can be
        // a valid A[k]
        map[A[j + 1]]++;

        for (int i = 0; i < j; i++) {

            int target = A[i] * A[j];

            // If target exists in the map
            if (map.find(target)
                != map.end())
                ans += map[target];
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
int main()
{
    int N = 5;
    int A[] = { 2, 3, 4, 6, 12 };

    cout << countTriplets(A, N);

    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Returns total number of
// valid triplets possible
static int countTriplets(int A[], int N)
{

    // Stores the count
    int ans = 0;

    // Map to store frequency
    // of array elements
    HashMap<Integer,
            Integer> map = new HashMap<Integer,
                                       Integer>();

    for(int j = N - 2; j >= 1; j--) 
    {

        // Increment the frequency
        // of A[j+1] as it can be
        // a valid A[k]
        if(map.containsKey(A[j + 1]))
            map.put(A[j + 1], map.get(A[j + 1]) + 1);
        else
            map.put(A[j + 1], 1);

        for(int i = 0; i < j; i++) 
        {
            int target = A[i] * A[j];

            // If target exists in the map
            if (map.containsKey(target))
                ans += map.get(target);
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int A[] = { 2, 3, 4, 6, 12 };

    System.out.print(countTriplets(A, N));
}
}

// This code is contributed by sapnasingh4991

```

## Python3

```py

# Python3 program for the above approach

> 原文：[https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/)
from collections import defaultdict

# Returns total number of

> 原文：[https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/)
# valid triplets possible

> 原文：[https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/)
def countTriplets(A, N):

    # Stores the count
    ans = 0

    # Map to store frequency
    # of array elements
    map = defaultdict(lambda: 0)

    for j in range(N - 2, 0, -1):

        # Increment the frequency
        # of A[j+1] as it can be
        # a valid A[k]
        map[A[j + 1]] += 1

        for i in range(j):
            target = A[i] * A[j]

            # If target exists in the map
            if(target in map.keys()):
                ans += map[target]

    # Return the final count 
    return ans

# Driver code

> 原文：[https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/)
if __name__ == '__main__':

    N = 5
    A = [ 2, 3, 4, 6, 12 ]

    print(countTriplets(A, N))

# This code is contributed by Shivam Singh

> 原文：[https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-such-that-ai-aj-ak-and-i-j-k/)

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Returns total number of
// valid triplets possible
static int countTriplets(int []A, int N)
{

    // Stores the count
    int ans = 0;

    // Map to store frequency
    // of array elements
    Dictionary<int,
               int> map = new Dictionary<int,
                                         int>();

    for(int j = N - 2; j >= 1; j--) 
    {

        // Increment the frequency
        // of A[j+1] as it can be
        // a valid A[k]
        if(map.ContainsKey(A[j + 1]))
            map[A[j + 1]] = map[A[j + 1]] + 1;
        else
            map.Add(A[j + 1], 1);

        for(int i = 0; i < j; i++) 
        {
            int target = A[i] * A[j];

            // If target exists in the map
            if (map.ContainsKey(target))
                ans += map[target];
        }
    }

    // Return the readonly count
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;
    int []A = { 2, 3, 4, 6, 12 };

    Console.Write(countTriplets(A, N));
}
}

// This code is contributed by sapnasingh4991

```

**Output:**

```
3

```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N）*



* * *

* * *


