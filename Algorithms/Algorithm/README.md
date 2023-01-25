## ⚡️ 算法

### 排序

排序算法 | 平均时间复杂度 | 最差时间复杂度 | 空间复杂度 | 数据对象稳定性
---|---|---|---|---
[冒泡排序](BubbleSort.h) | O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(1)|稳定
[选择排序](SelectionSort.h) | O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(1)|数组不稳定、链表稳定
[插入排序](InsertSort.h) | O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(1)|稳定
[快速排序](QuickSort.h) | O(n*log<sub>2</sub>n) |  O(n<sup>2</sup>) | O(log<sub>2</sub>n) | 不稳定
[堆排序](HeapSort.cpp) | O(n*log<sub>2</sub>n)|O(n*log<sub>2</sub>n)|O(1)|不稳定
[归并排序](MergeSort.h) | O(n*log<sub>2</sub>n) | O(n*log<sub>2</sub>n)|O(n)|稳定
[希尔排序](ShellSort.h) | O(n*log<sup>2</sup>n)|O(n<sup>2</sup>)|O(1)|不稳定
[计数排序](CountSort.cpp) | O(n+m)|O(n+m)|O(n+m)|稳定
[桶排序](BucketSort.cpp) | O(n)|O(n)|O(m)|稳定
[基数排序](RadixSort.h) | O(k*n)|O(n<sup>2</sup>)| |稳定

> * 均按从小到大排列
> * k：代表数值中的 “数位” 个数
> * n：代表数据规模
> * m：代表数据的最大值减最小值
> * 来自：[wikipedia . 排序算法](https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)

### 查找

查找算法 | 平均时间复杂度 | 空间复杂度 | 查找条件
---|---|---|---
[顺序查找](SequentialSearch.h) | O(n) | O(1) | 无序或有序
[二分查找（折半查找）](BinarySearch.h) | O(log<sub>2</sub>n)| O(1) | 有序
[插值查找](InsertionSearch.h) | O(log<sub>2</sub>(log<sub>2</sub>n)) | O(1) | 有序
[斐波那契查找](FibonacciSearch.cpp) | O(log<sub>2</sub>n) | O(1) | 有序
[哈希查找](DataStructure/HashTable.cpp) | O(1) | O(n) | 无序或有序
[二叉查找树（二叉搜索树查找）](BSTSearch.h) |O(log<sub>2</sub>n) |   | 
[红黑树](DataStructure/RedBlackTree.cpp) |O(log<sub>2</sub>n) | |
2-3树 | O(log<sub>2</sub>n - log<sub>3</sub>n) |   | 
B树/B+树 |O(log<sub>2</sub>n) |   | 

### 图搜索算法

图搜索算法 |数据结构| 遍历时间复杂度 | 空间复杂度
---|---|---|---
[BFS广度优先搜索](https://zh.wikipedia.org/wiki/%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)|邻接矩阵<br/>邻接链表|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)
[DFS深度优先搜索](https://zh.wikipedia.org/wiki/%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)|邻接矩阵<br/>邻接链表|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)

### 其他算法

算法 |思想| 应用
---|---|---
[分治法](https://zh.wikipedia.org/wiki/%E5%88%86%E6%B2%BB%E6%B3%95)|把一个复杂的问题分成两个或更多的相同或相似的子问题，直到最后子问题可以简单的直接求解，原问题的解即子问题的解的合并|[循环赛日程安排问题](https://github.com/huihut/interview/tree/master/Problems/RoundRobinProblem)、排序算法（快速排序、归并排序）
[动态规划](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)|通过把原问题分解为相对简单的子问题的方式求解复杂问题的方法，适用于有重叠子问题和最优子结构性质的问题|[背包问题](https://github.com/huihut/interview/tree/master/Problems/KnapsackProblem)、斐波那契数列
[贪心法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E6%B3%95)|一种在每一步选择中都采取在当前状态下最好或最优（即最有利）的选择，从而希望导致结果是最好或最优的算法|旅行推销员问题（最短路径问题）、最小生成树、哈夫曼编码
