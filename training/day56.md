# 😬 day56

## 代码随想录算法训练营第五十六天| 动态规划 62 63

### 62 不同路径

题目链接：[https://leetcode.cn/problems/unique-paths/](https://leetcode.cn/problems/unique-paths/)

文章讲解：[https://programmercarl.com/0062.%E4%B8%8D%E5%90%8C%E8%B7%AF%E5%BE%84.html](https://programmercarl.com/0062.%E4%B8%8D%E5%90%8C%E8%B7%AF%E5%BE%84.html)

视频讲解：[https://www.bilibili.com/video/BV1ve4y1x7Eu/](https://www.bilibili.com/video/BV1ve4y1x7Eu/)

**思路**

动态规划的题最好还是先动手模拟一遍，这样会比较清楚从上一步是如何过渡到下一步的，有助于得出 dp 的推导公式

同时也要敢于大胆尝试不同的 dp\[i] 的定义，在试错中找到正确的答案

这道题，

**1. 确定 dp 数组以及下标的含义**

`dp[i][j]`： 表示到达第 i 行第 j 列共有 `dp[i][j]` 方法

**2. 确定递推公式**

根据题意，只能向下或向右移动一步，因此

`dp[i][j]` 可以有两个方向推出来：

* `dp[i - 1][j]`，第 i-1 行第 j 列，有 `dp[i - 1][j]` 种方法，再向下走一步就是 `dp[i][j]` 了
* `dp[i][j - 1]`，第 i 行第 j-1 列，有 `dp[i][j - 1]` 种方法，再向右走一步就是 `dp[i][j]` 了

所以 `dp[i][j] = dp[i - 1][j] + dp[i][j - 1]` !

**3. dp 数组初始化**

因为只能向下或向右，因此第 0 行的格子只能由左边的格子移动到，

同样第 0 列的格子只能由上边的格子移动到，

而我们初始从第 0 行第 0 列出发，认为只有一种情况，即 `dp[i][j] = 1`

则 `dp[0][j] = 1` `dp[i][0] = 1`

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day56/0062\_unique\_paths.go)

### 63 不同路径2

题目链接：[https://leetcode.cn/problems/unique-paths-ii/](https://leetcode.cn/problems/unique-paths-ii/)

文章讲解：[https://programmercarl.com/0063.%E4%B8%8D%E5%90%8C%E8%B7%AF%E5%BE%84II.html](https://programmercarl.com/0063.%E4%B8%8D%E5%90%8C%E8%B7%AF%E5%BE%84II.html)

视频讲解：[https://www.bilibili.com/video/BV1Ld4y1k7c6/](https://www.bilibili.com/video/BV1Ld4y1k7c6/)

**思路**

这道题跟上面一样，就是多了障碍物的一些判断，

当遇到障碍物，`dp[i][j] = 0` 结合 dp 数组的含义，因为当前位置有障碍物，所以无法到达该位置，所以值为 0

这里想说明一下，可以先对第 0 行和第 0 列做赋值操作，这样可以用上剪枝

即，当在第 0 行或第 0 列中遇到障碍物，后面的位置也无需判断，因为一定到达不了

```go
// 初始化, 如果是障碍物, 后面的就都是0, 不用循环了
for i := 0; i < m && obstacleGrid[i][0] == 0; i++ {
    dp[i][0] = 1
}
for i := 0; i < n && obstacleGrid[0][i] == 0; i++ {
    dp[0][i] = 1
}
```

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day56/0063\_unique\_paths\_ii.go)
