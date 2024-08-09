# 🤨 day10

## 代码随想录算法训练营第十天| 字符串 344 541 151

### 344 反转字符串

题目链接：[https://leetcode.cn/problems/reverse-string/](https://leetcode.cn/problems/reverse-string/)

文章讲解：[https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html](https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

视频讲解：[https://www.bilibili.com/video/BV1fV4y17748](https://www.bilibili.com/video/BV1fV4y17748)

**思路**

与 [反转链表](https://github.com/hd2yao/leetcode/tree/master/training/day3/0206\_reverse\_linked\_list.go) 类似，都使用双指针法

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day10/0344\_reverse\_string.go)

### 541 反转字符串II

题目链接：[https://leetcode.cn/problems/reverse-string-ii/](https://leetcode.cn/problems/reverse-string-ii/)

文章讲解：[https://programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html](https://programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html)

视频讲解：[https://www.bilibili.com/video/BV1dT411j7NN](https://www.bilibili.com/video/BV1dT411j7NN)

**思路**

这道题其实也是在模拟过程

每 2k 个字符在循环，然后根据题意进行判断是哪种情况

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day10/0541\_reverse\_string\_ii.go)

### 151 翻转字符串里的单词

题目链接：[https://leetcode.cn/problems/reverse-words-in-a-string/](https://leetcode.cn/problems/reverse-words-in-a-string/)

文章讲解：[https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html](https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html)

视频讲解：[https://www.bilibili.com/video/BV1uT41177fX](https://www.bilibili.com/video/BV1uT41177fX)

**思路**

这道题第一次做应该会没什么思路，不过后续再做最难的部分就可以解决了，当然这只是说思路层面的，代码还是要多理解多写才可以

反转单词分两步：

* 先整个字符串翻转
* 每个单词再翻转

> 上面两个步骤也可以颠倒过来

这道题又多了一个步骤，就是要先去除字符串种多余的空格：头尾以及单词之间

**1. 去除多余空格**

这一步很容易想到使用内置方法 `strings.TrimPrefix()`、`strings.TrimSuffix()`，不过单词之间多余的空格还是需要手动去删除

这里我们可以回想一下 [移除元素](https://github.com/hd2yao/leetcode/tree/master/training/day1/0027\_remove\_element.go)， 使用快慢指针的方法来去除目标元素，留下需要的元素，因此在这一步中我们同样使用 **双指针法**

* 慢指针 slow 用来保存新元素
* 快指针 fast 用来寻找符合条件的元素，在改进之后可以直接使用一个 for 循环代替

其中，在单词之间只保留一个空格

```go
b := []byte(s)
slow := 0
for i := 0; i < len(b); i++ {
    if b[i] != ' ' {
        // 说明此时不是首单词
        if slow != 0 {
            b[slow] = ' '
            slow++
        }
        // 循环读取当前单词字母
        for i < len(b) && b[i] != ' ' {
            b[slow] = b[i]
            i++
            slow++
        }
    }
}
```

最后，通过 slow 来获取处理后的新字符串

```go
b = b[:slow]
```

**2. 翻转**

首先是整个字符串的翻转，这一步没什么好说的，在今天的第一题已经完成了

接着是每个单词的翻转，单词之间是空格相隔，也就是说，我们循环字符串，当遇到一个空格则说明一个单词结束，因此需要一个指针或是索引来标识单词的起始的位置

* 若是首单词，起始就是 0
* 除此，每个单词的起始都在空格的下一位

```go
start := 0
for i := 0; i < len(b); i++ {
    if b[i] == ' ' {
        reverse1(b[start:i])
        start = i + 1
    }
}
```

最后需要注意的一点，由于最后一个单词后面不存在空格，所以上面的循环并不没有将最后一个单词翻转，我们需要手动翻转一下，

```go
reverse1(b[start:])
```

> 思路还是很清晰，容易理解的，但是代码还是要好好去写写的，毕竟下笔不易

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day10/0151\_reverse\_words\_in\_a\_string.go)
