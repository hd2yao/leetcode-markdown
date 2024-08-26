# 😒 day70

## 代码随想录算法训练营第七十天| 动态规划 123 188

### 123 买卖股票的最佳时机3

题目链接：[https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

文章讲解：[https://programmercarl.com/0123.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIII.html](https://programmercarl.com/0123.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIII.html)

视频讲解：[https://www.bilibili.com/video/BV1WG411K7AR](https://www.bilibili.com/video/BV1WG411K7AR)

**思路**

我是先尝试使用贪心法，但是多次尝试之后发现并不能全部覆盖可能性

这是因为，

* 贪心算法是局部最优的策略，但无法确保全局最优
  * 在两次交易的场景下，某一天的局部最优可能会干扰另一笔交易的全局最优；例如，贪心算法可能会因为在某个局部最优点卖出了股票，而错失了更优的后续交易机会
  * 而在不限制交易次数的场景下，可以再每次股价上涨时卖出，不需要考虑交易之间的顺序问题；而问题的目标就变成了尽可能多地利用每一个局部的价格上涨区间

这里有一个例子，`prices = [1,2,4,2,5,7,2,4,9,0]`，我们分别看一下不限制交易次数和在两次交易内的情况，

我们还是先求出每天的利润数组 `profit = [1 2 -2 3 2 -5 2 5 -9]`

首先看一下不限制交易次数，我们只需要选择利润为正的全局情况即可，`max = 1 + 2 + 3 + 2 + 2 + 5 = 15`

再看一下如果限制两次之内，我们应该选择利润最高的两次交易，那么我们可以根据利润数组将其中连续正数的情况视为一次， 那么第一次应该是 `[3 2]` 第二次应该是 `[2 5]` 结果是 12

可结果应该是第一次选择 `[1 2 -2 3 2]` 第二次选择 `[2 5]` max = 13

看到了嘛，如果要使用贪心去做，我们无法保证当前选择就是局部最优，因为有可能后面会出现更大的结果

这样反而就与贪心的想法不同了

因此，还是选择使用动态规划的方法去做

这里贴一下上面的贪心的代码，当然是不对的，不过还是记录一下

```go
func maxProfit(prices []int) int {
	if len(prices) == 1 {
		return 0
	}

    // 计算每日利润
	profit := make([]int, 0)
	for i := 1; i < len(prices); i++ {
		profit = append(profit, prices[i]-prices[i-1])
	}

	result := make([]int, 0)
	index := -1
    
    // 重新计算得到连续的正利润
	for i := 0; i < len(profit); i++ {
		if profit[i] < 0 {
			result = append(result, 0)
			index++
		} else if i == 0 {
			result = append(result, profit[i])
			index++
		} else {
			result[index] += profit[i]
		}
	}
	sort.Ints(result)

	if len(result) == 1 {
		return result[0]
	}
	return result[len(result)-1] + result[len(result)-2]
}
```

**动态规划**

每一天都有四种状态：

1. 第一次持有股票
2. 第一次不持有股票
3. 第二次持有股票
4. 第二次不持有股票

那么，`dp[i][j]`：表示在第 i 天在状态 j 下的最大现金为 `dp[i][j]`

这样就比较容易写出递推公式了，具体可看代码

我这里想说一下初始化，`dp[0][3] = - prices[0]`

我们可以理解为，在第 0 天买入又卖出，然后再次买入

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day70/0123\_best\_time\_to\_buy\_and\_sell\_stock\_iii.go)

### 188 买卖股票的最佳时机4

题目链接：[https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)

文章讲解：[https://programmercarl.com/0188.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIV.html](https://programmercarl.com/0188.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIV.html)

视频讲解：[https://www.bilibili.com/video/BV16M411U7XJ](https://www.bilibili.com/video/BV16M411U7XJ)

**思路**

本题在上一题的基础上，增加状态 j 即可，

当 j 为奇数是就是买入，j 为偶数是就是卖出

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day70/0188\_best\_time\_to\_buy\_and\_sell\_stock\_iv.go)
