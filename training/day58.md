# 😵‍💫 day58

## 代码随想录算法训练营第五十八天| 动态规划 背包01 416

### 01 背包理论基础

文章讲解：[https://programmercarl.com/%E8%83%8C%E5%8C%85%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%8001%E8%83%8C%E5%8C%85-1.html](https://programmercarl.com/%E8%83%8C%E5%8C%85%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%8001%E8%83%8C%E5%8C%85-1.html)

视频讲解：[https://www.bilibili.com/video/BV1cg411g7Y6/](https://www.bilibili.com/video/BV1cg411g7Y6/)

**二维 dp 数组**

**1. 确定 dp 数组以及下标的含义**

`dp[i][j]`：从下标为 \[0 - i] 的物品里任意取，放进容量为 j 的背包中，价值总和的最大值为 `dp[i][j]`

**2. 确定递推公式**

具体的过程可以看上面的文章讲解，这里不再赘述，

* **不放物品 i**：由 `dp[i - 1][j]` 推出，即背包容量为 j，里面不放物品 i 的最大价值，此时 `dp[i][j]` 就是 `dp[i - 1][j]`
* **放物品 i**：由 `dp[i - 1][j - weight[i]]` 推出，`dp[i - 1][j - weight[i]]` 为背包容量为 `j - weight[i]` 的时候不放物品 i 的最大价值， 那么 `dp[i - 1][j - weight[i]] + value[i]`，就是背包放物品 i 得到的最大价值

递归公式： `dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i])`

**3. dp 数组初始化**

* 背包容量为 0 时，总和一定都是 0
* 只放物品 0 的时，背包容量超过物品 0 重量后，总和都是物品 0 的价值

**降维成一维 dp 数组**

**为什么可以降维以及如何降维**

首先，我们要知道二维数组 `dp[i][j]` 里面存储的是将物品 \[0,i] 放入容量为j的背包能获得的最大价值， 那么最后一个元素 `dp[m][n]` 表示的就是将物品 \[0,m] 放入容量为 n 的背包能获得的最大价值。

其次，再说一下 `dp[i][j]` 的更新，`dp[i][j]` 更新有两种情况:

* 不把物品 i 放入背包，`dp[i][j] = dp[i - 1][j]`
  * 由于背包 j 容量有限小于物品i的体积(可以剪枝的部分)或者放入物品i不划算，此时将物品 \[0,i-1] 放入容量为 j 的背包能获得的最大价值 与将物品 \[0,i] 放入容量为j的背包能获得的最大价值相等
* 把物品 i 放入背包，此时需要考虑给物品 i 预留足够的容量 `[j-weight[i]]`
  * 因为是在 \[0,i-1] 的基础上放入物品 i，所以 `dp[i][j] = dp[i-1][j-weight[i]]+value[i]`

经过观察可以发现，`dp[i][j]` 的更新只与 `dp[i - 1]` 的状态有关，我们关联到二维的表格中，只与上一行有关

那么我们可以像斐波那契数列那样优化，只保留两行就够了，每一次根据第一行来更新第二行的信息，然后再把第二行替换为第一行，这样就降维成一维

**1. 确定 dp 数组以及下标的含义**

`dp[j]`：容量为 j 的背包中，价值总和的最大值为 `dp[j]`

**2. 确定递推公式**

根据上面所说的降维的方式，将 dp\[i - 1] 直接覆盖在 dp\[i] 上，原先的二维递推公式就可以变成

`dp[i][j] = max(dp[i][j], dp[i][j - weight[i]] + value[i])`

然后再降维就可以得到，

`dp[j] = max(dp[j], dp[j - weight[i]] + value[i])`

举例说明一下，

针对于物品 1，`dp[1][j] = max(dp[0][j], dp[0][j-weight[1]]+value[1])`

`dp[1][j]` 的更新只与 `dp[0][j]` 和 `dp[0][j-weight[1]]+value[1]` **左上角**这两个数据有关，**而与右边的数据无关**

也就是说递推公式中，

* 等号右边的 dp\[j] 表示的是上一行的数据，也对应着没有放入当前物品的情况，那么直接将上一行的数据复制下来
* 等号左边的 dp\[j] 表示的是当前行的数据

那么从右向左遍历，遍历时左边的数据还是上一行的数据没有更新；

反之，如果正序遍历，那么一定是左边的数据先更新，此时就直接将上一行的数据覆盖掉了；同时也会出现一个物品被多次放入的情况

**3. dp 数组初始化**

背包容量为 0 时，总和一定都是 0

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day58/01\_bag.go)

### 416 分割等和子集

题目链接：[https://leetcode.cn/problems/partition-equal-subset-sum/](https://leetcode.cn/problems/partition-equal-subset-sum/)

文章讲解：[https://programmercarl.com/0416.%E5%88%86%E5%89%B2%E7%AD%89%E5%92%8C%E5%AD%90%E9%9B%86.html](https://programmercarl.com/0416.%E5%88%86%E5%89%B2%E7%AD%89%E5%92%8C%E5%AD%90%E9%9B%86.html)

视频讲解：[https://www.bilibili.com/video/BV1rt4y1N7jE/](https://www.bilibili.com/video/BV1rt4y1N7jE/)

**思路**

哪怕是知道这道题是要使用 01背包问题的方式来解决，结果想了半天都没想通到底怎么套上来

下面来总结一下，

* 背包的体积为sum / 2
* 背包要放入的商品（集合里的元素）重量为 元素的数值，价值也为元素的数值
* 背包如果正好装满，说明找到了总和为 sum / 2 的子集。
* 背包中每一个元素是不可重复放入。

**1. 确定 dp 数组以及下标的含义**

套到本题来看，

`dp[j]`：容量为 j 的背包中，价值总和的最大值为 `dp[j]`

当 `dp[target] == target`，背包就装满了，target 为背包的容量

**2. 确定递推公式**

`dp[j] = max(dp[j], dp[j - nums[i]] + nums[i])`

**3. dp 数组初始化**

如题意可得，dp\[0] = 0

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day58/0416\_partition\_equal\_subset\_sum.go.go)
