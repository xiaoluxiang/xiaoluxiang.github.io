# 树

## 二分查找树

> 遍历，查找，插入，删除
>

遍历，查找特定值，查找最值，查找前驱或后继节点（转换成子树的最值查询），插入，删除

## AVL树

> 重难点在于插入或者删除后的LL，LR，RL，RR的再平衡。

定义：AVL是高度平衡的二叉树，任何节点的左右子树高度差距最大是2

插入调整：对于插入后，直的就将挂载多的提成根节点。如果非直，则按照所在左右阵营调整成直的，然后阵营内提成根节点

## 红黑树

> [参考地址](https://blog.csdn.net/tanrui519521/article/details/80980135)

**定义：**一个节点要么为红色，要么为黑色。根节点为黑色。红色节点的子节点不允许为红色。任何一条路径上的黑色个数相等（红色作为间隔色，最大存在2倍的路径）

**更新操作：**默认插入红色，如果其父节点为黑色，则OK，如果为红，先搞直自己，如果Uncle为黑，则通过调整旋转。Uncle为红通过向上变色传递

## Huffman树



# 图

## 深度优先遍历

1: 数据结构

## 广度优先遍

## 最小生成树

> 图是由顶点和路径组成的。所以在将图转为树的过程切入点可为顶点或者路径

### prime算法（P，顶点）

### Kruskal算法（路径）

## 单源最短路径

>  Dijkstra & Frolyd，[参考博客地址：https://www.cnblogs.com/lisen10/p/10876132.html](https://www.cnblogs.com/lisen10/p/10876132.html)

Dijkstra，维护一张起点到各个点的最短距离，直到扩展到终点o（n2）

Frolyd，基于邻接矩阵，逐个将所有的点纳入中介点，进行更新最短距离，然后读矩阵即可获得 o（n3）

# 排序

> 排序是主要分为四大类：选择类，插入类，交换类，其他类
>
> 选择最大/最小的值并入有序队列，拿一个插入到有序队列，在待排中互相交换直到有序。

![img](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/alg-sort-overview-1.png)

## 冒泡排序

排序原理

选取最值数字不断上浮。

时间复杂度

排序稳定性

## 快速排序

通过预取定的中间数X，完成二分。难点在于理解所有指针移动交换，最终左右指针合并落中间数X

## 插入排序

通过不断将单个数插入有序集中，完成排序

## 希尔排序

> 对于希尔排序，个人的看法是为了解决直接插入排序中，潜在的大量移动做优化，即通过gap长度设定，进行预插入进而实现对数组的初步有序化。下一次gap长度每次应该是取log，最小为1，退化成直接插入

## 选择排序

在未排序中选择极值与第一个未排序的进行交换。同数组中，不稳定

堆排序

这种排序方法有点意思，根据数组作为二叉树的映射关系，自底向上进行获得最大堆。然后交换最值，然后自顶向下调整最大堆。