# 😎 day71

## 代码随想录算法训练营第七十一天| 动态规划 309 714

### 309 买卖股票的最佳时机含冷冻期

题目链接：[https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

文章讲解：[https://programmercarl.com/0309.%E6%9C%80%E4%BD%B3%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E6%97%B6%E6%9C%BA%E5%90%AB%E5%86%B7%E5%86%BB%E6%9C%9F.html](https://programmercarl.com/0309.%E6%9C%80%E4%BD%B3%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E6%97%B6%E6%9C%BA%E5%90%AB%E5%86%B7%E5%86%BB%E6%9C%9F.html)

视频讲解：[https://www.bilibili.com/video/BV1rP4y1D7ku](https://www.bilibili.com/video/BV1rP4y1D7ku)

**思路**

同样的，本题也是对每一天的状态进行情况考虑，不过因为有了冷冻期并且只有一天，所以在未持有的状态上会有不同，因此，

* 0：当天为冷冻期
* 1：当天持有股票
* 2：当天卖出股票
* 3：未持有股票且已度过冷冻期（至少前一天是冷冻期）

当所有情况都以罗列之后，递推公式就可以根据不同的状态写出 `dp[i][j]`，

* `dp[i][0]`：今天为冷冻期，说明前一天刚卖出股票，即 `dp[i-1][2]`
* `dp[i][1]`：今天持有股票，可以是前一天已经持有股票；可以是前一天是冷冻期，今天买入；可以是前一天未持有股票且不是冷冻期，今天买入
* `dp[i][2]`：今天卖出股票，说明前一天是持有股票的
* `dp[i][3]`：可以是前一天为冷冻期，`dp[i-1][0]`；也可以是冷冻期在更早之前 `dp[i-1][3]`

将状态分成四种情况再状态转移写递推公式时非常的清晰

我一开始是按照三种情况来写的，

* 0：冷冻期
* 1：持有股票
* 2：未持有股票

持有股票很容易写出，而冷冻期和未持有股票的状态却不好写，因为未持有的状态中又会包含冷冻期的状态

这也提醒了我，这种情况下说明我们细分的状态不合适，需要重新分类或者继续拆分！

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day71/0309\_best\_time\_to\_buy\_and\_sell\_stock\_with\_cooldown.go)

### 714 买卖股票的最佳时机含手续费

题目链接：[https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

文章讲解：[https://programmercarl.com/0714.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BA%E5%90%AB%E6%89%8B%E7%BB%AD%E8%B4%B9%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html](https://programmercarl.com/0714.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BA%E5%90%AB%E6%89%8B%E7%BB%AD%E8%B4%B9%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html)

视频讲解：[https://www.bilibili.com/video/BV1z44y1Z7UR](https://www.bilibili.com/video/BV1z44y1Z7UR)

**思路**

这道题需要注意的一点就是一笔交易只计算一次手续费，那么要么是在买入时计算，那么是在卖出时计算

如果是在买入时计算的话，在初始化也记得要先减去哦！

切不可多次计算！

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day71/0714\_best\_time\_to\_buy\_and\_sell\_stock\_with\_transaction\_fee.go)
