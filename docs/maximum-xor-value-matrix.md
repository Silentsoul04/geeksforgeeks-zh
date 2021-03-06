# 矩阵中的最大 XOR 值

> 原文： [https://www.geeksforgeeks.org/maximum-xor-value-matrix/](https://www.geeksforgeeks.org/maximum-xor-value-matrix/)

给定一个方阵（`N X N`），任务是查找完整行或完整列的最大 XOR 值。

**示例**：

```
Input :  N = 3 
        mat[3][3] = {{1, 0, 4},
                    {3, 7, 2},
                    {5, 9, 10} };
Output : 14
We get this maximum XOR value by doing XOR 
of elements in second column 0 ^ 7 ^ 9 = 14

Input : N = 4 
        mat[4][4] = { {1, 2, 3, 6},
                      {4, 5, 6,7},
                      {7, 8, 9, 10},
                      {2, 4, 5, 11}}
Output : 12 

```



这个问题的**简单解决方案**是我们可以遍历矩阵两次并逐行计算最大 xor 值和列，最后返回`(xor_row, xor_column)`之间的最大值。

**有效解决方案**是我们只能遍历矩阵一次并计算最大 XOR 值。

1.  开始遍历矩阵，并在每个索引行和列方向上计算 XOR。 我们可以通过反向使用索引来计算两个值。 这是可能的，因为矩阵是一个正方形矩阵。

2.  存储两者的最大值。

下面是实现：

## C++ 

```cpp

// C++ program to Find maximum XOR value in 
// matrix either row / column wise 
#include<iostream> 
using namespace std; 

// maximum number of row and column 
const int MAX = 1000; 

// function return the maximum xor value that is 
// either row or column wise 
int maxXOR(int mat[][MAX], int N) 
{ 
    // for row xor and column xor 
    int r_xor, c_xor; 
    int max_xor = 0; 

    // traverse matrix 
    for (int i = 0 ; i < N ; i++) 
    { 
        r_xor = 0, c_xor = 0; 
        for (int j = 0 ; j < N ; j++) 
        { 
            // xor row element 
            r_xor = r_xor^mat[i][j]; 

            // for each column : j is act as row & i 
            // act as column xor column element 
            c_xor = c_xor^mat[j][i]; 
        } 

        // update maximum between r_xor , c_xor 
        if (max_xor < max(r_xor, c_xor)) 
            max_xor = max(r_xor, c_xor); 
    } 

    // return maximum xor value 
    return max_xor; 
} 

// driver Code 
int main() 
{ 
    int N = 3; 

    int mat[][MAX] = {{1 , 5, 4}, 
                      {3 , 7, 2 }, 
                      {5 , 9, 10} 
    }; 

    cout << "maximum XOR value : "
         << maxXOR(mat, N); 
    return 0; 
} 

```

## Java

```java
// Java program to Find maximum XOR value in 
// matrix either row / column wise 
class GFG { 
      
    // maximum number of row and column 
    static final int MAX = 1000; 
      
    // function return the maximum xor value  
    // that is either row or column wise 
    static int maxXOR(int mat[][], int N) 
    { 
          
        // for row xor and column xor 
        int r_xor, c_xor; 
        int max_xor = 0; 
      
        // traverse matrix 
        for (int i = 0 ; i < N ; i++) 
        { 
            r_xor = 0; c_xor = 0; 
              
            for (int j = 0 ; j < N ; j++) 
            { 
                  
                // xor row element 
                r_xor = r_xor^mat[i][j]; 
      
                // for each column : j is act as row & i 
                // act as column xor column element 
                c_xor = c_xor^mat[j][i]; 
            } 
      
            // update maximum between r_xor , c_xor 
            if (max_xor < Math.max(r_xor, c_xor)) 
                max_xor = Math.max(r_xor, c_xor); 
        } 
      
        // return maximum xor value 
        return max_xor; 
    } 
      
    //driver code 
    public static void main (String[] args) 
    { 
          
        int N = 3; 
      
        int mat[][] = { {1, 5, 4}, 
                        {3, 7, 2}, 
                        {5, 9, 10}}; 
      
        System.out.print("maximum XOR value : "
            + maxXOR(mat, N)); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python3 program to Find maximum 
# XOR value in matrix either row / column wise 
  
# maximum number of row and column 
MAX = 1000
   
# Function return the maximum 
# xor value that is either row 
# or column wise 
def maxXOR(mat, N): 
  
    # For row xor and column xor 
    max_xor = 0
   
    # Traverse matrix 
    for i in range(N): 
      
        r_xor = 0
        c_xor = 0
        for j in range(N): 
          
            # xor row element 
            r_xor = r_xor ^ mat[i][j] 
   
            # for each column : j is act as row & i 
            # act as column xor column element 
            c_xor = c_xor ^ mat[j][i] 
          
   
        # update maximum between r_xor , c_xor 
        if (max_xor < max(r_xor, c_xor)): 
            max_xor =  max(r_xor, c_xor) 
   
    # return maximum xor value 
    return max_xor 
   
# Driver Code 
N = 3
   
mat= [[1 , 5, 4], 
      [3 , 7, 2 ], 
      [5 , 9, 10]] 
   
print("maximum XOR value : ", 
              maxXOR(mat, N)) 
                
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// C# program to Find maximum XOR value in 
// matrix either row / column wise 
using System; 
  
class GFG  
{ 
      
    // maximum number of row and column 
  
      
    // function return the maximum xor value  
    // that is either row or column wise 
    static int maxXOR(int [,]mat, int N) 
    { 
          
        // for row xor and column xor 
        int r_xor, c_xor; 
        int max_xor = 0; 
      
        // traverse matrix 
        for (int i = 0 ; i < N ; i++) 
        { 
            r_xor = 0; c_xor = 0; 
              
            for (int j = 0 ; j < N ; j++) 
            { 
                  
                // xor row element 
                r_xor = r_xor^mat[i, j]; 
      
                // for each column : j is act as row & i 
                // act as column xor column element 
                c_xor = c_xor^mat[j, i]; 
            } 
      
            // update maximum between r_xor , c_xor 
            if (max_xor < Math.Max(r_xor, c_xor)) 
                max_xor = Math.Max(r_xor, c_xor); 
        } 
      
        // return maximum xor value 
        return max_xor; 
    } 
      
    // Driver code 
    public static void Main () 
    { 
          
        int N = 3; 
      
        int [,]mat = { {1, 5, 4}, 
                        {3, 7, 2}, 
                        {5, 9, 10}}; 
      
        Console.Write("maximum XOR value : "
            + maxXOR(mat, N)); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// PHP program to Find  
// maximum XOR value in 
// matrix either row or  
// column wise 
  
// maximum number of  
// row and column 
$MAX = 1000; 
  
// function return the maximum  
// xor value that is either 
// row or column wise 
function maxXOR($mat, $N) 
{ 
      
    // for row xor and  
    // column xor 
    $r_xor; $c_xor; 
    $max_xor = 0; 
  
    // traverse matrix 
    for ($i = 0 ; $i < $N ; $i++) 
    { 
        $r_xor = 0; $c_xor = 0; 
        for ($j = 0 ; $j < $N ; $j++) 
        { 
              
            // xor row element 
            $r_xor = $r_xor^$mat[$i][$j]; 
  
            // for each column : j 
            // is act as row & i 
            // act as column xor 
            // column element 
            $c_xor = $c_xor^$mat[$j][$i]; 
        } 
  
        // update maximum between 
        // r_xor , c_xor 
        if ($max_xor < max($r_xor, $c_xor)) 
            $max_xor = max($r_xor, $c_xor); 
    } 
  
    // return maximum  
    // xor value 
    return $max_xor; 
} 
  
    // Driver Code 
    $N = 3; 
    $mat = array(array(1, 5, 4), 
                 array(3, 7, 2), 
                 array(5, 9, 10)); 
  
    echo "maximum XOR value : "
        , maxXOR($mat, $N); 
  
// This code is contributed by anuj_67. 
?>
```

时间复杂度：`O(N * N)`。

空间复杂度：`O(1)`。