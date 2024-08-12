# 🤗 day14

## 代码随想录算法训练营第十四天| 栈与队列 232 225

### 232 用栈实现队列

题目链接：[https://leetcode.cn/problems/implement-queue-using-stacks/](https://leetcode.cn/problems/implement-queue-using-stacks/)

文章讲解：[https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html](https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html)

视频讲解：[https://www.bilibili.com/video/BV1nY4y1w7VC](https://www.bilibili.com/video/BV1nY4y1w7VC)

**思路**

这种题就是在模拟过程，只要始终记住栈是 FILO 而队列是 FIFO，动手画一画就能够比较清楚地知晓整个过程

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day14/0232\_implement\_queue\_using\_stacks.go)

### 225 用队列实现栈

题目链接：[https://leetcode.cn/problems/implement-stack-using-queues/](https://leetcode.cn/problems/implement-stack-using-queues/)

文章讲解：[https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html](https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html)

视频讲解：[https://www.bilibili.com/video/BV1Fd4y1K7sm](https://www.bilibili.com/video/BV1Fd4y1K7sm)

**思路**

使用栈实现队列，我们使用了两个栈，一个用作输入栈，另一个用作输出栈

而用队列实现栈，如果我们同样使用两个队列，一个用作输出一个用作输入，下面看一下是否可行

现在我们思考一下，输入栈正常接收 push 的数据，1 - 2 - 3 - 4 ；当 pop 时，将输入栈的数据放到输出栈中输出，由于是队列，所以转移的顺序 依旧是 1 - 2 - 3 - 4，所以无法像栈一样输出 4 -3 - 2 - 1

所以要想改变顺序只有将尾部的元素放在头部，这样的话一个队列就可以实现，每次 pop 将前面的元素依次取出再放如队尾，可以看做是一个循环队列

那如果使用两个队列呢？

思路跟一个队列类似，还是需要先取出前面的元素，取出的元素可以直接保存在另一个队列中，这些元素的相对位置还是不变的，等待 pop 结束后再将其放回

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day14/0225\_implement\_stack\_using\_queues.go)
