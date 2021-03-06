# 按升序对矩阵行进行排序，然后按降序对列进行排序

> 原文： [https://www.geeksforgeeks.org/sorting-rows-matrix-ascending-order-followed-sorting-columns-descending-order/](https://www.geeksforgeeks.org/sorting-rows-matrix-ascending-order-followed-sorting-columns-descending-order/)

给定矩阵，以升序对矩阵的行进行排序，然后以降序对列进行排序。

**示例**：

```
Input : a[3][3] = {{1, 2, 3},
                  {4, 5, 6}, 
                  {7, 8, 9}};
Output : 7 8 9
         4 5 6
         1 2 3

Input : a[3][3] = {{3, 2, 1},
                  {9, 8, 7}, 
                  {6, 5, 4}};
Output : 7 8 9
         4 5 6
         1 2 3

```



1.  遍历所有行，并使用简单数组排序以升序对行进行排序。

2.  将矩阵转换为其[转置](https://www.geeksforgeeks.org/c-program-find-transpose-matrix/)。

3.  再次对所有行进行排序，但是这次以升序排列。

4.  再次将矩阵转换为其[转置](https://www.geeksforgeeks.org/c-program-find-transpose-matrix/)。

## C++ 

```cpp

// C++ implementation to sort the rows 
// of matrix in ascending order followed by 
// sorting the columns in descending order 
#include <bits/stdc++.h> 
using namespace std; 

#define MAX_SIZE 10 

// function to sort each row of the matrix 
// according to the order specified by  
// ascending. 
void sortByRow(int mat[][MAX_SIZE], int n,  
                           bool ascending) 
{ 
    for (int i = 0; i < n; i++) 
    { 
      if (ascending)     
        sort(mat[i], mat[i] + n); 
      else
          sort(mat[i], mat[i] + n, greater<int>()); 
    }       
} 

// function to find transpose of the matrix 
void transpose(int mat[][MAX_SIZE], int n) 
{ 
    for (int i = 0; i < n; i++) 
        for (int j = i + 1; j < n; j++)  

            // swapping element at index (i, j)  
            // by element at index (j, i) 
            swap(mat[i][j], mat[j][i]); 
} 

// function to sort the matrix row-wise 
// and column-wise 
void sortMatRowAndColWise(int mat[][MAX_SIZE], 
                                       int n) 
{ 
    // sort rows of mat[][] 
    sortByRow(mat, n, true); 

    // get transpose of mat[][] 
    transpose(mat, n); 

    // again sort rows of mat[][] in descending 
    // order. 
    sortByRow(mat, n, false); 

    // again get transpose of mat[][] 
    transpose(mat, n); 
} 

// function to print the matrix 
void printMat(int mat[][MAX_SIZE], int n) 
{ 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) 
            cout << mat[i][j] << " "; 
        cout << endl; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    int n = 3; 

    int mat[n][MAX_SIZE]  = {{3, 2, 1}, 
                            {9, 8, 7},  
                            {6, 5, 4}}; 

    cout << "Original Matrix:\n"; 
    printMat(mat, n); 

    sortMatRowAndColWise(mat, n); 

    cout << "\nMatrix After Sorting:\n"; 
    printMat(mat, n); 

    return 0; 
} 

```

## Java

```java
// Java implementation to sort the rows 
// of matrix in ascending order followed by 
// sorting the columns in descending order 
import java.util.Arrays; 
import java.util.Collections; 
  
class GFG 
{ 
    static int MAX_SIZE=10; 
      
    // function to sort each row of the matrix 
    // according to the order specified by  
    // ascending. 
    static void sortByRow(Integer mat[][], int n,  
                                 boolean ascending) 
    { 
        for (int i = 0; i < n; i++) 
        { 
            if (ascending)  
                Arrays.sort(mat[i]); 
            else
                Arrays.sort(mat[i],Collections.reverseOrder()); 
        }      
    } 
      
    // function to find transpose of the matrix 
    static void transpose(Integer mat[][], int n) 
    { 
        for (int i = 0; i < n; i++) 
            for (int j = i + 1; j < n; j++)  
            { 
                // swapping element at index (i, j)  
                // by element at index (j, i) 
                int temp = mat[i][j]; 
                mat[i][j] = mat[j][i]; 
                mat[j][i] = temp; 
            } 
    } 
      
    // function to sort the matrix row-wise 
    // and column-wise 
    static void sortMatRowAndColWise(Integer mat[][], 
                                              int n) 
    { 
        // sort rows of mat[][] 
        sortByRow(mat, n, true); 
      
        // get transpose of mat[][] 
        transpose(mat, n); 
      
        // again sort rows of mat[][] in descending 
        // order. 
        sortByRow(mat, n, false); 
      
        // again get transpose of mat[][] 
        transpose(mat, n); 
    } 
      
    // function to print the matrix 
    static void printMat(Integer mat[][], int n) 
    { 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = 0; j < n; j++) 
                System.out.print(mat[i][j] + " "); 
            System.out.println(); 
        } 
    } 
      
    // Driver code 
    public static void main (String[] args)  
    { 
        int n = 3; 
          
        Integer mat[][] = {{3, 2, 1}, 
                           {9, 8, 7},  
                           {6, 5, 4}}; 
      
        System.out.print("Original Matrix:\n"); 
        printMat(mat, n); 
      
        sortMatRowAndColWise(mat, n); 
      
        System.out.print("\nMatrix After Sorting:\n"); 
        printMat(mat, n); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python implementation to sort the rows 
# of matrix in ascending order followed by 
# sorting the columns in descending order 
  
MAX_SIZE=10
   
# function to sort each row of the matrix 
# according to the order specified by  
# ascending. 
def sortByRow(mat, n, ascending): 
  
    for i in range(n): 
        if (ascending):     
            mat[i].sort() 
        else: 
            mat[i].sort(reverse=True) 
   
# function to find  
# transpose of the matrix 
def transpose(mat, n): 
  
    for i in range(n): 
        for j in range(i + 1, n):  
          
            # swapping element at index (i, j)  
            # by element at index (j, i) 
            temp = mat[i][j] 
            mat[i][j] = mat[j][i] 
            mat[j][i] = temp 
  
# function to sort  
# the matrix row-wise 
# and column-wise 
def sortMatRowAndColWise(mat, n): 
  
    # sort rows of mat[][] 
    sortByRow(mat, n, True) 
   
    # get transpose of mat[][] 
    transpose(mat, n) 
   
    # again sort rows of  
    # mat[][] in descending 
    # order. 
    sortByRow(mat, n, False) 
   
    # again get transpose of mat[][] 
    transpose(mat, n) 
   
# function to print the matrix 
def printMat(mat, n): 
  
    for i in range(n): 
        for j in range(n): 
            print(mat[i][j] , " ", end="") 
        print() 
  
#Driver code 
n = 3
       
mat = [[3, 2, 1], 
    [9, 8, 7],  
    [6, 5, 4]] 
   
print("Original Matrix:") 
printMat(mat, n) 
   
sortMatRowAndColWise(mat, n) 
   
print("Matrix After Sorting:") 
printMat(mat, n) 
  
# This code is contributed 
# by Anant Agarwal.
```

## PHP

```php
<?php  
// PHP implementation to sort the rows 
// of matrix in ascending order followed by 
// sorting the columns in descending order 
$MAX_SIZE = 10; 
  
// function to sort each row of the matrix 
// according to the order specified by  
// ascending. 
function sortByRow(&$mat, $n, $ascending) 
{ 
    for ($i = 0; $i < $n; $i++) 
    { 
        if ($ascending)  
            sort($mat[$i]); 
        else
            rsort($mat[$i]); 
    }      
} 
  
// function to find transpose 
// of the matrix 
function transpose(&$mat, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
    { 
        for ($j = $i + 1; $j < $n; $j++)  
        { 
            // swapping element at index (i, j)  
            // by element at index (j, i) 
            $temp = $mat[$i][$j]; 
            $mat[$i][$j] = $mat[$j][$i]; 
            $mat[$j][$i] = $temp; 
        } 
    } 
} 
  
// function to sort the matrix row-wise 
// and column-wise 
function sortMatRowAndColWise(&$mat, $n) 
{ 
    // sort rows of mat[][] 
    sortByRow($mat, $n, true); 
  
    // get transpose of mat[][] 
    transpose($mat, $n); 
  
    // again sort rows of mat[][] in  
    // descending order. 
    sortByRow($mat, $n, false); 
  
    // again get transpose of mat[][] 
    transpose($mat, $n); 
} 
  
// function to print the matrix 
function printMat(&$mat, $n) 
{ 
    for ($i = 0; $i < $n; $i++)  
    { 
        for ($j = 0; $j < $n; $j++) 
            echo $mat[$i][$j] . " "; 
        echo "\n" ; 
    } 
} 
  
// Driver Code 
$n = 3; 
  
$mat = array(array(3, 2, 1), 
             array(9, 8, 7),  
             array(6, 5, 4)); 
  
echo "Original Matrix:\n"; 
printMat($mat, $n); 
  
sortMatRowAndColWise($mat, $n); 
  
echo "\nMatrix After Sorting:\n"; 
printMat($mat, $n); 
  
// This code is contributed by Ita_c 
?>
```

输出：

```
Original Matrix:
3 2 1 
9 8 7 
6 5 4 

Matrix After Sorting:
7 8 9 
4 5 6 
1 2 3 
```

