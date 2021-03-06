# 数组旋转程序

> 原文： [https://www.geeksforgeeks.org/array-rotation/](https://www.geeksforgeeks.org/array-rotation/)

编写一个函数`turn(ar[], d, n)`，该函数将大小为`n`的`arr[]`旋转`d`个元素。

![Array](img/2977f0e946a3bb34a3b4fd46d9b0fc5e.png "Array")

将上面的数组旋转 2 将产生数组：

![ArrayRotation1](img/bc7352a2ba78ed382cec52dde78d1e6f.png "ArrayRotation1")



**方法 1（使用临时数组）**：

```
Input arr[] = [1, 2, 3, 4, 5, 6, 7], d = 2, n =7
1) Store the first d elements in a temp array
   temp[] = [1, 2]
2) Shift rest of the arr[]
   arr[] = [3, 4, 5, 6, 7, 6, 7]
3) Store back the d elements
   arr[] = [3, 4, 5, 6, 7, 1, 2]
```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(d)`。

**方法 2（一轮旋转）**：

```
leftRotate(arr[], d, n)
start
  For i = 0 to i < d
    Left rotate all elements of arr[] by one
end
```

要旋转一个，将`arr[0]`存储在临时变量`temp`中，将`arr[1]`移至`arr[0]`，将`arr[2]`移至`arr[1]`…最后将`temp`移至`arr[n-1]`。

让我们以相同的示例`arr[] = [1,2,3,4,5,6,7]`，`d = 2`。将`arr []`旋转 2 次，我们得到`[2, 3]`，第一次旋转后为`[4, 5, 6, 7, 1]`，第二次旋转后为`[3, 4, 5, 6, 7, 1, 2]`。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to rotate an array by 
// d elements 
#include <bits/stdc++.h> 
using namespace std; 

/*Function to left Rotate arr[] of  
  size n by 1*/
void leftRotatebyOne(int arr[], int n) 
{ 
    int temp = arr[0], i; 
    for (i = 0; i < n - 1; i++) 
        arr[i] = arr[i + 1]; 

    arr[i] = temp; 
} 

/*Function to left rotate arr[] of size n by d*/
void leftRotate(int arr[], int d, int n) 
{ 
    for (int i = 0; i < d; i++) 
        leftRotatebyOne(arr, n); 
} 

/* utility function to print an array */
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // Function calling 
    leftRotate(arr, 2, n); 
    printArray(arr, n); 

    return 0; 
} 

```

## C

```c
// C program to rotate an array by 
// d elements 
#include <stdio.h> 
  
/* Function to left Rotate arr[] of size n by 1*/
void leftRotatebyOne(int arr[], int n); 
  
/*Function to left rotate arr[] of size n by d*/
void leftRotate(int arr[], int d, int n) 
{ 
    int i; 
    for (i = 0; i < d; i++) 
        leftRotatebyOne(arr, n); 
} 
  
void leftRotatebyOne(int arr[], int n) 
{ 
    int temp = arr[0], i; 
    for (i = 0; i < n - 1; i++) 
        arr[i] = arr[i + 1]; 
    arr[i] = temp; 
} 
  
/* utility function to print an array */
void printArray(int arr[], int n) 
{ 
    int i; 
    for (i = 0; i < n; i++) 
        printf("%d ", arr[i]); 
} 
  
/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 }; 
    leftRotate(arr, 2, 7); 
    printArray(arr, 7); 
    return 0; 
} 
```

## Java

```java
// Java program to rotate an array by 
// d elements 
  
class RotateArray { 
    /*Function to left rotate arr[] of size n by d*/
    void leftRotate(int arr[], int d, int n) 
    { 
        for (int i = 0; i < d; i++) 
            leftRotatebyOne(arr, n); 
    } 
  
    void leftRotatebyOne(int arr[], int n) 
    { 
        int i, temp; 
        temp = arr[0]; 
        for (i = 0; i < n - 1; i++) 
            arr[i] = arr[i + 1]; 
        arr[i] = temp; 
    } 
  
    /* utility function to print an array */
    void printArray(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args) 
    { 
        RotateArray rotate = new RotateArray(); 
        int arr[] = { 1, 2, 3, 4, 5, 6, 7 }; 
        rotate.leftRotate(arr, 2, 7); 
        rotate.printArray(arr, 7); 
    } 
} 
  
// This code has been contributed by Mayank Jaiswal 
```

## Python3

```py
# Python3 program to rotate an array by  
# d elements  
# Function to left rotate arr[] of size n by d*/ 
def leftRotate(arr, d, n): 
    for i in range(d): 
        leftRotatebyOne(arr, n) 
  
# Function to left Rotate arr[] of size n by 1*/  
def leftRotatebyOne(arr, n): 
    temp = arr[0] 
    for i in range(n-1): 
        arr[i] = arr[i + 1] 
    arr[n-1] = temp 
          
  
# utility function to print an array */ 
def printArray(arr, size): 
    for i in range(size): 
        print ("% d"% arr[i], end =" ") 
  
   
# Driver program to test above functions */ 
arr = [1, 2, 3, 4, 5, 6, 7] 
leftRotate(arr, 2, 7) 
printArray(arr, 7) 
  
# This code is contributed by Shreyanshi Arun 
```

### C#

```cs
// C# program for array rotation 
using System; 
  
class GFG { 
    /* Function to left rotate arr[] 
    of size n by d*/
    static void leftRotate(int[] arr, int d, 
                           int n) 
    { 
        for (int i = 0; i < d; i++) 
            leftRotatebyOne(arr, n); 
    } 
  
    static void leftRotatebyOne(int[] arr, int n) 
    { 
        int i, temp = arr[0]; 
        for (i = 0; i < n - 1; i++) 
            arr[i] = arr[i + 1]; 
  
        arr[i] = temp; 
    } 
  
    /* utility function to print an array */
    static void printArray(int[] arr, int size) 
    { 
        for (int i = 0; i < size; i++) 
            Console.Write(arr[i] + " "); 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 2, 3, 4, 5, 6, 7 }; 
        leftRotate(arr, 2, 7); 
        printArray(arr, 7); 
    } 
} 
  
// This code is contributed by Sam007 
```

## PHP

```php
<?php  
// PHP program to rotate an array 
// by d elements 
  
/*Function to left Rotate arr[]   
of size n by 1*/
function leftRotatebyOne(&$arr, $n) 
{ 
    $temp = $arr[0]; 
    for ($i = 0; $i < $n - 1; $i++) 
        $arr[$i] = $arr[$i + 1]; 
  
    $arr[$i] = $temp; 
} 
  
/*Function to left rotate arr[]  
  of size n by d*/
function leftRotate(&$arr, $d, $n) 
{ 
    for ($i = 0; $i < $d; $i++) 
        leftRotatebyOne($arr, $n); 
} 
  
/* utility function to print  
   an array */
function printArray(&$arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
        echo $arr[$i] . " "; 
} 
  
// Driver Code 
$arr = array( 1, 2, 3, 4, 5, 6, 7 ); 
$n = sizeof($arr); 
  
// Function calling 
leftRotate($arr, 2, $n); 
printArray($arr, $n); 
  
// This code is contributed 
// by ChitraNayal 
?> 
```

输出：

```
3 4 5 6 7 1 2 
```

时间复杂度：`O(n * d)`。

空间复杂度：`O(1)`。