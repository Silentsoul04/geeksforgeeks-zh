# 查找丢失的数字

> 原文： [https://www.geeksforgeeks.org/find-the-missing-number/](https://www.geeksforgeeks.org/find-the-missing-number/)

系统会为您提供`n-1`个整数的列表，这些整数在 1 到`n`的范围内。 列表中没有重复项。 列表中缺少整数之一。 编写有效的代码以查找丢失的整数。

**示例**：

```
Input: arr[] = {1, 2, 4, 6, 3, 7, 8}
Output: 5
Explanation: The missing number from 1 to 8 is 5

Input: arr[] = {1, 2, 3, 5}
Output: 4
Explanation: The missing number from 1 to 5 is 4

```



**方法 1**：此方法使用求和公式的技术。

*   **方法**：数组的长度为`n-1`。 因此，可以使用公式`n * (n + 1) / 2`计算所有`n`个元素的总和，即从 1 到`n`的数字之和。 现在找到数组中所有元素的总和，并从前`n`个自然数的总和中减去它，这将是缺失元素的值。

*   **算法**：

    1.  将前`n`个自然数的总和计算为`sumtotal = n * (n + 1) / 2`。

    2.  创建一个变量`sum`来存储数组元素的和。

    3.  从头到尾遍历数组。

    4.  将`sum`的值更新为`sum = sum + array[i]`。

    5.  将缺少的数字打印为`sumtotal - sum`。

*   **实现**：

    ## C++ 

    ```

    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to get the missing number 
    int getMissingNo(int a[], int n) 
    { 

        int total = (n + 1) * (n + 2) / 2; 
        for (int i = 0; i < n; i++) 
            total -= a[i]; 
        return total; 
    } 

    // Driver Code 
    int main() 
    { 
        int arr[] = { 1, 2, 4, 5, 6 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        int miss = getMissingNo(arr, n); 
        cout << miss; 
    } 

    ```

    ## C

    ```

    #include <stdio.h> 

    /* getMissingNo takes array and size of array as arguments*/
    int getMissingNo(int a[], int n) 
    { 
        int i, total; 
        total = (n + 1) * (n + 2) / 2; 
        for (i = 0; i < n; i++) 
            total -= a[i]; 
        return total; 
    } 

    /*program to test above function */
    int main() 
    { 
        int a[] = { 1, 2, 4, 5, 6 }; 
        int miss = getMissingNo(a, 5); 
        printf("%d", miss); 
        getchar(); 
    } 

    ```

    ## Java

    ```

    // Java program to find missing Number 

    class Main { 
        // Function to ind missing number 
        static int getMissingNo(int a[], int n) 
        { 
            int i, total; 
            total = (n + 1) * (n + 2) / 2; 
            for (i = 0; i < n; i++) 
                total -= a[i]; 
            return total; 
        } 

        /* program to test above function */
        public static void main(String args[]) 
        { 
            int a[] = { 1, 2, 4, 5, 6 }; 
            int miss = getMissingNo(a, 5); 
            System.out.println(miss); 
        } 
    } 

    ```

    ## Python

    ```

    # getMissingNo takes list as argument 
    def getMissingNo(A): 
        n = len(A) 
        total = (n + 1)*(n + 2)/2
        sum_of_A = sum(A) 
        return total - sum_of_A 

    # Driver program to test the above function 
    A = [1, 2, 4, 5, 6] 
    miss = getMissingNo(A) 
    print(miss) 
    # This code is contributed by Pratik Chhajer 

    ```

    ## C# 

    ```

    // C# program to find missing Number 
    using System; 

    class GFG { 
        // Function to ind missing number 
        static int getMissingNo(int[] a, int n) 
        { 
            int total = (n + 1) * (n + 2) / 2; 

            for (int i = 0; i < n; i++) 
                total -= a[i]; 

            return total; 
        } 

        /* program to test above function */
        public static void Main() 
        { 
            int[] a = { 1, 2, 4, 5, 6 }; 
            int miss = getMissingNo(a, 5); 
            Console.Write(miss); 
        } 
    } 

    // This code is contributed by Sam007_ 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find 
    // the Missing Number 

    // getMissingNo takes array and 
    // size of array as arguments 
    function getMissingNo ($a, $n) 
    { 
        $total = ($n + 1) * ($n + 2) / 2;  
        for ( $i = 0; $i < $n; $i++) 
            $total -= $a[$i]; 
        return $total; 
    } 

    // Driver Code 
    $a = array(1, 2, 4, 5, 6); 
    $miss = getMissingNo($a, 5); 
    echo($miss); 

    // This code is contributed by Ajit. 
    ?> 

    ```

    **输出**：

    ```
    3
    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        仅需要遍历数组。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间。

**为溢出修改**：

*   **方法**：方法保持不变，但是如果`n`大，则可能会溢出。 为了避免整数溢出，请从已知数字中选择一个数字，然后从给定数字中减去一个数字。 这样一来，就不会有整数溢出。

*   **算法**：

    1.  创建一个变量`sum = 1`，该变量将存储缺少的数字，并创建一个计数器`c = 2`。

    2.  从头到尾遍历数组。

    3.  将`sum`的值更新为`sum = sum – array[i] + c`，将`x`更新为`c++`。

    4.  将缺少的数字打印为`sum`。

*   **实现**：

    ## C++ 

    ```

    #include <bits/stdc++.h> 
    using namespace std; 

    // a represents the array 
    // n : Number of elements in array a 
    int getMissingNo(int a[], int n)  
    {  
        int i, total=1;  

        for ( i = 2; i<= (n+1); i++) 
        { 
            total+=i; 
            total -= a[i-2]; 
        } 
        return total;  
    }  

    //Driver Program 
    int main() { 
        int arr[] = {1, 2, 3, 5}; 
        cout<<getMissingNo(arr,sizeof(arr)/sizeof(arr[0])); 
        return 0; 
    } 

    //This code is contributed by Ankur Goel 

    ```

    ## Java

    ```

    // Java implementation  
    class GFG 
    { 

        // a represents the array 
        // n : Number of elements in array a 
        static int getMissingNo(int a[], int n)  
        { 
            int total = 1; 
            for (int i = 2; i <= (n + 1); i++) 
            { 
                total += i; 
                total -= a[i - 2]; 
            } 
            return total; 
        } 

        // Driver Code 
        public static void main(String[] args) 
        { 
            int[] arr = { 1, 2, 3, 5 }; 
            System.out.println(getMissingNo(arr, arr.length)); 
        } 
    } 

    // This post is contributed  
    // by Vivek Kumar Singh 

    ```

    ## Python3

    ```

    # a represents the array 
    # n : Number of elements in array a 
    def getMissingNo(a, n):  
        i, total = 0, 1

        for i in range(2, n + 2): 
            total += i 
            total -= a[i - 2] 
        return total 

    # Driver Code 
    arr = [1, 2, 3, 5] 
    print(getMissingNo(arr, len(arr))) 

    # This code is contributed by Mohit kumar 

    ```

    ## C# 

    ```

    using System; 

    class GFG 
    { 

    // a represents the array 
    // n : Number of elements in array a 
    static int getMissingNo(int[] a, int n)  
    {  
        int i, total = 1;  

        for ( i = 2; i <= (n + 1); i++) 
        { 
            total += i; 
            total -= a[i - 2]; 
        } 
        return total;  
    }  

    // Driver Code 
    public static void Main()  
    { 
        int[] arr = {1, 2, 3, 5}; 
        Console.Write(getMissingNo(arr, (arr.Length))); 

        // Console.Write(getMissingNo(arr, 4)); 
    } 
    } 
    // This code is contributed by SoumikMondal 

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        仅需要遍历数组。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间。

**感谢 Sahil Rally 提出的改进建议。**

**方法 2**：此方法使用 XOR 技术解决问题。

*   **方法**：

    XOR 具有一定特性：

    *   假设`a1 ^ a2 ^ a3 ^…^ an = a`和`a1 ^ a2 ^ a3 ^…^ an-1 = b`

    *   然后`a ^ b = an`

    使用此属性，可以找到丢失的元素。 计算从 1 到`n`的所有自然数的 XOR，并将其存储为`a`。 现在，计算该数组所有元素的 XOR 并将其存储为`b`。 缺少的数字将是`a ^ b`。

    `^`是 XOR 运算符。

*   **算法**：

    1.  创建两个变量`a = 0`和`b = 0`。

    2.  以`i`为计数器从 1 到`n`循环运行。

    3.  对于每个索引更新为`a = a ^ i`。

    4.  现在，从头到尾遍历数组。

    5.  对于每个索引更新`b`，作为`b = b ^ array[i]`。

    6.  将缺少的数字打印为`a ^ b`。

*   **实现**：

    ## C++ 

    ```

    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to get the missing number 
    int getMissingNo(int a[], int n) 
    { 
        // For xor of all the elements in array 
        int x1 = a[0]; 

        // For xor of all the elements from 1 to n+1 
        int x2 = 1; 

        for (int i = 1; i < n; i++) 
            x1 = x1 ^ a[i]; 

        for (int i = 2; i <= n + 1; i++) 
            x2 = x2 ^ i; 

        return (x1 ^ x2); 
    } 

    // Driver Code 
    int main() 
    { 
        int arr[] = { 1, 2, 4, 5, 6 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        int miss = getMissingNo(arr, n); 
        cout << miss; 
    } 

    ```

    ## C

    ```

    #include <stdio.h> 

    /* getMissingNo takes array and size of array as arguments*/
    int getMissingNo(int a[], int n) 
    { 
        int i; 
        int x1 = a[0]; /* For xor of all the elements in array */
        int x2 = 1; /* For xor of all the elements from 1 to n+1 */

        for (i = 1; i < n; i++) 
            x1 = x1 ^ a[i]; 

        for (i = 2; i <= n + 1; i++) 
            x2 = x2 ^ i; 

        return (x1 ^ x2); 
    } 

    /*program to test above function */
    int main() 
    { 
        int a[] = { 1, 2, 4, 5, 6 }; 
        int miss = getMissingNo(a, 5); 
        printf("%d", miss); 
        getchar(); 
    } 

    ```

    ## Java

    ```

    // Java program to find missing Number 
    // using xor 
    class Main { 
        // Function to find missing number 
        static int getMissingNo(int a[], int n) 
        { 
            int x1 = a[0]; 
            int x2 = 1; 

            /* For xor of all the elements  
               in array */
            for (int i = 1; i < n; i++) 
                x1 = x1 ^ a[i]; 

            /* For xor of all the elements  
               from 1 to n+1 */
            for (int i = 2; i <= n + 1; i++) 
                x2 = x2 ^ i; 

            return (x1 ^ x2); 
        } 

        /* program to test above function */
        public static void main(String args[]) 
        { 
            int a[] = { 1, 2, 4, 5, 6 }; 
            int miss = getMissingNo(a, 5); 
            System.out.println(miss); 
        } 
    } 

    ```

    ## Python3

    ```

    # Python3 program to find 
    # the mising Number 
    # getMissingNo takes list as argument  

    def getMissingNo(a, n): 
        x1 = a[0] 
        x2 = 1

        for i in range(1, n): 
            x1 = x1 ^ a[i] 

        for i in range(2, n + 2): 
            x2 = x2 ^ i 

        return x1 ^ x2 

    # Driver program to test above function 
    if __name__=='__main__': 

        a = [1, 2, 4, 5, 6] 
        n = len(a) 
        miss = getMissingNo(a, n)  
        print(miss) 

    # This code is contributed by Yatin Gupta  

    ```

    ## C# 

    ```

    // C# program to find missing Number 
    // using xor 
    using System; 

    class GFG { 
        // Function to find missing number 
        static int getMissingNo(int[] a, int n) 
        { 
            int x1 = a[0]; 
            int x2 = 1; 

            /* For xor of all the elements  
            in array */
            for (int i = 1; i < n; i++) 
                x1 = x1 ^ a[i]; 

            /* For xor of all the elements  
            from 1 to n+1 */
            for (int i = 2; i <= n + 1; i++) 
                x2 = x2 ^ i; 

            return (x1 ^ x2); 
        } 

        /* driver program to test above function */
        public static void Main() 
        { 
            int[] a = { 1, 2, 4, 5, 6 }; 
            int miss = getMissingNo(a, 5); 
            Console.Write(miss); 
        } 
    } 

    // This code is contributed by Sam007_ 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find 
    // the Misiing Number 
    // getMissingNo takes array and  
    // size of array as arguments 
    function getMissingNo($a, $n) 
    { 
        // For xor of all the 
        // elements in array  
        $x1 = $a[0];  

        // For xor of all the  
        // elements from 1 to n + 1 
        $x2 = 1;  

        for ($i = 1; $i < $n; $i++) 
            $x1 = $x1 ^ $a[$i]; 

        for ($i = 2; $i <= $n + 1; $i++) 
            $x2 = $x2 ^ $i;      

        return ($x1 ^ $x2); 
    } 

    // Driver Code 
    $a = array(1, 2, 4, 5, 6); 
    $miss = getMissingNo($a, 5); 
    echo($miss); 

    // This code is contributed by Ajit. 
    ?> 

    ```

    **输出**：

    ```
    3
    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        仅需要遍历数组。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间。

