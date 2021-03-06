# 在未排序的数组中找到出现奇数次的两个数字

> 原文： [https://www.geeksforgeeks.org/find-the-two-numbers-with-odd-occurences-in-an-unsorted-array/](https://www.geeksforgeeks.org/find-the-two-numbers-with-odd-occurences-in-an-unsorted-array/)

给定一个未排序的数组，其中包含除两个数字以外的所有数字的偶数个出现次数。 找出在`O(n)`时间复杂度和`O(1)`额外空间中出现奇数的两个数字。

例子：

```
Input: {12, 23, 34, 12, 12, 23, 12, 45}
Output: 34 and 45

Input: {4, 4, 100, 5000, 4, 4, 4, 4, 100, 100}
Output: 100 and 5000

Input: {10, 20}
Output: 10 and 20

```



解决此问题的一种**朴素的方法**是运行两个嵌套循环。 外循环拾取一个元素，内循环计数拾取的元素的出现次数。 如果出现次数是奇数，则打印数字。 该方法的时间复杂度为`O(n ^ 2)`。

我们可以使用**排序**来获得`O(nLogn)`时间中出现的奇数。 首先使用`O(nLogn)`排序算法（例如归并排序，堆排序等）对数字进行排序。对数组进行排序后，我们要做的就是对数组进行线性扫描并打印出现的奇数。

我们还可以**使用哈希**。 创建一个空的哈希表，其中将包含元素及其计数。 一一挑选输入数组的所有元素。 在哈希表中查找选择的元素。 如果在哈希表中找到该元素，则在表中增加其计数。 如果未找到该元素，则将其输入到哈希表中，计数为 1。将所有元素输入哈希表后，扫描哈希表并打印具有奇数的元素。 这种方法平均可能需要`O(n)`时间，但需要`O(n)`额外空间。

**`O(n)`时间和`O(1)`额外空间解决方案**：

这个想法类似于此帖子的方法 2。 令两个出现的奇数为`x`和`y`。 我们**使用按位异或**获得`x`和`y`。 第一步是对数组中存在的所有元素进行 XOR。 由于 XOR 运算的以下特性，所有元素的 XOR 使我们对`x`和`y`进行 XOR。

1.  任何数字`n`与自身的 XOR 给我们 0，即`n ^ n = 0`。

2.  任何数字`n`与 0 的 XOR 给我们`n`，即`n ^ 0 = n`。

3.  [XOR 是累积性和关联性的](https://www.geeksforgeeks.org/find-two-non-repeating-elements-in-an-array-of-repeating-elements/)。

因此，第一步之后，我们对`x`和`y`进行了 XOR。 令 XOR 的值为`xor2`。 `xor2`中的每个置位指示`x`和`y`中的对应位具有彼此不同的值。 例如，如果`x = 6`（0110）并且`y`为 15（1111），则`xor2`将为（1001），`xor2`中的两个置位指示`x`和`y`中的相应位不同。 在第二步中，我们选择`xor2`的一个固定位并将数组元素分为两组。 `x`和`y`将进入不同的组。 在下面的代码中，选择`xor2`的最右边设置位是因为很容易获得数字的最右边设置位。 如果我们对所有具有对应位集（或 1）的数组元素进行 XOR，则得到第一个奇数。 而且，如果我们对所有具有相应位 0 的元素进行 XOR，那么我们将获得另一个奇数发生数。 由于 XOR 具有相同的属性，因此可以执行此步骤。 一个数字的所有出现都将进入同一集合。 对所有出现的偶数次出现的所有数字进行 XOR 运算，其结果将为 0。 集合的异或将是奇数发生的元素之一。

## C++

```cpp
// C++ Program to find the two odd occurring elements  
#include <bits/stdc++.h> 
using namespace std; 
  
/* Prints two numbers that occur odd number of times. The  
function assumes that the array size is at least 2 and  
there are exactly two numbers occurring odd number of times. */
void printTwoOdd(int arr[], int size)  
{  
    int xor2 = arr[0]; /* Will hold XOR of two odd occurring elements */
    int set_bit_no; /* Will have only single set bit of xor2 */
    int i;  
    int n = size - 2;  
    int x = 0, y = 0;  
      
    /* Get the xor of all elements in arr[]. The xor will basically  
        be xor of two odd occurring elements */
    for(i = 1; i < size; i++)  
        xor2 = xor2 ^ arr[i];  
      
    /* Get one set bit in the xor2. We get rightmost set bit  
        in the following line as it is easy to get */
    set_bit_no = xor2 & ~(xor2-1);  
      
    /* Now divide elements in two sets:  
        1) The elements having the corresponding bit as 1.  
        2) The elements having the corresponding bit as 0. */
    for(i = 0; i < size; i++)  
    {  
        /* XOR of first set is finally going to hold one odd  
        occurring number x */
        if(arr[i] & set_bit_no)  
        x = x ^ arr[i];  
      
        /* XOR of second set is finally going to hold the other  
        odd occurring number y */
        else
        y = y ^ arr[i];  
    }  
  
    cout << "The two ODD elements are " << x << " & " << y;  
}  
  
/* Driver code */
int main()  
{  
    int arr[] = {4, 2, 4, 5, 2, 3, 3, 1};  
    int arr_size = sizeof(arr)/sizeof(arr[0]);  
    printTwoOdd(arr, arr_size);  
    return 0;  
}  
  
// This is code is contributed by rathbhupendra
```

## C

```c
// Program to find the two odd occurring elements 
#include<stdio.h> 
  
/* Prints two numbers that occur odd number of times. The 
   function assumes that the array size is at least 2 and 
   there are exactly two numbers occurring odd number of times. */
void printTwoOdd(int arr[], int size) 
{ 
  int xor2 = arr[0]; /* Will hold XOR of two odd occurring elements */
  int set_bit_no;  /* Will have only single set bit of xor2 */
  int i; 
  int n = size - 2; 
  int x = 0, y = 0; 
  
  /* Get the xor of all elements in arr[]. The xor will basically 
     be xor of two odd occurring elements */
  for(i = 1; i < size; i++) 
    xor2 = xor2 ^ arr[i]; 
  
  /* Get one set bit in the xor2. We get rightmost set bit 
     in the following line as it is easy to get */
  set_bit_no = xor2 & ~(xor2-1); 
  
  /* Now divide elements in two sets:  
    1) The elements having the corresponding bit as 1.  
    2) The elements having the corresponding bit as 0.  */
  for(i = 0; i < size; i++) 
  { 
     /* XOR of first set is finally going to hold one odd  
       occurring number x */ 
    if(arr[i] & set_bit_no) 
      x = x ^ arr[i]; 
  
     /* XOR of second set is finally going to hold the other  
       odd occurring number y */ 
    else
      y = y ^ arr[i];  
  } 
  
  printf("\n The two ODD elements are %d & %d ", x, y); 
} 
  
/* Driver program to test above function */
int main() 
{ 
  int arr[] = {4, 2, 4, 5, 2, 3, 3, 1}; 
  int arr_size = sizeof(arr)/sizeof(arr[0]); 
  printTwoOdd(arr, arr_size); 
  getchar(); 
  return 0; 
}
```

## Java

```java
// Java program to find two odd 
// occurring elements 
  
import java.util.*; 
  
class Main 
{    
       
    /* Prints two numbers that occur odd  
       number of times. The function assumes  
       that the array size is at least 2 and 
       there are exactly two numbers occurring  
       odd number of times. */
    static void printTwoOdd(int arr[], int size) 
    { 
      /* Will hold XOR of two odd occurring elements */    
      int xor2 = arr[0];  
        
      /* Will have only single set bit of xor2 */
      int set_bit_no;   
      int i; 
      int n = size - 2; 
      int x = 0, y = 0; 
       
      /* Get the xor of all elements in arr[].  
         The xor will basically be xor of two  
         odd occurring elements */
      for(i = 1; i < size; i++) 
        xor2 = xor2 ^ arr[i]; 
       
      /* Get one set bit in the xor2. We get  
         rightmost set bit in the following  
         line as it is easy to get */
      set_bit_no = xor2 & ~(xor2-1); 
       
      /* Now divide elements in two sets:  
            1) The elements having the  
               corresponding bit as 1.  
            2) The elements having the  
               corresponding bit as 0.  */
      for(i = 0; i < size; i++) 
      { 
         /* XOR of first set is finally going  
            to hold one odd occurring number x */
        if((arr[i] & set_bit_no)>0) 
          x = x ^ arr[i]; 
       
         /* XOR of second set is finally going  
            to hold the other odd occurring number y */
        else
          y = y ^ arr[i];  
      } 
       
      System.out.println("The two ODD elements are "+ 
                                        x + " & " + y); 
    } 
      
    // main function 
    public static void main (String[] args)  
    { 
        int arr[] = {4, 2, 4, 5, 2, 3, 3, 1}; 
        int arr_size = arr.length; 
        printTwoOdd(arr, arr_size); 
    } 
}
```

## Python3

```py
# Python3 program to find the 
# two odd occurring elements 
  
# Prints two numbers that occur odd 
# number of times. The function assumes 
# that the array size is at least 2 and 
# there are exactly two numbers occurring 
# odd number of times. 
def printTwoOdd(arr, size): 
      
    # Will hold XOR of two odd occurring elements  
    xor2 = arr[0]  
      
    # Will have only single set bit of xor2 
    set_bit_no = 0  
    n = size - 2
    x, y = 0, 0
  
    # Get the xor of all elements in arr[].  
    # The xor will basically be xor of two 
    # odd occurring elements  
    for i in range(1, size): 
        xor2 = xor2 ^ arr[i] 
  
    # Get one set bit in the xor2. We get  
    # rightmost set bit in the following  
    # line as it is easy to get  
    set_bit_no = xor2 & ~(xor2 - 1) 
  
    # Now divide elements in two sets:  
    # 1) The elements having the corresponding bit as 1.  
    # 2) The elements having the corresponding bit as 0.  
    for i in range(size): 
      
        # XOR of first set is finally going to   
        # hold one odd  occurring number x  
        if(arr[i] & set_bit_no): 
            x = x ^ arr[i] 
  
        # XOR of second set is finally going  
        # to hold the other odd occurring number y  
        else: 
            y = y ^ arr[i]  
  
    print("The two ODD elements are", x, "&", y) 
  
# Driver Code 
arr = [4, 2, 4, 5, 2, 3, 3, 1] 
arr_size = len(arr) 
printTwoOdd(arr, arr_size) 
  
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// C# program to find two odd 
// occurring elements 
using System; 
  
class main 
{    
        
    // Prints two numbers that occur 
    // odd number of times. Function 
    // assumes that array size is at 
    // least 2 and there are exactly 
    // two numbers occurring odd number 
    // of times. 
    static void printTwoOdd(int []arr, int size) { 
     
      // Will hold XOR of two odd 
      //occurring elements    
      int xor2 = arr[0];  
         
      // Will have only single set 
      // bit of xor2 
      int set_bit_no;   
      int i; 
        
      //int n = size - 2; 
      int x = 0, y = 0; 
        
      // Get the xor of all the elements 
      // in arr[].The xor will basically  
      // be xor of two odd occurring 
      // elements 
      for(i = 1; i < size; i++) 
        xor2 = xor2 ^ arr[i]; 
        
      // Get one set bit in the xor2. 
      // We get rightmost set bit in 
      // the following line as it is 
      // to get. 
         set_bit_no = xor2 & ~(xor2-1); 
        
      // divide elements in two sets:  
      // 1) The elements having the  
      // corresponding bit as 1.  
      // 2) The elements having the  
      // corresponding bit as 0. 
      for(i = 0; i < size; i++) 
      { 
         // XOR of first set is finally  
         // going to hold one odd  
         // occurring number x 
            if((arr[i] & set_bit_no)>0) 
            x = x ^ arr[i]; 
        
            // XOR of second set is finally 
            // going to hold the other  
            // odd occurring number y 
            else
            y = y ^ arr[i];  
      } 
        
      Console.WriteLine("The two ODD elements are "+ 
                                        x + " & " + y); 
    } 
       
    // main function 
    public static void Main()  
    { 
        int []arr = {4, 2, 4, 5, 2, 3, 3, 1}; 
        int arr_size = arr.Length; 
        printTwoOdd(arr, arr_size); 
    } 
} 
  
//This code is contributed by Anant Agarwal.
```

## PHP

```php
<?php 
// PHP program to find the  
// two odd occurring elements 
  
/* Prints two numbers that occur 
   odd number of times. The 
   function assumes that the  
   array size is at least 2 and 
   there are exactly two numbers  
   occurring odd number of times. */
function printTwoOdd($arr, $size) 
{ 
      
     // Will hold XOR of two  
     // odd occurring elements 
     $xor2 = $arr[0]; 
       
     // Will have only single  
     // set bit of xor2  
     $set_bit_no; 
       
    $i; 
    $n = $size - 2; 
    $x = 0;$y = 0; 
  
     // Get the xor of all elements 
     // in arr[]. The xor will basically 
     // be xor of two odd occurring  
     // elements  
    for($i = 1; $i < $size; $i++) 
        $xor2 = $xor2 ^ $arr[$i]; 
      
    // Get one set bit in the xor2.  
    // We get rightmost set bit 
    // in the following line as  
    // it is easy to get  
    $set_bit_no = $xor2 & ~($xor2-1); 
      
    /* Now divide elements in two sets:  
        1) The elements having the 
           corresponding bit as 1.  
        2) The elements having the  
           corresponding bit as 0. */
    for($i = 0; $i < $size; $i++) 
    { 
          
        /* XOR of first set is finally  
           going to hold one odd  
           occurring number x */
        if($arr[$i] & $set_bit_no) 
        $x = $x ^ $arr[$i]; 
      
        /* XOR of second set is finally 
           going to hold the other  
           odd occurring number y */
        else
        $y = $y ^ $arr[$i];  
    } 
      
    echo "The two ODD elements are ", $x, " & ", $y; 
    } 
  
// Driver Code 
$arr = array(4, 2, 4, 5, 2, 3, 3, 1); 
$arr_size = sizeof($arr); 
printTwoOdd($arr, $arr_size); 
  
// This code is Contributed by Ajit 
?>
```

输出：

```
The two ODD elements are 5 & 1
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。

