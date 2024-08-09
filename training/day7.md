# 😎 day7

## 代码随想录算法训练营第七天| 哈希表 242 349 202 1

### 242 有效的字母异位词

题目链接：[https://leetcode.cn/problems/valid-anagram/](https://leetcode.cn/problems/valid-anagram/)

文章讲解：[https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html](https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)

视频讲解：[https://www.bilibili.com/video/BV1YG411p7BA](https://www.bilibili.com/video/BV1YG411p7BA)

**思路**

这道题很容易想到使用 map，所以不再详细说明，主要来说一下针对这道题的一种特殊方法

因为题目中有提到 “`s` 和 `t` 仅包含小写字母”，也就是说这两个字符串种包含的元素最多只有26种，选择使用数组会是更优的方法

如何将字母与数组相结合呢？ 需要把字符映射到数组也就是哈希表的索引下标上

**因为字符`a`到字符`z`的ASCII是26个连续的数值，所以字符a映射为下标0，相应的字符z映射为下标25**

```go
s[i] - 'a'
```

可将字符对应到数组下标上

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day7/0242\_vaild\_anagram.go)

### 349 两个数组的交集

题目链接：[https://leetcode.cn/problems/intersection-of-two-arrays/](https://leetcode.cn/problems/intersection-of-two-arrays/)

文章讲解：[https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html](https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html)

视频讲解：[https://www.bilibili.com/video/BV1ba411S7wu](https://www.bilibili.com/video/BV1ba411S7wu)

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day7/0349\_intersection\_of\_two\_arrays.go)

### 202 快乐数

题目链接：[https://leetcode.cn/problems/happy-number/](https://leetcode.cn/problems/happy-number/)

文章讲解：[https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html](https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html)

**思路**

**当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法了**

题目中说会无限循环，这说明在求和的过程中会出现重复的过程，这里动手去算一算就可以知道了，也能够更加明白这个求和的过程，有助于理解代码

因此，这道题的过程可以分为两个过程：

* 求和
* 判断结果是否重复

首先，求和代码的核心其实就是求余

判断是否重复就要用到集合，go 中使用 map

```go
numMap := make(map[int]struct{}, 0)
```

> map 中 value 的类型都是可以的，只需要判断 key 是否存在即可，使用 struct{} 来构造集合是算法

每次求和结果去集合中寻找是否已存在，若不存在，存入然后重复这个过程；若存在，说明开始重复，直接结束

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day7/0202\_happy\_number.go)

### 1 两数之和

题目链接：[https://leetcode.cn/problems/two-sum/](https://leetcode.cn/problems/two-sum/)

文章讲解：[https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html](https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html)

视频讲解：[https://www.bilibili.com/video/BV1aT41177mK](https://www.bilibili.com/video/BV1aT41177mK)

**思路**

使用 map 分别保存对应差值和下标

梦之始，两数之和！

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day7/0001\_two\_sum.go)
