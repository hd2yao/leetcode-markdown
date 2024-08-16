# 🥱 day59

## 代码随想录算法训练营第五十九天| 动态规划 1049

### 1049 最后一块石头的重量2

题目链接：[https://leetcode.cn/problems/last-stone-weight-ii/](https://leetcode.cn/problems/last-stone-weight-ii/)

文章讲解：[https://programmercarl.com/1049.%E6%9C%80%E5%90%8E%E4%B8%80%E5%9D%97%E7%9F%B3%E5%A4%B4%E7%9A%84%E9%87%8D%E9%87%8FII.html](https://programmercarl.com/1049.%E6%9C%80%E5%90%8E%E4%B8%80%E5%9D%97%E7%9F%B3%E5%A4%B4%E7%9A%84%E9%87%8D%E9%87%8FII.html)

视频讲解：[https://www.bilibili.com/video/BV14M411C7oV/](https://www.bilibili.com/video/BV14M411C7oV/)

**思路**

01背包的应用场景的关键就是，如何将题目转化为 01背包，只要这个想明白，代码就可以直接套用

那么这道题，我一开始就在想怎么去两两选取：差值最小的先、最大最小的先，但是都没有得到统一的方法，

那么应该怎么去思考呢？

上面的想法可以说是贪心的思想，每一步都在找局部最优已达到全部最优，但是结果证明这样都是不通过，也就是说都是反例，说明了不适合用贪心

实际上，我们不用两两去考虑，直接考虑整体：**尽量让石头分成重量相同的两堆，相撞之后剩下的石头最小**

这样的话就跟昨天的题目一样了，分割等和子集

不过不太一样的是，今天的结果可能未必 `dp[target] == target`

**1. 确定 dp 数组以及下标的含义**

套到本题来看，

`dp[j]`：容量为 j 的背包中，价值总和的最大值为 `dp[j]`

当 `dp[target] == target`，背包就装满了，target 为背包的容量

**2. 确定递推公式**

`dp[j] = max(dp[j], dp[j - nums[i]] + nums[i])`

**3. dp 数组初始化**

如题意可得，dp\[0] = 0

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day59/1049\_last\_stone\_weight\_ii.go)
