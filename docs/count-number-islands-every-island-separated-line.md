# 计算岛屿数量，每个岛按行和列分隔

> 原文： [https://www.geeksforgeeks.org/count-number-islands-every-island-separated-line/](https://www.geeksforgeeks.org/count-number-islands-every-island-separated-line/)

给定一个只有两个可能值`X`和`O`的矩形矩阵。 值`X`始终以矩形孤岛的形式出现，并且这些孤岛始终以行和列方式被至少一行`O`隔开。 请注意，岛只能沿对角线相邻。 计算给定矩阵中的孤岛数量。

**示例**：

```
mat[M][N] =  {{'O', 'O', 'O'},
              {'X', 'X', 'O'},
              {'X', 'X', 'O'},
              {'O', 'O', 'X'},
              {'O', 'O', 'X'},
              {'X', 'X', 'O'}
             };
Output: Number of islands is 3

mat[M][N] =  {{'X', 'O', 'O', 'O', 'O', 'O'},
              {'X', 'O', 'X', 'X', 'X', 'X'},
              {'O', 'O', 'O', 'O', 'O', 'O'},
              {'X', 'X', 'X', 'O', 'X', 'X'},
              {'X', 'X', 'X', 'O', 'X', 'X'},
              {'O', 'O', 'O', 'O', 'X', 'X'},
             };
Output: Number of islands is 4

```

**我们强烈建议您最小化您的浏览器，然后自己尝试。**

这个想法是计算给定矩阵的所有最左上角。 通过检查以下条件，我们可以检查`X`是否位于左上角。

1.  如果`X`位于矩形上方，如果位于其上方的单元格是`O`。

2.  如果`X`位于矩形的最左侧，如果位于其左侧的单元格是`O`。

请注意，我们必须检查这两个条件，因为在一个矩形岛中可能有一个以上的顶部单元和一个以上的最左侧单元。 以下是上述想法的实现。

## C/C++ 

```

// A C++ program to count the number of rectangular 
// islands where every island is separated by a line 
#include<iostream> 
using namespace std; 

// Size of given matrix is M X N 
#define M 6 
#define N 3 

// This function takes a matrix of 'X' and 'O' 
// and returns the number of rectangular islands 
// of 'X' where no two islands are row-wise or 
// column-wise adjacent, the islands may be diagonaly 
// adjacent 
int countIslands(int mat[][N]) 
{ 
    int count = 0; // Initialize result 

    // Traverse the input matrix 
    for (int i=0; i<M; i++) 
    { 
        for (int j=0; j<N; j++) 
        { 
            // If current cell is 'X', then check 
            // whether this is top-leftmost of a 
            // rectangle. If yes, then increment count 
            if (mat[i][j] == 'X') 
            { 
                if ((i == 0 || mat[i-1][j] == 'O') && 
                    (j == 0 || mat[i][j-1] == 'O')) 
                    count++; 
            } 
        } 
    } 

    return count; 
} 

// Driver program to test above function 
int main() 
{ 
    int mat[M][N] =  {{'O', 'O', 'O'}, 
                      {'X', 'X', 'O'}, 
                      {'X', 'X', 'O'}, 
                      {'O', 'O', 'X'}, 
                      {'O', 'O', 'X'}, 
                      {'X', 'X', 'O'} 
                    }; 
    cout << "Number of rectangular islands is "
         << countIslands(mat); 
    return 0; 
}

```

## Java

```java
// A Java program to count the number of rectangular 
// islands where every island is separated by a line 
import java.io.*; 
  
class islands  
{ 
    // This function takes a matrix of 'X' and 'O' 
    // and returns the number of rectangular islands 
    // of 'X' where no two islands are row-wise or 
    // column-wise adjacent, the islands may be diagonaly 
    // adjacent 
    static int countIslands(int mat[][], int m, int n) 
    { 
        // Initialize result 
        int count = 0;  
  
        // Traverse the input matrix 
        for (int i=0; i<m; i++) 
        { 
            for (int j=0; j<n; j++) 
            { 
                // If current cell is 'X', then check 
                // whether this is top-leftmost of a 
                // rectangle. If yes, then increment count 
                if (mat[i][j] == 'X') 
                { 
                    if ((i == 0 || mat[i-1][j] == 'O') && 
                        (j == 0 || mat[i][j-1] == 'O')) 
                        count++; 
                } 
            } 
        } 
  
        return count; 
    } 
      
    // Driver program 
    public static void main (String[] args)  
    { 
        // Size of given matrix is m X n 
        int m = 6; 
        int n = 3; 
        int mat[][] = {{'O', 'O', 'O'}, 
                        {'X', 'X', 'O'}, 
                        {'X', 'X', 'O'}, 
                        {'O', 'O', 'X'}, 
                        {'O', 'O', 'X'}, 
                        {'X', 'X', 'O'} 
                    }; 
        System.out.println("Number of rectangular islands is: " 
                                    + countIslands(mat, m, n)); 
    } 
} 
  
// This code is contributed by Pramod Kumar
```

## Python3

```py
# A Python3 program to count the number  
# of rectangular islands where every  
# island is separated by a line 
  
# Size of given matrix is M X N 
M = 6
N = 3
  
# This function takes a matrix of 'X' and 'O' 
# and returns the number of rectangular  
# islands of 'X' where no two islands are  
# row-wise or column-wise adjacent, the islands  
# may be diagonaly adjacent 
def countIslands(mat): 
  
    count = 0; # Initialize result 
  
    # Traverse the input matrix 
    for i in range (0, M): 
      
        for j in range(0, N): 
          
            # If current cell is 'X', then check 
            # whether this is top-leftmost of a 
            # rectangle. If yes, then increment count 
            if (mat[i][j] == 'X'): 
              
                if ((i == 0 or mat[i - 1][j] == 'O') and
                    (j == 0 or mat[i][j - 1] == 'O')): 
                    count = count + 1
              
    return count 
  
# Driver Code 
mat = [['O', 'O', 'O'], 
       ['X', 'X', 'O'], 
       ['X', 'X', 'O'], 
       ['O', 'O', 'X'], 
       ['O', 'O', 'X'], 
       ['X', 'X', 'O']] 
                  
print("Number of rectangular islands is",  
                       countIslands(mat)) 
  
# This code is contributed by iAyushRaj
```

## C#

```cs
// A C# program to count the number of rectangular  
// islands where every island is separated by  
// a line 
using System; 
  
class GFG { 
      
    // This function takes a matrix of 'X' and 'O' 
    // and returns the number of rectangular  
    // islands of 'X' where no two islands are 
    // row-wise or column-wise adjacent, the 
    // islands may be diagonaly adjacent 
    static int countIslands(int [,]mat, int m, int n) 
    { 
          
        // Initialize result 
        int count = 0;  
  
        // Traverse the input matrix 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                // If current cell is 'X', then check 
                // whether this is top-leftmost of a 
                // rectangle. If yes, then increment 
                // count 
                if (mat[i,j] == 'X') 
                { 
                    if ((i == 0 || mat[i-1,j] == 'O') && 
                        (j == 0 || mat[i,j-1] == 'O')) 
                        count++; 
                } 
            } 
        } 
  
        return count; 
    } 
      
    // Driver program 
    public static void Main ()  
    { 
          
        // Size of given matrix is m X n 
        int m = 6; 
        int n = 3; 
        int [,]mat = { {'O', 'O', 'O'}, 
                       {'X', 'X', 'O'}, 
                       {'X', 'X', 'O'}, 
                       {'O', 'O', 'X'}, 
                       {'O', 'O', 'X'}, 
                       {'X', 'X', 'O'} 
                    }; 
        Console.WriteLine("Number of rectangular "
         + "islands is: " + countIslands(mat, m, n)); 
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```php
<?php 
// A PHP program to count the 
// number of rectangular islands  
// where every island is separated 
// by a line 
// Size of given matrix is M X N 
  
// This function takes a matrix  
// of 'X' and 'O' and returns the 
// number of rectangular islands 
// of 'X' where no two islands are 
// row-wise or column-wise adjacent, 
// the islands may be diagonaly 
// adjacent 
function countIslands($mat) 
{ 
    $M = 6; 
    $N = 3; 
      
    // Initialize result 
    $count = 0;  
  
    // Traverse the input matrix 
    for($i = 0; $i < $M; $i++) 
    { 
        for ($j = 0; $j < $N; $j++) 
        { 
              
            // If current cell is  
            // 'X', then check whether 
            // this is top-leftmost of a 
            // rectangle. If yes, then  
            // increment count 
            if ($mat[$i][$j] == 'X') 
            { 
                if (($i == 0 || $mat[$i - 1][$j] == 'O') &&  
                    ($j == 0 || $mat[$i][$j-1] == 'O')) 
                    $count++; 
            } 
        } 
    } 
  
    return $count; 
} 
  
    // Driver Code 
    $mat = array(array('O', 'O', 'O'), 
                 array('X', 'X', 'O'), 
                 array('X', 'X', 'O'), 
                 array('O', 'O', 'X'), 
                 array('O', 'O', 'X'), 
                 array('X', 'X', 'O')); 
    echo "Number of rectangular islands is "
                       , countIslands($mat); 
                         
// This code is contributed by nitin mittal 
?>
```

输出：

```
Number of rectangular islands is 3
```

该解决方案的时间复杂度为`O(MN)`。