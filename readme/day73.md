# 😬 day73

## 代码随想录算法训练营第七十三天| 动态规划 1143 1035 53

### 1143 最长公共子序列

题目链接：[https://leetcode.cn/problems/longest-common-subsequence/](https://leetcode.cn/problems/longest-common-subsequence/)

文章讲解：[https://programmercarl.com/1143.%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E5%BA%8F%E5%88%97.html](https://programmercarl.com/1143.%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E5%BA%8F%E5%88%97.html)

视频讲解：[https://www.bilibili.com/video/BV1ye4y1L7CQ](https://www.bilibili.com/video/BV1ye4y1L7CQ)

**思路**

`dp[i][j]` ：以下标 `i - 1` 为结尾的 nums1，和以下标 `j - 1` 为结尾的 nums2，最长公共子序列长度为 `dp[i][j]`

跟 **718 最长重复子数组** 思路一致

这里有一点要注意，本题 i 和 j 的定义要理解！

不同的是，本题不要求连续，因此在 text1\[i - 1] 与 text2\[j - 1] 不相同时，还需要向前去看最大值

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day73/1143\_longest\_common\_subsequence.go)

### 1035 不相交的线

题目链接：[https://leetcode.cn/problems/uncrossed-lines/](https://leetcode.cn/problems/uncrossed-lines/)

文章讲解：[https://programmercarl.com/1035.%E4%B8%8D%E7%9B%B8%E4%BA%A4%E7%9A%84%E7%BA%BF.html](https://programmercarl.com/1035.%E4%B8%8D%E7%9B%B8%E4%BA%A4%E7%9A%84%E7%BA%BF.html)

视频讲解：[https://www.bilibili.com/video/BV1h84y1x7MP](https://www.bilibili.com/video/BV1h84y1x7MP)

**思路**

换汤不换药 还是求最长公共子序列！

手动画一下图就知道了，然后看一下连线的数值就能清晰的知道了

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day73/1035\_uncrossed\_lines.go)

### 53 最大子数组和

题目链接：[https://leetcode.cn/problems/maximum-subarray/](https://leetcode.cn/problems/maximum-subarray/)

文章讲解：[https://programmercarl.com/0053.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html](https://programmercarl.com/0053.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89.html)

视频讲解：[https://www.bilibili.com/video/BV19V4y1F7b5](https://www.bilibili.com/video/BV19V4y1F7b5)

**思路**

本题在之前的贪心法中做过一次

使用动态规划也是比较简单的

不过这里还有有一些小坑：初始化，

* dp\[0] 的初始化应该是 nums\[0] 而不是 0
* 最大值的初始化也应该是 nums\[0] 而不是 0

原因就在于，如果一个数组全是负数，这样一个例子就可以明白了吧

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day73/0053\_maximum\_subarray.go)
