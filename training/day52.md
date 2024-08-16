# 😮‍💨 day52

## 代码随想录算法训练营第五十二天| 贪心法 738 968

### 738 单调递增的数字

题目链接：[https://leetcode.cn/problems/monotone-increasing-digits/](https://leetcode.cn/problems/monotone-increasing-digits/)

文章讲解：[https://programmercarl.com/0738.%E5%8D%95%E8%B0%83%E9%80%92%E5%A2%9E%E7%9A%84%E6%95%B0%E5%AD%97.html](https://programmercarl.com/0738.%E5%8D%95%E8%B0%83%E9%80%92%E5%A2%9E%E7%9A%84%E6%95%B0%E5%AD%97.html)

视频讲解：[https://www.bilibili.com/video/BV1Kv4y1x7tP](https://www.bilibili.com/video/BV1Kv4y1x7tP)

**思路**

这道题理解题意之后模拟一下过程就很容易想到从后往前来遍历了

需要提醒的点就是，如果去写出代码

* 将数字转为字符串，方便使用下标
* 将字符串转为 byte 数组，方便修改

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day52/0738\_monotone\_increasing\_digits.go)

### 968 监控二叉树

题目链接：[https://leetcode.cn/problems/binary-tree-cameras/](https://leetcode.cn/problems/binary-tree-cameras/)

文章讲解：[https://programmercarl.com/0968.%E7%9B%91%E6%8E%A7%E4%BA%8C%E5%8F%89%E6%A0%91.html](https://programmercarl.com/0968.%E7%9B%91%E6%8E%A7%E4%BA%8C%E5%8F%89%E6%A0%91.html)

视频讲解：[https://www.bilibili.com/video/BV1SA411U75i](https://www.bilibili.com/video/BV1SA411U75i)

**思路**

我一开始的思路大致方向是没有错的，只是没有统一，所以想的过程很复杂，不够清楚，导致写出来的代码不能把全部的情况都考虑进去

下面来说一下：

* 0：节点无覆盖
* 1：节点有摄像头
* 2：节点有覆盖

如果传入的是空节点，则认为是 2 有覆盖

而放置摄像头的节点规则是：

* 从下往上遍历，则使用后续遍历
* 叶子节点不放摄像头
* 相隔两个节点放一个摄像头，需要单独考虑根节点

根据上面的情况，我们可以写出递归三部曲：

**1.递归参数和返回值**

因为我们是使用闭包，所以不必将 count 作为参数传入，如果是单独的函数，需要使用 \*int

我们需要根据左右孩子的状态来判定当前节点的状态，因此需要一个 mark 返回值

**2.终止条件**

遍历到叶子节点就返回

```go
if treeNode == nil {
    return 2
}
```

**3.单层递归逻辑**

从下至上遍历，因此我们要使用后序遍历，根据左右子节点的状态来判定当前节点的状态

```go
leftMark := postorder(treeNode.Left, count)
rightMark := postorder(treeNode.Right, count)
```

* 叶子节点

```go
if leftMark == 2 && rightMark == 2 {
    return 0
}
```

* 非叶子节点

非叶子节点的话，还有很多种情况，如果一一去考虑容易出错不全，我写的时候就是这样

因此，我们可以直接根据节点状态来判断

节点状态为 0，说明节点无覆盖，我们可以认为是叶子节点，那就在它的父节点放置摄像头

节点状态为 1，说明在当前节点放置了摄像头，那它的父节点就是有覆盖的状态

节点状态为 2，说明当前节点处于有覆盖状态，不需要操作

```go
if leftMark == 0 || rightMark == 0 {
    return 1
}
```

其他都都是覆盖的状态

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day52/0968\_binary\_tree\_cameras.go)
