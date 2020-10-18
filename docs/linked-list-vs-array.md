# 链表与数组

> 原文： [https://www.geeksforgeeks.org/linked-list-vs-array/](https://www.geeksforgeeks.org/linked-list-vs-array/)

[数组](https://www.geeksforgeeks.org/array-data-structure/)和[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)都可以用于存储相似类型的线性数据，但是它们相互之间都有一些优点和缺点。

![](img/f135b70319b69f7c8fc3364f232504ba.png)

![](img/f3277ee37f20568b18a51cd230eb1fa6.png)

数组和链表之间的主要区别：

1.  数组是包含相似类型的数据元素的集合的数据结构，而链表被视为非原始数据结构，它包含称为节点的无序链接元素的集合。

2.  在数组中，元素属于索引，即，如果要进入第四个元素，则必须编写变量名称及其索引或在方括号内的位置。

3.  但是，在链表中，您必须从头开始并逐步进行，直到到达第四个元素。

4.  访问数组中的元素速度很快，而“链表”需要线性时间，因此访问速度要慢得多。

5.  诸如在数组中插入和删除之类的操作会花费大量时间。 另一方面，链表中这些操作的执行速度很快。

6.  数组的大小固定。 相反，链表是动态且灵活的，并且可以扩展和缩小其大小。

7.  在数组中，内存是在编译时分配的，而在链表中，内存是在执行或运行时分配的。

9.  元素连续存储在数组中，而元素则随机存储在链表中。

10.  由于实际数据存储在数组的索引内，因此对内存的需求减少了。 相反，由于存储了额外的下一个和上一个引用元素，因此需要在链表中有更多的存储空间。

11.  此外，数组中的内存利用率低下。 相反，在链表中内存利用率很高。

以下是支持链表的要点。

1.  数组的大小是固定的：因此，我们必须提前知道元素数量的上限。 而且，通常，所分配的存储器与用途无关地等于上限，并且在实际使用中，很少达到上限。

2.  在元素数组中插入新元素非常昂贵，因为必须为新元素创建一个空间，并且为创建空间而必须移动现有元素。

例如，假设我们在数组`id[]`中维护 ID 的排序列表。

```
id[] = [1000, 1010, 1050, 2000, 2040, …]
```

如果要插入新的 ID 1005，则要维持排序顺序，我们必须将所有元素都移到 1000（不包括 1000）之后。

除非使用某些特殊技术，否则删除数组也很昂贵。 例如，要删除`id[]`中的 1010，必须移动 1010 之后的所有内容。

因此，链表相对于数组具有以下两个优点：1）动态大小，2）易于插入/删除。

链表具有以下缺点：

1.  不允许随机访问。 我们必须从第一个节点开始顺序访问元素。 因此，我们无法使用链表进行二分搜索。

2.  列表的每个元素都需要用于指针的额外存储空间。

3.  数组具有更好的缓存局部性，可以在性能上产生很大的不同。

参考：

[http://cslibrary.stanford.edu/103/LinkedListBasics.pdf](http://cslibrary.stanford.edu/103/LinkedListBasics.pdf)
