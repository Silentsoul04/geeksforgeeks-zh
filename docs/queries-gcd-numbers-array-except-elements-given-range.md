# 查询给定数组中所有数字的 GCD（给定范围内的元素除外）

> 原文： [https://www.geeksforgeeks.org/queries-gcd-numbers-array-except-elements-given-range/](https://www.geeksforgeeks.org/queries-gcd-numbers-array-except-elements-given-range/)

给定一个由`n`个数字组成的数组，并给出了多个查询。 每个查询将由两个整数`l`，`r`表示。 任务是找出每个查询的数组中所有数字的 [GCD](https://en.wikipedia.org/wiki/Greatest_common_divisor)，但不包括范围`l`，`r`（包括两端）中给出的数字。

**示例**：

```
Input : arr[] = {2, 6, 9}
        Ranges [0 0], [1 1], [1 2]
Output : 3
         1
         2 
GCD of numbers excluding [0 0] or 
first element is GCD(6, 9) = 3
GCD of numbers excluding the [1 1] or
second element is GCD(2, 9) = 1
GCD of numbers excluding [1 2] is 
equal to first element = 2

```



**注意**：在下面的说明中，我们使用基于 1 的索引。

我们从一个非常基本的问题开始，如何计算两个数字的 GCD，最好的选择是 [Euclid 算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)。 现在如何计算一个以上数字的 GCD，简单地假设存在三个数字`a`，`b`和`c`，则解决方案很简单。`GCD(a, b, c) = GCD(GCD(a, b), c)`。 这样，我们可以轻松找出任意数量的 GCD。

解决每个查询问题的一种**简单方法**假定给定的范围是`l`和`r`。 假设从 1 到`l-1`的数字的 GCD 为`x`，然后取从`r + 1`到`n`的数字的 GCD，让它为`y`，则每个查询的输出将为`GCD(x, y)`。

一种有效的**解决方案**是使用两个数组，一个作为前缀数组，第二个作为后缀数组。 前缀数组的第`i`个索引将存储从 1 到`i`的数字的 GCD，后缀数组的第`i`个索引将表示从`i`到`n`的数字的 GCD。 现在假设给定的特定查询范围是`l`，`r`，很明显该查询的输出将是`GCD(prefix[l - 1], suffix[r + 1])`。

## C++ 

```cpp

// C++ program for queries of GCD excluding 
// given range of elements. 
#include<bits/stdc++.h> 
using namespace std; 

// Filling the prefix and suffix array 
void FillPrefixSuffix(int prefix[], int arr[], 
                           int suffix[], int n) 
{ 
    // Filling the prefix array following relation 
    // prefix(i) = __gcd(prefix(i-1), arr(i)) 
    prefix[0] = arr[0]; 
    for (int i=1 ;i<n; i++) 
        prefix[i] = __gcd(prefix[i-1], arr[i]); 

    // Filling the suffix array following the 
    // relation suffix(i) = __gcd(suffix(i+1), arr(i)) 
    suffix[n-1] = arr[n-1]; 

    for (int i=n-2; i>=0 ;i--) 
        suffix[i] = __gcd(suffix[i+1], arr[i]); 
} 

// To calculate gcd of the numbers outside range 
int GCDoutsideRange(int l, int r, int prefix[], 
                           int suffix[], int n) 
{ 
    // If l=0, we need to tell GCD of numbers 
    // from r+1 to n 
    if (l==0) 
        return suffix[r+1]; 

    // If r=n-1 we need to return the gcd of 
    // numbers from 1 to l 
    if (r==n-1) 
        return prefix[l-1]; 
    return __gcd(prefix[l-1], suffix[r+1]); 
} 

// Driver function 
int main() 
{ 
    int arr[] = {2, 6, 9}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int prefix[n], suffix[n]; 
    FillPrefixSuffix(prefix, arr, suffix, n); 

    int l = 0, r = 0; 
    cout << GCDoutsideRange(l, r, prefix, suffix, n) 
         << endl; 
    l = 1 ; r = 1; 
    cout << GCDoutsideRange(l, r, prefix, suffix, n) 
         << endl; 
    l = 1 ; r = 2; 
    cout << GCDoutsideRange(l, r, prefix, suffix, n) 
         << endl; 
    return 0; 
} 

```

## Java

```java

// Java program for queries of GCD excluding 
// given range of elements. 
import java.util.*; 

class GFG { 

// Calculating GCD using euclid algorithm 
static int GCD(int a, int b) 
{ 
    if (b == 0) 
    return a; 
    return GCD(b, a % b); 
} 

// Filling the prefix and suffix array 
static void FillPrefixSuffix(int prefix[],  
          int arr[], int suffix[], int n)  
{ 
    // Filling the prefix array following relation 
    // prefix(i) = GCD(prefix(i-1), arr(i)) 
    prefix[0] = arr[0]; 
    for (int i = 1; i < n; i++) 
    prefix[i] = GCD(prefix[i - 1], arr[i]); 

    // Filling the suffix array folowing the 
    // relation suffix(i) = GCD(suffix(i+1), arr(i)) 
    suffix[n - 1] = arr[n - 1]; 

    for (int i = n - 2; i >= 0; i--) 
    suffix[i] = GCD(suffix[i + 1], arr[i]); 
} 

// To calculate gcd of the numbers outside range 
static int GCDoutsideRange(int l, int r, 
      int prefix[], int suffix[], int n) { 

    // If l=0, we need to tell GCD of numbers 
    // from r+1 to n 
    if (l == 0) 
    return suffix[r + 1]; 

    // If r=n-1 we need to return the gcd of 
    // numbers from 1 to l 
    if (r == n - 1) 
    return prefix[l - 1]; 
    return GCD(prefix[l - 1], suffix[r + 1]); 
} 

// Driver code 
public static void main(String[] args) { 
    int arr[] = {2, 6, 9}; 
    int n = arr.length; 
    int prefix[] = new int[n]; 
    int suffix[] = new int[n]; 
    FillPrefixSuffix(prefix, arr, suffix, n); 

    int l = 0, r = 0; 
    System.out.println(GCDoutsideRange 
             (l, r, prefix, suffix, n)); 

    l = 1; 
    r = 1; 
    System.out.println(GCDoutsideRange 
             (l, r, prefix, suffix, n)); 

    l = 1; 
    r = 2; 
    System.out.println(GCDoutsideRange 
             (l, r, prefix, suffix, n)); 
} 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python program for 
# queries of GCD excluding 
# given range of elements. 

# Calculating GCD 
# using euclid algorithm 
def GCD(a,b): 
    if (b==0): 
        return a 
    return GCD (b, a%b) 

# Filling the prefix 
# and suffix array 
def FillPrefixSuffix(prefix,arr,suffix,n): 

    # Filling the prefix array 
    # following relation 
    # prefix(i) = GCD(prefix(i-1), arr(i)) 
    prefix[0] = arr[0] 
    for i in range(1,n): 
        prefix[i] = GCD (prefix[i-1], arr[i]) 

    # Filling the suffix 
    # array folowing the 
    # relation suffix(i) = GCD(suffix(i+1), arr(i)) 
    suffix[n-1] = arr[n-1] 

    for i in range(n-2,-1,-1): 
        suffix[i] = GCD (suffix[i+1], arr[i]) 

# To calculate gcd of 
# the numbers outside range 
def GCDoutsideRange(l,r,prefix,suffix,n): 

    # If l=0, we need to tell GCD of numbers 
    # from r+1 to n 
    if (l==0): 
        return suffix[r+1] 

    # If r=n-1 we need to return the gcd of 
    # numbers from 1 to l 
    if (r==n-1): 
        return prefix[l-1] 
    return GCD(prefix[l-1], suffix[r+1]) 

# Driver code 

arr = [2, 6, 9] 
n = len(arr) 
prefix=[] 
suffix=[] 
for i in range(n+1): 
    prefix.append(0) 
    suffix.append(0) 

FillPrefixSuffix(prefix, arr, suffix, n) 
l = 0 
r = 0
print(GCDoutsideRange(l, r, prefix, suffix, n)) 

l = 1
r = 1
print(GCDoutsideRange(l, r, prefix, suffix, n)) 

l = 1
r = 2
print(GCDoutsideRange(l, r, prefix, suffix, n)) 

# This code is contributed 
# by Anant Agarwal. 

```

## C# 

```cs

// C# program for queries of GCD  
// excluding given range of elements. 
using System; 

class GFG { 

// Calculating GCD using  
// euclid algorithm 
static int GCD(int a, int b) 
{ 
    if (b == 0) 
    return a; 
    return GCD(b, a % b); 
} 

// Filling the prefix and suffix array 
static void FillPrefixSuffix(int []prefix,  
                             int []arr,  
                             int []suffix, 
                             int n)  
{ 

    // Filling the prefix array following 
    // relation prefix(i) =  
    // GCD(prefix(i - 1), arr(i)) 
    prefix[0] = arr[0]; 
    for (int i = 1; i < n; i++) 
    prefix[i] = GCD(prefix[i - 1], arr[i]); 

    // Filling the suffix array folowing  
    // the relation suffix(i) =  
    // GCD(suffix(i+1), arr(i)) 
    suffix[n - 1] = arr[n - 1]; 

    for (int i = n - 2; i >= 0; i--) 
    suffix[i] = GCD(suffix[i + 1], arr[i]); 
} 

// To calculate gcd of the numbers outside range 
static int GCDoutsideRange(int l, int r, 
                           int []prefix,  
                           int []suffix, 
                           int n) 
    { 

    // If l=0, we need to tell  
    // GCD of numbers from r+1 to n 
    if (l == 0) 
    return suffix[r + 1]; 

    // If r=n-1 we need to return the  
    // gcd of numbers from 1 to l 
    if (r == n - 1) 
    return prefix[l - 1]; 
    return GCD(prefix[l - 1], suffix[r + 1]); 
} 

// Driver Code 
public static void Main() 
{ 
    int []arr = {2, 6, 9}; 
    int n = arr.Length; 
    int []prefix = new int[n]; 
    int []suffix = new int[n]; 
    FillPrefixSuffix(prefix, arr, suffix, n); 

    int l = 0, r = 0; 
    Console.WriteLine(GCDoutsideRange 
                     (l, r, prefix, suffix, n)); 

    l = 1; 
    r = 1; 
    Console.WriteLine(GCDoutsideRange 
                        (l, r, prefix, suffix, n)); 

    l = 1; 
    r = 2; 
    Console.Write(GCDoutsideRange 
                 (l, r, prefix, suffix, n)); 
} 
} 

// This code is contributed by Nitin Mittal. 

```

## PHP

```php

<?php  
// PHP program for queries of GCD excluding 
// given range of elements. 

// Calculating GCD using euclid algorithm 
function GCD($a, $b) 
{ 
    if ($b == 0) 
        return $a; 
    return GCD ($b, $a % $b); 
} 

// Filling the prefix and suffix array 
function FillPrefixSuffix(&$prefix, &$arr, &$suffix, $n) 
{ 
    // Filling the prefix array following relation 
    // prefix(i) = GCD(prefix(i-1), arr(i)) 
    $prefix[0] = $arr[0]; 
    for ($i = 1; $i < $n; $i++) 
        $prefix[$i] = GCD ($prefix[$i - 1], $arr[$i]); 

    // Filling the suffix array folowing the 
    // relation suffix(i) = GCD(suffix(i+1), arr(i)) 
    $suffix[$n - 1] = $arr[$n - 1]; 

    for ($i = $n - 2; $i >= 0 ;$i--) 
        $suffix[$i] = GCD ($suffix[$i + 1], $arr[$i]); 
} 

// To calculate gcd of the numbers outside range 
function GCDoutsideRange($l, $r, &$prefix, &$suffix, $n) 
{ 
    // If l=0, we need to tell GCD of numbers 
    // from r+1 to n 
    if ($l == 0) 
        return $suffix[$r + 1]; 

    // If r=n-1 we need to return the gcd of 
    // numbers from 1 to l 
    if ($r == $n - 1) 
        return $prefix[$l - 1]; 
    return GCD($prefix[$l - 1], $suffix[$r + 1]); 
} 

// Driver Code 
$arr = array(2, 6, 9); 
$n = sizeof($arr); 
$prefix = array_fill(0, $n, NULL); 
$suffix = array_fill(0, $n, NULL); 
FillPrefixSuffix($prefix, $arr, $suffix, $n); 

$l = 0; 
$r = 0; 
echo GCDoutsideRange($l, $r, $prefix, $suffix, $n) . "\n"; 
$l = 1 ; 
$r = 1; 
echo GCDoutsideRange($l, $r, $prefix, $suffix, $n) . "\n"; 
$l = 1 ; 
$r = 2; 
echo GCDoutsideRange($l, $r, $prefix, $suffix, $n) . "\n"; 

// This code is contributed by ita_c 
?> 

```

**输出**：

```
3
1
2

```

