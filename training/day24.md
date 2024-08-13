# 😫 day24

## 代码随想录算法训练营第二十四天| 二叉树 226 101

### 226 翻转二叉树

题目链接：[https://leetcode.cn/problems/invert-binary-tree/](https://leetcode.cn/problems/invert-binary-tree/)

文章讲解：[https://programmercarl.com/0226.%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.html](https://programmercarl.com/0226.%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.html)

视频讲解：[https://www.bilibili.com/video/BV1sP4y1f7q7](https://www.bilibili.com/video/BV1sP4y1f7q7)

**思路**

这道题还是比较简单的，就是从上至下，交换左右孩子节点，那么就很容易想到用递归的方法

还有一点需要补充的，递归的前序遍历和后序遍历都没有问题，而中序遍历需要注意的

```go
invert(treeNode.Left)
treeNode.Left, treeNode.Right = treeNode.Right, treeNode.Left
invert(treeNode.Left)
```

1. 先翻转左子树
2. 交换左右子树
3. 再翻转左子树

也就是说，两次翻转子树中间先进行了一次交换，因此原先没有翻转的右子树在步骤 2 后交换到新的左子树上

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day24/0226\_invert\_binary\_tree.go)

### 101 对称二叉树

题目链接：[https://leetcode.cn/problems/symmetric-tree/](https://leetcode.cn/problems/symmetric-tree/)

文章讲解：[https://programmercarl.com/0101.%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.html](https://programmercarl.com/0101.%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.html)

视频讲解：[https://www.bilibili.com/video/BV1ue4y1Y7Mf](https://www.bilibili.com/video/BV1ue4y1Y7Mf)

**思路**

我开始的思路就是，如果是一棵对称二叉树，那么它一定和翻转之后相同

这样的话就和上面 翻转二叉树 结合到一起了

* 翻转二叉树
* 比较两棵树是否相同

在比较的过程中，遇到了不少问题：

首先，我选择用层序遍历得出两棵树的结果，以此来比较是否相同，但是会出现一个问题，无法确定各个节点的位置，也就是说 只能确定存在这些节点的值，但是不能确定这些节点是否应该在相同的位置

然后，我选择使用中序遍历的方法去得出结果，这个方法确实可以将节点的位置区分出来，但是也有一个问题，就是保存的是节点的值， 那么当全部节点的值都相同时，也就无计可施了

最后，只能求助于讲解了

使用两个指针，去一次比较对应节点是否相同

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day24/0101\_symmetric\_tree.go)
