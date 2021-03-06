# 给定布尔矩阵，找到`k`，使第`k`行中的所有元素均为 0，第`k`列为 1。

> 原文： [https://www.geeksforgeeks.org/find-k-such-that-all-elements-in-kth-row-are-0-and-kth-column-are-1-in-a-boolean-matrix/](https://www.geeksforgeeks.org/find-k-such-that-all-elements-in-kth-row-are-0-and-kth-column-are-1-in-a-boolean-matrix/)

给定一个平方布尔矩阵`mat[n][n]`，求`k`使得第`k`行的所有元素均为 0，第`k`列的所有元素均为 1。`mat[k][k]`的值可以是任意值（0 或 1）。 如果不存在这样的`k`，则返回 -1。

**示例**：

```
Input: bool mat[n][n] = { {1, 0, 0, 0},
                          {1, 1, 1, 0},
                          {1, 1, 0, 0},
                          {1, 1, 1, 0},
                        };
Output: 0
All elements in 0'th row are 0 and all elements in 
0'th column are 1\.  mat[0][0] is 1 (can be any value)

Input: bool mat[n][n] = {{0, 1, 1, 0, 1},
                         {0, 0, 0, 0, 0},
                         {1, 1, 1, 0, 0},
                         {1, 1, 1, 1, 0},
                         {1, 1, 1, 1, 1}};
Output: 1
All elements in 1'st row are 0 and all elements in 
1'st column are 1\.  mat[1][1] is 0 (can be any value)

Input: bool mat[n][n] = {{0, 1, 1, 0, 1},
                         {0, 0, 0, 0, 0},
                         {1, 1, 1, 0, 0},
                         {1, 0, 1, 1, 0},
                         {1, 1, 1, 1, 1}};
Output: -1
There is no k such that k'th row elements are 0 and
k'th column elements are 1.

```

预期时间复杂度为`O(n)`。

**我们强烈建议您最小化浏览器，然后自己尝试。**

一个**简单解决方案**是一一检查所有行。 如果我们发现行`i`使得该行的所有元素均为 0，但 `mat[i][i]`可能为 0 或 1，则我们检查`i`列中的所有值。 如果该列中的所有值均为 1，则返回`i`。 该解决方案的时间复杂度为`O(n^2)`。

有效的**解决方案**可以在`O(n)`时间内解决此问题。 该解决方案基于以下事实。

1.  最多可以有一个`k`可以作为答案（为什么？请注意，如果第`k`行除`mat[k][k]`之外全为 0，那么任何列都不能全部为 1）。

2.  如果我们从某个角（最好从右上角和左下角）遍历给定的矩阵，则可以根据以下规则快速丢弃完整的行或完整的列。

    1.  如果`mat[i][j]`为 0 且`i != j`，则列`j`不能为解。

    2.  如果`mat[i][j]`为 1 且`i != j`，则行`i`不能为解。

下面是基于上述观察的完整算法。

```
1) Start from top right corner, i.e., i = 0, j = n-1\.  
   Initialize result as -1.

2) Do following until we find the result or reach outside the matrix.

......a) If mat[i][j] is 0, then check all elements on left of j in current row. 
.........If all elements on left of j are also 0, then set result as i. Note 
.........that i may not be result, but if there is a result, then it must be i 
.........(Why? we reach mat[i][j] after discarding all rows above it and all 
.........columns on right of it)

.........If all left side elements of i'th row are not 0, them this row cannot 
.........be a solution, increment i.

......b) If mat[i][j] is 1, then check all elements below i in current column. 
.........If all elements below i are 1, then set result as j. Note that j may
......... not be result, but if there is a result, then it must be j 

.........If all elements of j'th column are not 1, them this column cannot be a
.........solution decrement j.

3) If result is -1, return it. 

4) Else check validity of result by checking all row and column
          elements of result
```

下面是基于以上思想的实现。

## C++ 

```cpp

// C++ program to find i such that all entries in i'th row are 0 
// and all entries in i't column are 1 
#include <iostream> 
using namespace std; 
#define n 5 

int find(bool arr[n][n]) 
{ 
    // Start from top-most rightmost corner 
    // (We could start from other corners also) 
    int i=0, j=n-1; 

    // Initialize result 
    int res = -1; 

    // Find the index (This loop runs at most 2n times, we either 
    // increment row number or decrement column number) 
    while (i<n && j>=0) 
    { 
        // If current element is 0, then this row may be a solution 
        if (arr[i][j] == 0) 
        { 
            // Check for all elements in this row 
            while (j >= 0 && (arr[i][j] == 0 || i == j)) 
                j--; 

            // If all values are 0, then store this row as result 
            if (j == -1) 
            { 
                res = i; 
                break; 
            } 

            // We reach here if we found a 1 in current row, so this 
            //  row cannot be a solution, increment row number 
            else i++; 
        } 
        else // If current element is 1 
        { 
            // Check for all elements in this column 
            while (i<n && (arr[i][j] == 1 || i == j)) 
                i++; 

            // If all elements are 1 
            if (i == n) 
            { 
                res = j; 
                break; 
            } 

            // We reach here if we found a 0 in current column, so this 
            // column cannot be a solution, increment column number 
            else j--; 
        } 
    } 

    // If we could not find result in above loop, then result doesn't exist 
    if (res == -1) 
       return res; 

    // Check if above computed res is valid 
    for (int i=0; i<n; i++) 
       if (res != i && arr[i][res] != 1) 
          return -1; 
    for (int j=0; j<n; j++) 
       if (res != j && arr[res][j] != 0) 
          return -1; 

    return res; 
} 

/* Driver program to test above functions */
int main() 
{ 
    bool mat[n][n] = {{0, 0, 1, 1, 0}, 
                      {0, 0, 0, 1, 0}, 
                      {1, 1, 1, 1, 0}, 
                      {0, 0, 0, 0, 0}, 
                      {1, 1, 1, 1, 1}}; 
    cout << find(mat); 

    return 0; 
} 

```

## Java

```java

// Java program to find i such that all entries in i'th row are 0 
// and all entries in i't column are 1 
class GFG { 

    static int n = 5; 

    static int find(boolean arr[][]) { 
        // Start from top-most rightmost corner 
        // (We could start from other corners also) 
        int i = 0, j = n - 1; 

        // Initialize result 
        int res = -1; 

        // Find the index (This loop runs at most 2n times, we either 
        // increment row number or decrement column number) 
        while (i < n && j >= 0) { 
            // If current element is false, then this row may be a solution 
            if (arr[i][j] == false) { 
                // Check for all elements in this row 
                while (j >= 0 && (arr[i][j] == false || i == j)) { 
                    j--; 
                } 

                // If all values are false, then store this row as result 
                if (j == -1) { 
                    res = i; 
                    break; 
                } // We reach here if we found a 1 in current row, so this 
                //  row cannot be a solution, increment row number 
                else { 
                    i++; 
                } 
            } else // If current element is 1 
            { 
                // Check for all elements in this column 
                while (i < n && (arr[i][j] == true || i == j)) { 
                    i++; 
                } 

                // If all elements are 1 
                if (i == n) { 
                    res = j; 
                    break; 
                } // We reach here if we found a 0 in current column, so this 
                // column cannot be a solution, increment column number 
                else { 
                    j--; 
                } 
            } 
        } 

        // If we could not find result in above loop, then result doesn't exist 
        if (res == -1) { 
            return res; 
        } 

        // Check if above computed res is valid 
        for (int k = 0; k < n; k++) { 
            if (res != k && arr[k][res] != true) { 
                return -1; 
            } 
        } 
        for (int l = 0; l < n; l++) { 
            if (res != l && arr[res][l] != false) { 
                return -1; 
            } 
        } 

        return res; 
    } 

    /* Driver program to test above functions */
    public static void main(String[] args) { 
        boolean mat[][] = {{false, false, true, true, false}, 
        {false, false, false, true, false}, 
        {true, true, true, true, false}, 
        {false, false, false, false, false}, 
        {true, true, true, true, true}}; 
        System.out.println(find(mat)); 
    } 
} 

/* This Java code is contributed by PrinciRaj1992*/

```

## Python

```py

''' Python program to find k such that all elements in k'th row  
    are 0 and k'th column are 1'''

def find(arr): 

    # store length of the array 
    n = len(arr) 

    # start from top right-most corner  
    i = 0
    j = n - 1

    # initialise result 
    res = -1

    # find the index (This loop runs at most 2n times, we  
    # either increment row number or decrement column number) 
    while i < n and j >= 0: 

        # if the current element is 0, then this row may be a solution 
        if arr[i][j] == 0: 

            # check for all the elements in this row 
            while j >= 0 and (arr[i][j] == 0 or i == j): 
                j -= 1

            # if all values are 0, update result as row number     
            if j == -1: 
                res = i 
                break

            # if found a 1 in current row, the row can't be a  
            # solution, increment row number 
            else: i += 1

        # if the current element is 1 
        else: 

            #check for all the elements in this column 
            while i < n and (arr[i][j] == 1 or i == j): 
                i +=1

            # if all elements are 1, update result as col number 
            if i == n: 
                res = j 
                break

            # if found a 0 in current column, the column can't be a 
            # solution, decrement column number 
            else: j -= 1

    # if we couldn't find result in above loop, result doesn't exist 
    if res == -1: 
        return res 

    # check if the above computed res value is valid 
    for i in range(0, n): 
        if res != i and arr[i][res] != 1: 
            return -1
    for j in range(0, j): 
        if res != j and arr[res][j] != 0: 
            return -1; 

    return res; 

# test find(arr) function 
arr = [ [0,0,1,1,0], 
         [0,0,0,1,0], 
         [1,1,1,1,0], 
         [0,0,0,0,0], 
         [1,1,1,1,1] ] 

print find(arr) 

```

## C# 

```cs

// C# program to find i such that all entries in i'th row are 0  
// and all entries in i't column are 1  

using System; 
public class GFG{ 

    static int n = 5;  

    static int find(bool [,]arr) {  
        // Start from top-most rightmost corner  
        // (We could start from other corners also)  
        int i = 0, j = n - 1;  

        // Initialize result  
        int res = -1;  

        // Find the index (This loop runs at most 2n times, we either  
        // increment row number or decrement column number)  
        while (i < n && j >= 0) {  
            // If current element is false, then this row may be a solution  
            if (arr[i,j] == false) {  
                // Check for all elements in this row  
                while (j >= 0 && (arr[i,j] == false || i == j)) {  
                    j--;  
                }  

                // If all values are false, then store this row as result  
                if (j == -1) {  
                    res = i;  
                    break;  
                } // We reach here if we found a 1 in current row, so this  
                // row cannot be a solution, increment row number  
                else {  
                    i++;  
                }  
            } else // If current element is 1  
            {  
                // Check for all elements in this column  
                while (i < n && (arr[i,j] == true || i == j)) {  
                    i++;  
                }  

                // If all elements are 1  
                if (i == n) {  
                    res = j;  
                    break;  
                } // We reach here if we found a 0 in current column, so this  
                // column cannot be a solution, increment column number  
                else {  
                    j--;  
                }  
            }  
        }  

        // If we could not find result in above loop, then result doesn't exist  
        if (res == -1) {  
            return res;  
        }  

        // Check if above computed res is valid  
        for (int k = 0; k < n; k++) {  
            if (res != k && arr[k,res] != true) {  
                return -1;  
            }  
        }  
        for (int l = 0; l < n; l++) {  
            if (res != l && arr[res,l] != false) {  
                return -1;  
            }  
        }  

        return res;  
    }  

    /* Driver program to test above functions */
    public static void Main() {  
        bool [,]mat = {{false, false, true, true, false},  
        {false, false, false, true, false},  
        {true, true, true, true, false},  
        {false, false, false, false, false},  
        {true, true, true, true, true}};  
        Console.WriteLine(find(mat));  
    }  
}  

// This code is contributed by PrinciRaj1992  

```

## PHP

```php

<?php 
// PHP program to find i such that all 
// entries in i'th row are 0 and all 
// entries in i'th column are 1 

function find(&$arr) 
{ 
    $n = 5; 

    // Start from top-most rightmost corner 
    // (We could start from other corners also) 
    $i = 0; 
    $j = $n - 1; 

    // Initialize result 
    $res = -1; 

    // Find the index (This loop runs at most 
    // 2n times, we either increment row number 
    // or decrement column number) 
    while ($i < $n && $j >= 0) 
    { 
        // If current element is 0, then this  
        // row may be a solution 
        if ($arr[$i][$j] == 0) 
        { 
            // Check for all elements in this row 
            while ($j >= 0 && ($arr[$i][$j] == 0 ||  
                                        $i == $j)) 
                $j--; 

            // If all values are 0, then store 
            // this row as result 
            if ($j == -1) 
            { 
                $res = $i; 
                break; 
            } 

            // We reach here if we found a 1 in current  
            // row, so this row cannot be a solution, 
            // increment row number 
            else
            $i++; 
        } 
        else // If current element is 1 
        { 
            // Check for all elements in this column 
            while ($i < $n && ($arr[$i][$j] == 1 ||  
                                        $i == $j)) 
                $i++; 

            // If all elements are 1 
            if ($i == $n) 
            { 
                $res = $j; 
                break; 
            } 

            // We reach here if we found a 0 in current 
            // column, so this column cannot be a solution, 
            // increment column number 
            else
            $j--; 
        } 
    } 

    // If we could not find result in above  
    // loop, then result doesn't exist 
    if ($res == -1) 
    return $res; 

    // Check if above computed res is valid 
    for ($i = 0; $i < $n; $i++) 
    if ($res != $i && $arr[$i][$res] != 1) 
        return -1; 
    for ($j = 0; $j < $n; $j++) 
    if ($res != $j && $arr[$res][$j] != 0) 
        return -1; 

    return $res; 
} 

// Driver Code 
$mat = array(array(0, 0, 1, 1, 0), 
             array(0, 0, 0, 1, 0), 
             array(1, 1, 1, 1, 0), 
             array(0, 0, 0, 0, 0), 
             array(1, 1, 1, 1, 1)); 
echo (find($mat)); 

// This code is contributed by Shivi_Aggarwal 
?> 

```

**输出**：

```
3
```

该解决方案的时间复杂度为`O(n)`。 请注意，我们在主`while`循环中遍历最多`2n`个元素。

