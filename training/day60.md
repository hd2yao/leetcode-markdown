# 🥳 day60

## 代码随想录算法训练营第六十天| 动态规划 494 474

### 494 目标和

题目链接：[https://leetcode.cn/problems/target-sum/](https://leetcode.cn/problems/target-sum/)

文章讲解：[https://programmercarl.com/0494.%E7%9B%AE%E6%A0%87%E5%92%8C.html](https://programmercarl.com/0494.%E7%9B%AE%E6%A0%87%E5%92%8C.html)

视频讲解：[https://www.bilibili.com/video/BV1o8411j73x/](https://www.bilibili.com/video/BV1o8411j73x/)

**思路**

我结合上面一题的经验，很容易把这道题也转化到 01背包问题上来了，下面是转化的思路

* 可以拆解为两部分，`P` 和 `N`，其中 `P` 中的元素是加号前面的数，`N` 是减号前面的数
* 我们要求 `P - N = target`，可以转换为 `P = (target + sum(nums)) / 2`； 如果 `(target + sum(nums))` 是奇数或者 P 小于 0，则无法找到满足条件的组合
* 转化为在 nums 中找到和为 p 的子集个数

> 因为 sum 和 target 都是固定的，所以找到一个 P，那么就对应找到一个 N，因此不用再去考虑 N 了
>
> 这道题也可以用回溯法

**错误的做法**

在转化到 01背包上后，我的想法是像前面几题一样，构造 dp\[i]\[j]，然后去统计 dp\[i]\[target] = target 的个数

最后的结果就是：加法的个数 \* 减法的个数

**错误的原因**

为什么不能像上面一样做？

我们又要回到动态规划的核心上：dp 的含义到底是什么

如果像之前一样，dp\[i]\[j] 含义是：容量为 j 最大的价值是 dp\[i]\[j]，

即，如果 dp\[i]\[target] = target 也只能说明：容量为 target 是可以达到价值为 target；

但是不能说明有几种组合可以达到 target！

所以上面的思路是不正确的！

**正确的思路**

还是从二维开始，然后降维到一维

此时，`dp[i][j]` 含义：`[0,i]` 中的元素任意选取的总和达到 `j` 共有 `dp[i][j]` 种方式

`dp[i][j]` 有两种来源：

* 不选取 `nums[i]`，那么此时的方式就是 `dp[i - 1][j]`
* 选取 `nums[i]`，那么此时的方式就是 `dp[i - 1][j - nums[i]]`

因此递推公式为，

`dp[i][j] = dp[i-1][j] + dp[i-1][j-nums[i]]`

下面来说一下初始化，也是困扰了我很久的一点，

这道题有个大坑就是，元素值是可以为 0 的，所以在初始化的时候就需要注意

我们的 j 是从 0 开始的，根据定义我们知道此时，总和为 0 可以选择的情况是 dp\[0]\[0]，

* 如果 nums\[0] != 0，毫无疑问 dp\[0]\[0] = 1 也就是只有一种情况，不选择 nums\[0];
* 可是如果 nums\[0] = 0 时，此时无论是否选择 nums\[0] 总和都还是 0，那么此时 dp\[0]\[0] = 2！

这就是跟前面几道题不一样的地方，针对这一点我给出了两种方法，一种就是代码中

```go
if i == 0 {
    if nums[i] == 0 {
        dp[i][j] = 1
    }
    if nums[i] == j {
        dp[i][j]++
    }
}
```

跟之前一样单独考虑第一行，即初始化的情况，

* 先将 dp\[0]\[0] 初始化为 1，可以理解为不选取 nums\[0] 的情况
* 然后第二步就是选取 nums\[0] 的情况，而这里使用 `dp[i][j]++` 就是考虑到 nums\[0] = 0 的情况

第二种方法，思想有点儿像链表中的虚拟头节点一样，先给出代码

```go
dp := make([][]int, len(nums)+1)
for i := 0; i < len(dp); i++ {
    dp[i] = make([]int, target+1)
}

dp[0][0] = 1
for i := 1; i <= len(nums); i++ {
    for j := 0; j <= target; j++ {
        if j >= nums[i-1] {
            dp[i][j] = dp[i-1][j] + dp[i-1][j-nums[i-1]]
        } else {
            dp[i][j] = dp[i-1][j]
        }
    }
}
```

这样写是因为，`dp[i][j]` 的含义为：使用前 i 个元素，能够凑出和为 j 的组合数； 其中 i 表示前 i 个元素，即 nums\[0], nums\[1], ..., nums\[i-1]

那么这样情况下，`dp[0][j]` 表示在不使用任何元素的情况下，能否凑出和为 j 的组合数，这是一个特别的边界情况：

* `dp[0][0] = 1` 表示不选择任何元素时，和为 0 的情况有且只有一种（即空集）
* 对于 j > 0 的情况，由于不选择任何元素，显然无法凑出和为 j，所以 `dp[0][j]` 对于 j > 0 应该为 0

因为，后面的代码都一致了，是不是很像虚拟头节点的使用！

**降维成一维**

在理解了二维之后，我们根据前面降维的思想，也可以直接降维，

`dp[j] = dp[j] + dp[j-nums[i]]` 也就是 `dp[j] += dp[j-nums[i]]`

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day60/0494\_target\_sum.go)

### 474 一和零

题目链接：[https://leetcode.cn/problems/ones-and-zeroes/](https://leetcode.cn/problems/ones-and-zeroes/)

文章讲解：[https://programmercarl.com/0474.%E4%B8%80%E5%92%8C%E9%9B%B6.html](https://programmercarl.com/0474.%E4%B8%80%E5%92%8C%E9%9B%B6.html)

视频讲解：[https://www.bilibili.com/video/BV1rW4y1x7ZQ/](https://www.bilibili.com/video/BV1rW4y1x7ZQ/)

**思路**

这道题其实是一个三维的 dp，因为 weight 在本题中是两个维度 m 和 n

那么降维一下就是 `dp[i][j]`: 最多有 i 个 0 和 j 个 1 的 strs 的最大子集的大小为 `dp[i][j]`

把这个当成一维去做，只要想明白这一点就很简单了

> 如果是三维的话，第一层就是 strs\[i] 了，每一层都是一张 m \* n 的表
>
> `dp[i][j][k] = max(dp[i-1][j][k], dp[i-1][j-zero][k-one]+1)`

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day60/0474\_ones\_and\_zeroes.go)
