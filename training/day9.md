# 😌 day9

## 代码随想录算法训练营第九天| 哈希表 454 383 15 18

### 454 四数相加II

题目链接：[https://leetcode.cn/problems/4sum-ii/](https://leetcode.cn/problems/4sum-ii/)

文章讲解：[https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html)

视频讲解：[https://www.bilibili.com/video/BV1Md4y1Q7Yh](https://www.bilibili.com/video/BV1Md4y1Q7Yh)

**思路**

这道题的关键有两点：

* `nums1[i] + nums2[j] == - nums3[k] - nums4[l]`
* 如何使用 map 来保存信息

首先第一点，两两组合之后，四数之和降维成两数之和，将四重循环转变为两个二重循环，大大降低了时间复杂度，避免超时

再来看第二点，在两数之和中，map 中的 key 保存的是 `target - nums[i]` ，同样的四数之和中，key 也保存 `nums1[i] + nums2[j]` 或是 `- nums1[i] - nums2[j]`； 两数之和中只会出现一组结果，因此 value 直接保存对应的下标，而在本题中，组合的结果不止一种，而且只需要返回结果的数量，而不需要返回全部的组合， 因此直接统计数量即可

```go
for i := 0; i < len(nums1); i++ {
    for j := 0; j < len(nums2); j++ {
        targetMap[nums1[i]+nums2[j]]++
    }
}
```

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day9/0454\_4sum\_ii.go)

### 383 赎金信

题目链接：[https://leetcode.cn/problems/ransom-note/](https://leetcode.cn/problems/ransom-note/)

文章讲解：[https://programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html](https://programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html)

**思路**

这道题还是很简单的，跟之前 [0242-vaild-anagram](https://github.com/hd2yao/leetcode/tree/master/training/day7/0242\_vaild\_anagram.go) 差不多

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day9/0383\_ransom\_note.go)

### 15 三数之和

题目链接：[https://leetcode.cn/problems/3sum/](https://leetcode.cn/problems/3sum/)

文章讲解：[https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html)

视频讲解：[https://www.bilibili.com/video/BV1GW4y127qo](https://www.bilibili.com/video/BV1GW4y127qo)

**思路**

哪怕是第二次写这道题，想到使用双指针法，但是还是会一头雾水，依稀记得在第一次做的时候的一个词语 “剪枝”，可是实际做的时候还是无法把这个词代入

**1. 排序**

首先我们来回顾一下，[有序数组的平方](https://github.com/hd2yao/leetcode/tree/master/training/day2/0977\_squares\_of\_a\_sorted\_array.go)， 这道题中我们也是使用的是双指针，双指针始终指向平方后最大的两个元素，为什么平方最大的元素只会出现在数组两端，因为这个数组是有序的

我们要求三数之和，使用双指针法，同样需要先进行排序

**2. left 和 right 移动**

通过一个 for 循环遍历数组，表示第一个数，两个指针分别指向 `i+1` 和 `len(nums)-1`

* 当总和大于 target，我们需要减小总和，那就要将 right 向左移动一位，因为左边的数永远小于等于右边的数
* 同理，当总和小于 target，我们需要增加总和，那就要将 left 向右移动一位

> * 因为每一次都只移动 left 或者 right，只涉及一个元素的变动，因此不会忽略某一种情况

在本题中，结果不能有重复的情况，例如，当前 nums\[i] = -1, nums\[left] = -1, nums\[right] = 2, 假如我们需要增加总和，要移动 left， 而 nums\[left+1] = -1, 那么我们就可以直接跳过这个结果，因为移动前后的三元组都是 \[-1, -1, 2]；移动 right 与 left 一致

**3. i 移动**

上面我们说明了 left 与 right 出现重复的情况，由于是三数之和，如果当 i 指向相同元素要如何移动？例如 \[-1, -1, 0, 2]

当 i = 0，我们发现 nums\[i] == nums\[i+1]，那么是否要像上面一样直接跳过。

如果直接跳过，此时 i = 1，后面是没有能够使三数之和为 0 的情况，但实际上我们可以看出应该是有一个结果的 \[-1, -1, 2]，这个结果应该是在 i = 0 时得到的

通过上面的例子，我们可以知道要去重 i，应该是判断 nums\[i] == nums\[i-1]

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day9/0015\_3sum.go)

### 18 四数之和

题目链接：[https://leetcode.cn/problems/4sum/](https://leetcode.cn/problems/4sum/)

文章讲解：[https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html](https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html)

视频讲解：[https://www.bilibili.com/video/BV1DS4y147US](https://www.bilibili.com/video/BV1DS4y147US)

**思路**

与三数之和的过程一致，无非是多了一层循环，这个过程一旦掌握，五数之和、六数之和 都是类似的

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day9/0018\_4sum.go)
