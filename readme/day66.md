# 🥴 day66

## 代码随想录算法训练营第六十六天| 动态规划 198 213 337

### 198 打家劫舍

题目链接：[https://leetcode.cn/problems/house-robber/](https://leetcode.cn/problems/house-robber/)

文章讲解：[https://programmercarl.com/0198.%E6%89%93%E5%AE%B6%E5%8A%AB%E8%88%8D.html](https://programmercarl.com/0198.%E6%89%93%E5%AE%B6%E5%8A%AB%E8%88%8D.html)

视频讲解：[https://www.bilibili.com/video/BV1Te411N7SX](https://www.bilibili.com/video/BV1Te411N7SX)

**思路**

这道理很简单，不再过多讲解了

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day66/0198\_house\_robber.go)

### 213 打家劫舍 II

题目链接：[https://leetcode.cn/problems/house-robber-ii/](https://leetcode.cn/problems/house-robber-ii/)

文章讲解：[https://programmercarl.com/0213.%E6%89%93%E5%AE%B6%E5%8A%AB%E8%88%8DII.html](https://programmercarl.com/0213.%E6%89%93%E5%AE%B6%E5%8A%AB%E8%88%8DII.html)

视频讲解：[https://www.bilibili.com/video/BV1oM411B7xq](https://www.bilibili.com/video/BV1oM411B7xq)

**思路**

这里可以分情况讨论，

* 考虑包含头元素，不包含尾元素
* 考虑包含尾元素，不包含头元素

这样就将环形结构转换成了两个线性结构，就回到了上面一题

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day66/0213\_house\_robber\_ii.go)

### 337 打家劫舍3

题目链接：[https://leetcode.cn/problems/house-robber-iii/](https://leetcode.cn/problems/house-robber-iii/)

文章讲解：[https://programmercarl.com/0337.%E6%89%93%E5%AE%B6%E5%8A%AB%E8%88%8DIII.html](https://programmercarl.com/0337.%E6%89%93%E5%AE%B6%E5%8A%AB%E8%88%8DIII.html)

视频讲解：[https://www.bilibili.com/video/BV1H24y1Q7sY](https://www.bilibili.com/video/BV1H24y1Q7sY)

**思路**

开始的时候没什么头绪，后面看了讲解就很清晰，也比较容易写出来了

这里想说的一点是，我们不用构造一个 dp 记录全部节点偷或者不偷的结果

根据递归的特性，我们记录当前节点的两种情况，是可以不断回到上一层的，这样可以节省了空间

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day66/0337\_house\_robber\_iii.go)
