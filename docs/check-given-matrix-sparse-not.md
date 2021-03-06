# 检查给定矩阵是否稀疏

> 原文： [https://www.geeksforgeeks.org/check-given-matrix-sparse-not/](https://www.geeksforgeeks.org/check-given-matrix-sparse-not/)

矩阵是具有`m`行和`n`列的二维数据对象，因此共有`m * n`个值。 如果矩阵的大多数值是 0，那么我们说矩阵是稀疏的。

考虑稀疏的定义，如果 0 的数量大于矩阵元素的一半，则认为矩阵是稀疏的，

例子：

```
Input : 1 0 3
        0 0 4
        6 0 0
Output : Yes
There are 5 zeros. This count
is more than half of matrix
size.

Input : 1 2 3
        0 7 8
        5 0 7 
Output: No

```



要检查矩阵是否为稀疏矩阵，我们只需要检查等于零的元素总数即可。 如果此计数大于`(m * n) / 2`，则返回`true`。

## CPP

```

// CPP code to check if a matrix is 
// sparse. 
#include <iostream> 
using namespace std; 

const int MAX = 100; 

bool isSparse(int array[][MAX], int m, int n) 
{ 
    int counter = 0; 

    // Count number of zeros in the matrix 
    for (int i = 0; i < m; ++i) 
        for (int j = 0; j < n; ++j) 
            if (array[i][j] == 0) 
                ++counter; 

    return (counter > ((m * n) / 2)); 
} 

// Driver Function 
int main() 
{ 
    int array[][MAX] = { { 1, 0, 3 },  
                        { 0, 0, 4 },  
                        { 6, 0, 0 } }; 

    int m = 3, 
        n = 3; 
    if (isSparse(array, m, n)) 
        cout << "Yes"; 
    else
        cout << "No"; 
} 

```

## Java

```java

// Java code to check  
// if a matrix is 
// sparse. 

import java.io.*; 

class GFG { 

    static int MAX = 100; 

    static boolean isSparse(int array[][], int m, int n) 
    { 
        int counter = 0; 

        // Count number of zeros in the matrix 
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (array[i][j] == 0) 
                    ++counter; 

        return (counter > ((m * n) / 2)); 
    } 

    // Driver Function 
    public static void main(String args[]) 
    { 
        int array[][] = { { 1, 0, 3 },  
                            { 0, 0, 4 },  
                            { 6, 0, 0 } }; 

        int m = 3, 
            n = 3; 
        if (isSparse(array, m, n)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed by 
// Nikita Tiwari. 

```

## Python3

```py

# Python 3 code to check 
# if a matrix is 
# sparse. 

MAX = 100

def isSparse(array,m, n) : 

    counter = 0

    # Count number of zeros 
    # in the matrix 
    for i in range(0,m) : 
        for j in range(0,n) : 
            if (array[i][j] == 0) : 
                counter = counter + 1

    return (counter >  
            ((m * n) // 2)) 

# Driver Function 
array = [ [ 1, 0, 3 ], 
          [ 0, 0, 4 ], 
          [ 6, 0, 0 ] ] 
m = 3
n = 3

if (isSparse(array, m, n)) : 
    print("Yes") 
else : 
    print("No") 

# this code is contributed by 
# Nikita tiwari 

```

## C# 

```cs

// C# code to check if a matrix is 
// sparse. 
using System; 

class GFG { 

    static bool isSparse(int [,]array, int m, 
                                       int n) 
    { 
        int counter = 0; 

        // Count number of zeros in the matrix 
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (array[i,j] == 0) 
                    ++counter; 

        return (counter > ((m * n) / 2)); 
    } 

    // Driver Function 
    public static void Main() 
    { 
        int [,]array = { { 1, 0, 3 },  
                         { 0, 0, 4 },  
                         { 6, 0, 0 } }; 

        int m = 3, 
            n = 3; 

        if (isSparse(array, m, n)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP code to check if a matrix is 
// sparse. 

$MAX = 100; 

function isSparse( $array, $m, $n) 
{ 
    $counter = 0; 

    // Count number of zeros 
    // in the matrix 
    for ($i = 0; $i < $m; ++$i) 
        for ($j = 0; $j < $n; ++$j) 
            if ($array[$i][$j] == 0) 
                ++$counter; 

    return ($counter > (($m * $n) / 2)); 
} 

    // Driver Code 
    $array = array(array(1, 0, 3),  
                   array(0, 0, 4),  
                   array(6, 0, 0)); 

    $m = 3; 
    $n = 3; 
    if (isSparse($array, $m, $n)) 
        echo "Yes"; 
    else
        echo "No"; 

// This code is contributed by anuj_67\. 
?> 

```

Output:

```
Yes

```

