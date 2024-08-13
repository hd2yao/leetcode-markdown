# 😥 day22

## 代码随想录算法训练营第二十二天| 二叉树 144 145 94

文章讲解：[https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html)

视频讲解：[https://www.bilibili.com/video/BV1Wh411S7xt](https://www.bilibili.com/video/BV1Wh411S7xt)

### 144 二叉树的前序遍历

题目链接：[https://leetcode.cn/problems/binary-tree-preorder-traversal/](https://leetcode.cn/problems/binary-tree-preorder-traversal/)

### 94 二叉树的中序遍历

题目链接：[https://leetcode.cn/problems/binary-tree-inorder-traversal/](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

### 145 二叉树的后续遍历

题目链接：[https://leetcode.cn/problems/binary-tree-postorder-traversal/](https://leetcode.cn/problems/binary-tree-postorder-traversal/)

***

#### 思路

**递归法**

二叉树的遍历，还是很容易用递归的方法写出来的，可能唯一需要注意的点，就是需要传入 `*[]int`

在整个递归过程中，数组始终都是同一个，因此需要传入指针来确保，然后在 append 操作时，又用到了昨天切片的一个知识点，这里再复习一下

```go
*val = append(*val, treeNode.Val)
```

需要对指针切片先 **解引用 `*val`**
