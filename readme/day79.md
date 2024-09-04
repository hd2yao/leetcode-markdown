# ☺️ day79

## 代码随想录算法训练营第七十九天| 单调栈 739 496 503

### 739 每日温度

题目链接：[https://leetcode.cn/problems/daily-temperatures/](https://leetcode.cn/problems/daily-temperatures/)

文章讲解：[https://programmercarl.com/0739.%E6%AF%8F%E6%97%A5%E6%B8%A9%E5%BA%A6.html](https://programmercarl.com/0739.%E6%AF%8F%E6%97%A5%E6%B8%A9%E5%BA%A6.html)

视频讲解：[https://www.bilibili.com/video/BV1my4y1Z7jj/](https://www.bilibili.com/video/BV1my4y1Z7jj/)

**思路**

本题开始我们学习最后一个篇章 —— 单调栈

通常是一维数组，要寻找任意元素的右边或者左边第一个比自己大或者小的元素的位置

单调栈的本质是空间换时间，因为在遍历的过程中需要用一个栈来记录右边第一个比当前元素高的元素，优点是整个数组只需要遍历一次

更直白来说，就是用一个栈来记录我们遍历过的元素

我们想一下暴力法，两层 for 循环，第一层用来记录当前的元素，第二层来找符合题意的元素

而使用栈，我们就可以代替第一层 for，将遍历的元素直接存入栈中，而单调栈法中的循环跟暴力法中的第二层 for 的作用是一致的

这么解释应该就比较清晰了！

那么本题，我们要找右边第一个比当前元素大的位置

单调栈中就存放元素的下标即可，

* 元素小于等于栈顶元素，入栈
* 元素大于栈顶元素，说明找了第一个大的元素，计算下标差值，然后先出栈再将新元素入栈

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day79/0739\_daily\_temperatures.go)

### 496 下一个更大元素1

题目链接：[https://leetcode.cn/problems/next-greater-element-i/](https://leetcode.cn/problems/next-greater-element-i/)

文章讲解：[https://programmercarl.com/0496.%E4%B8%8B%E4%B8%80%E4%B8%AA%E6%9B%B4%E5%A4%A7%E5%85%83%E7%B4%A0I.html](https://programmercarl.com/0496.%E4%B8%8B%E4%B8%80%E4%B8%AA%E6%9B%B4%E5%A4%A7%E5%85%83%E7%B4%A0I.html)

视频讲解：[https://www.bilibili.com/video/BV1jA411m7dX/](https://www.bilibili.com/video/BV1jA411m7dX/)

**思路**

本题的思路跟上一题类似，

* 先对 nums2 使用单调栈计算结果
  * 这里使用 map 来替代 slice，因为数组中的元素不会重复
* 然后遍历 nums1 在 map 中去寻找结果
  * 可以理解成按照 nums1 中的顺序对 map 的结果进行部分排序

这样，本题的整体过程就出来了

还有一点需要注意的是，上一题要我们求位置，本题要求数字，要懂得转换

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day79/0496\_next\_qreater\_element\_i.go)

### 503 下一个更大的元素2

题目链接：[https://leetcode.cn/problems/next-greater-element-ii/](https://leetcode.cn/problems/next-greater-element-ii/)

文章讲解：[https://programmercarl.com/0503.%E4%B8%8B%E4%B8%80%E4%B8%AA%E6%9B%B4%E5%A4%A7%E5%85%83%E7%B4%A0II.html](https://programmercarl.com/0503.%E4%B8%8B%E4%B8%80%E4%B8%AA%E6%9B%B4%E5%A4%A7%E5%85%83%E7%B4%A0II.html)

视频讲解：https://www.bilibili.com/video/BV15y4y1o7Dw/[https://www.bilibili.com/video/BV15y4y1o7Dw/](https://www.bilibili.com/video/BV15y4y1o7Dw/)

**思路**

比较简单的想法是，把两个 nums 拼接到一起，然后使用单调栈去做，最后只取前半部分即可

那么更精简的做法就是，不拼接扩容，只是在遍历的时候模拟走两遍，如下

```go
for i := 0; i < len(nums)*2; i++ {
  for len(stack) != 0 && nums[stack[len(stack)-1]] < nums[i%len(nums)] {
    index := stack[len(stack)-1]
    answer[index] = nums[i%len(nums)]
    stack = stack[:len(stack)-1]
  }
  stack = append(stack, i%len(nums))
}
```

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day79/0503\_next\_qreater\_element\_ii.go)
