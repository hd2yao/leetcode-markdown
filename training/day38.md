# 🫤 day38

## 代码随想录算法训练营第三十八天| 回溯法 39 40 131

### 39 组合总和

题目链接：[https://leetcode.cn/problems/combination-sum/](https://leetcode.cn/problems/combination-sum/)

文章讲解：[https://programmercarl.com/0039.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.html](https://programmercarl.com/0039.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.html)

视频讲解：[https://www.bilibili.com/video/BV1KT4y1M7HJ](https://www.bilibili.com/video/BV1KT4y1M7HJ)

**思路**

这道题的关键就是要想清楚如何像昨天的题目一样构造一棵树，并确定每层节点的候选值

因为题目说数组的元素可以重复，我一开始也没有思路，后面我根据下面图中的树完成了代码

<div align="left">

<figure><img src="../.gitbook/assets/day38-1.png" alt=""><figcaption></figcaption></figure>

</div>

* 递归参数和返回值

依旧是 candidates、target、sum

因为选取的值会随着节点取值变化，所以还是需要 startIndex 来控制可选择的数值

* 递归终止条件

```go
if sum == target {
    tmp := make([]int, len(combinationNums))
    copy(tmp, combinationNums)
    result = append(result, tmp)
    return
}
if sum > target {
    return
}
```

* 单层递归逻辑

这里的关键就是确定 startIndex

因为本题数值可以重复，也就是说当前节点选择的值，递归后在下一层节点还是可以选择，因此 `startIndex = i`

也可以像我给出的代码，

```go
backtracking(candidates[i:], sum+candidates[i], target)
```

**剪枝**

上面的代码是在节点加入后再判断总和是否大于 target，那我们可以在节点加入前先进行判断

也就是在 for 中判断，如果下一层的节点加入后 sum > target，可以直接结束当前值的操作

```go
if sum+candidates[i] > target {
    continue
}
```

我们还可以先对数组进行排序，从小到大，如果当前的 sum > target，那么可以直接不用判断下一层的全部节点

```go
if sum+candidates[i] > target {
    break
}
```

第一种剪枝只能 continue 是因为不确定下一个节点的值的大小

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day38/0039\_combination\_sum.go)

### 40 组合总和2

题目链接：[https://leetcode.cn/problems/combination-sum-ii/](https://leetcode.cn/problems/combination-sum-ii/)

文章讲解：[https://programmercarl.com/0040.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CII.html](https://programmercarl.com/0040.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CII.html)

视频讲解：[https://www.bilibili.com/video/BV12V4y1V73A](https://www.bilibili.com/video/BV12V4y1V73A)

**思路**

这道题又有了一些不同，数组里的数值有重复

所以在处理去重的逻辑上跟 [三数之和](https://github.com/hd2yao/leetcode/tree/master/training/day9/0015\_3sum.go) 是一致的

所以我选用这种方法而没有使用讲解中的 used 数组

> 代码中注释部分也是一种方法

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day38/0040\_combination\_sum\_ii.go)

### 131 分割回文串

题目链接：[https://leetcode.cn/problems/palindrome-partitioning/](https://leetcode.cn/problems/palindrome-partitioning/)

文章讲解：[https://programmercarl.com/0131.%E5%88%86%E5%89%B2%E5%9B%9E%E6%96%87%E4%B8%B2.html](https://programmercarl.com/0131.%E5%88%86%E5%89%B2%E5%9B%9E%E6%96%87%E4%B8%B2.html)

视频讲解：[https://www.bilibili.com/video/BV1c54y1e7k6](https://www.bilibili.com/video/BV1c54y1e7k6)

**思路**

谁能想到切割的问题也可以使用回溯法

不过在知道这一点后，代码也就比较容易写出来了

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day38/0131\_palindrome\_partitioning.go)
