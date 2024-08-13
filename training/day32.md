# 🥵 day32

## 代码随想录算法训练营第三十二天| 二叉树 530 501

### 530 二叉搜索树的最小绝对差

题目链接：[https://leetcode.cn/problems/minimum-absolute-difference-in-bst/](https://leetcode.cn/problems/minimum-absolute-difference-in-bst/)

文章讲解：[https://programmercarl.com/0530.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E7%BB%9D%E5%AF%B9%E5%B7%AE.html](https://programmercarl.com/0530.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E7%BB%9D%E5%AF%B9%E5%B7%AE.html)

视频讲解：[https://www.bilibili.com/video/BV1DD4y11779](https://www.bilibili.com/video/BV1DD4y11779)

**思路**

二叉搜索树的中序遍历可以得到一个递增的有序数组，这一点要记住

因为，求任意两个节点值的最小值，只需要一次比较数组中相邻两个值即可，因为数组是递增的，nums\[2] - nums\[0] 一定是大于 nums\[1] - nums\[0]

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day32/0530\_minimum\_absolute\_difference\_in\_bst.go)

### 501 二叉搜索树中的众数

题目链接：[https://leetcode.cn/problems/find-mode-in-binary-search-tree/](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)

文章讲解：[https://programmercarl.com/0501.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E4%BC%97%E6%95%B0.html](https://programmercarl.com/0501.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E4%BC%97%E6%95%B0.html)

视频讲解：[https://www.bilibili.com/video/BV1fD4y117gp](https://www.bilibili.com/video/BV1fD4y117gp)

**思路**

**统计全部众数**

首先，如果是普通的二叉树，我们要先遍历这棵树，然后对数组求众数

* 遍历时可以使用 map，然后利用 sort 接口特性，对 map 进行排序，得出众数
* 也可以直接将全部的值放入数组中，先对数组进行排序
  * 遍历两遍：第一遍计算 maxCount；第二遍根据 maxCount 得出相应的值
  * 遍历一遍：这就是重点要说明的地方

如果是二叉搜索树，可以直接使用中序遍历就得到一个有序数组

下面就重点说一下对有序数组统计众数的过程：

这里我们需要两个变量，一个是 count 用来统计数值的个数，一个是 maxCount 用来统计当前可能为众数的最大个数

因为数组是有序的，所以我们只需依次遍历，统计每个数值的个数 count，并与 maxCount 比较：

* count < maxCount，说明当前数值不可能为众数
* count == maxCount，说明当前数值是目前遍历结果中的众数之一，需要保存
* count > maxCount，说明当前数值是新的众数，之前统计的众数都不再是众数，清空之前保存的全部众数，记录当前数值并更新 maxCount

**1. 中序遍历数组**

首先还是用中序遍历得到有序数组，下面就变成了统计一个有序数组中的全部众数

下面是我在写代码中，遇到的一些问题点，记录一下：

```go
for i := 1; i < len(nums); i++ {
    for (判断条件) {
        // ...
        i++
    }
}
```

在上面的代码中，内部的 i++ 执行后，外层的 i++ 是否还会触发执行？

> 在 Go 语言中，for 循环中内层 for 循环结束后，跳回到外层 for 循环时，不会自动触发外层 for 循环的 i++ 操作。 内层循环中的 i++ 操作已经修改了 i 的值，因此当内层循环结束并返回到外层循环时，外层循环的 i++ 操作会被跳过， 不会再次执行。Go 语言不会重置或忽略 i 在循环体内的修改。

> 在 Go 语言中，如果你在内层 for 循环中对 i 进行了 i++ 操作后又进行了 i-- 操作， 那么当内层 for 循环结束并返回到外层 for 循环时，外层 for 循环仍会执行它的增量操作 i++。

> 具体来说，内层循环中对 i 的任何修改都将在内层循环结束后反映在外层循环中。 因此，如果你在内层循环中执行了 i++，然后又执行了 i--，那么 i 的值就恢复到内层循环之前的状态。 当控制流返回到外层循环时，外层循环的增量操作 i++ 将正常执行。

代码中给出了我原始的统计，以及后续简化后的代码

**2. 中序遍历直接在树上比较**

因为二叉搜索树的中序遍历时有序的，因此我们一样依次比较当前节点与前一个节点的值

这个过程就和遍历有序数组时，依次比较相邻两个数值是相同的

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day32/0501\_find\_mode\_in\_binary\_search\_tree.go)
