# 😫 day15

## 代码随想录算法训练营第十五天| 栈与队列 20 1047 150

### 20 有效的括号

题目链接：[https://leetcode.cn/problems/valid-parentheses/](https://leetcode.cn/problems/valid-parentheses/)

文章讲解：[https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html](https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html)

视频讲解：[https://www.bilibili.com/video/BV1AF411w78g](https://www.bilibili.com/video/BV1AF411w78g)

**思路**

这道题还是很简单的，只需要把各种不符合的情况全部罗列清楚，然后用代码写出来就可以了

* 左括号可以直接入栈
* 右括号需要依次匹配才可以进行下一步

在上面的过程中，还会出现 '(((\[{' 全是左括号 以及 ')\['、'()]\[' 打头是右括号的情况，这些情况未必可以在第一次写的时候都能够考虑到

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day15/0020\_valid\_parentheses.go)

## 1047 删除字符串中的所有相邻重复项

题目链接：[https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)

文章讲解：[https://programmercarl.com/1047.%E5%88%A0%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E7%9B%B8%E9%82%BB%E9%87%8D%E5%A4%8D%E9%A1%B9.html](https://programmercarl.com/1047.%E5%88%A0%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E7%9B%B8%E9%82%BB%E9%87%8D%E5%A4%8D%E9%A1%B9.html)

视频讲解：[https://www.bilibili.com/video/BV12a411P7mw](https://www.bilibili.com/video/BV12a411P7mw)

**思路**

同样是使用栈来实现，也是很简单的一道题，就是在代码上有些需要注意的点

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day15/1047\_remove\_all\_adjacent\_duplicates\_in\_string.go)

### 150 逆波兰表达式求值

题目链接：[https://leetcode.cn/problems/evaluate-reverse-polish-notation/](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)

文章讲解：[https://programmercarl.com/0150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.html](https://programmercarl.com/0150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.html)

视频讲解：[https://www.bilibili.com/video/BV1kd4y1o7on](https://www.bilibili.com/video/BV1kd4y1o7on)

**思路**

这道题思想也很类似的，模拟一下这个求值的过程，哪怕不知道 逆波兰表达式 是什么，也应该知道这就是后缀表达式

那么依旧是使用栈，

* 数字直接入栈
* 遇到运算符，就 pop 两个数字 进行运算，然后结果重新入栈

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day15/0150\_evaluate\_reverse\_polish\_notation.go)
