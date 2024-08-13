# 😮 day30

## 代码随想录算法训练营第三十天| 二叉树 513 112 113

### 513 找树左下角的值

题目链接：[https://leetcode.cn/problems/find-bottom-left-tree-value/](https://leetcode.cn/problems/find-bottom-left-tree-value/)

文章讲解：[https://programmercarl.com/0513.%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.html](https://programmercarl.com/0513.%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.html)

视频讲解：[https://www.bilibili.com/video/BV1424y1Z7pn](https://www.bilibili.com/video/BV1424y1Z7pn)

**思路**

这道题虽然难度为中等，但做起来反而比前两天简单的题还容易

直接使用层序遍历，最后将最后一行的第一个值返回即可

改进：

这里可以不保存全部的值，可以只记录每一层的第一个节点的值，这样可以减少内存使用

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day30/0513\_find\_bottom\_left\_tree\_value.go)

### 112 路径总和

题目链接：[https://leetcode.cn/problems/path-sum/](https://leetcode.cn/problems/path-sum/)

文章讲解：[https://programmercarl.com/0112.%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C.html](https://programmercarl.com/0112.%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C.html)

视频讲解：[https://www.bilibili.com/video/BV19t4y1L7CR](https://www.bilibili.com/video/BV19t4y1L7CR)

**思路**

这道题跟二叉树的全部路径类似，都是需要从根节点开始到叶子节点，只是这道题只需要找到有一条符合条件的路径就可以返回

因此，需要在左右子树中加入判断，这也是我一开始都没有想明白的地方

```go
if treeNode.Left != nil {
    if pathSum(treeNode.Left, sum) {
        return true
    }
}

if treeNode.Right != nil {
    if pathSum(treeNode.Right, sum) {
        return true
    }
}
```

开始的时候我一直在想，不是已经在叶子节点处进行了判断嘛，为什么还需要在这里加一层判断，直到我手动模拟了一遍流程

因为叶子节点处的判断只能针对当前叶子节点返回一个 bool 值，但是并不能直接返回到上一层节点

因为每一递归都是一层判断，如果当前路径一共包含四个节点，我们需要在第一个节点（根节点）得到结果，也即在第一层判断，但是叶子节点处的判断是在第四层， 索引需要对根据下层的结果得到上一层的结果

所以，上面代码中的判断就是为了将结果一层一层返回到顶层

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day30/0112\_path\_sum.go)

### 113 路径总和2

题目链接：[https://leetcode.cn/problems/path-sum-ii/](https://leetcode.cn/problems/path-sum-ii/)

文章讲解：[https://programmercarl.com/0112.%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C.html](https://programmercarl.com/0112.%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C.html)

视频讲解：[https://www.bilibili.com/video/BV19t4y1L7CR](https://www.bilibili.com/video/BV19t4y1L7CR)

**思路**

这道题也跟二叉树的全部路径类似，这道题也需要遍历全部的路径，只不过保存的直接是值，因此在代码层面有两点需要注意的：

**1. 路径副本放入结果集**

当我们找到一条符合的路径后，需要放入结果集，注意不能直接 append，代码如下：

```go
*result = append(*result, *path)
```

\*path 是节点的切片，是一个引用类型，如果像上面一样直接存入 result 中，后续对 \*path 中值的修改都是直接影响到 result

因此，我们需要先创建一个副本，将副本放入结果集中，

```go
pathCopy := make([]int, len(*path))
copy(pathCopy, *path)
*result = append(*result, pathCopy)
```

**2. 移除节点**

在每一轮递归结果后（到叶子节点为一轮），需要主动移除当前叶子节点（回溯）

这是因为 path 是全局共享的，而不像一般参数传入调用后，自动回溯

```go
*path = (*path)[:len(*path)-1]
```

同时，在叶子节点中，不能像往常一样加 return，不然无法执行上面的代码

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day30/0112\_path\_sum\_ii.go)
