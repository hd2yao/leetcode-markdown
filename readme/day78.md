# 🤐 day78

## 代码随想录算法训练营第七十八天| 动态规划 647 516

### 647 回文子串

题目链接：[https://leetcode.cn/problems/palindromic-substrings/](https://leetcode.cn/problems/palindromic-substrings/)

文章讲解：[https://programmercarl.com/0647.%E5%9B%9E%E6%96%87%E5%AD%90%E4%B8%B2.html](https://programmercarl.com/0647.%E5%9B%9E%E6%96%87%E5%AD%90%E4%B8%B2.html)

视频讲解：[https://www.bilibili.com/video/BV17G4y1y7z9/](https://www.bilibili.com/video/BV17G4y1y7z9/)

**思路**

按照以往的动态规划的思路，题目要求什么，我们的 dp 数组就设定为什么

但是本题不太一样，如果直接将 dp\[i] 定义为 下标 i 之前的子串的回文个数为 dp\[i]

那么在进行推导的时候，我们只能判断出 s\[0] 和 s\[i] 是否相等，即子串的两头，但无法判断子串中间是否为回文

因此，我们重新定义 dp，

`dp[i][j]`：索引 `i` 到 `j` 的子串 `s[i:j+1]` 是否是回文子串

接下来，我们看一下状态转移：

* 如果 `s[i] == s[j]`，且 `j-i <= 1`（即子串长度为 1 或 2），则 `dp[i][j] = true`
* 如果 `s[i] == s[j]` 且 `dp[i+1][j-1]` 为 true（即去掉首尾字符的子串也是回文），则 `dp[i][j] = true`

因为我们 dp 并不是计数，所以每次 `dp[i][j] = true` 时，我们计数加一

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day78/0647\_palindromic\_substrings.go)

### 516 最长回文子序列

题目链接：[https://leetcode.cn/problems/longest-palindromic-subsequence/](https://leetcode.cn/problems/longest-palindromic-subsequence/)

文章讲解：[https://programmercarl.com/0516.%E6%9C%80%E9%95%BF%E5%9B%9E%E6%96%87%E5%AD%90%E5%BA%8F%E5%88%97.html](https://programmercarl.com/0516.%E6%9C%80%E9%95%BF%E5%9B%9E%E6%96%87%E5%AD%90%E5%BA%8F%E5%88%97.html)

视频讲解：[https://www.bilibili.com/video/BV1d8411K7W6/](https://www.bilibili.com/video/BV1d8411K7W6/)

**思路**

我们定义一个二维数组 `dp[i][j]`，表示字符串 `s` 从索引 `i` 到 `j` 的子序列的最长回文子序列的长度

状态转移方程：

* 如果 `s[i] == s[j]`，那么 `dp[i][j] = dp[i+1][j-1] + 2`
  * 因为如果两个字符相等，它们可以构成回文的两端
* 如果 `s[i] != s[j]`，那么 `dp[i][j] = max(dp[i+1][j], dp[i][j-1])`
  * 这是因为如果这两个字符不相等，那么我们只能分别去掉 `s[i]` 或 `s[j]`，取这两种情况中的最大值

初始状态，对于所有的单个字符，`dp[i][i] = 1`，因为任何一个字符都是回文子序列

我们需要从短的子串开始，逐步扩展到更长的子串，以确保计算 `dp[i][j]` 时，`dp[i+1][j-1]` 已经计算出来

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day78/0516\_longest\_palindromic\_subsequence.go)
