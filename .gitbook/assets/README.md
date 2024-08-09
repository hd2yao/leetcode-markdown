## day2

## 代码随想录算法训练营第二天| 数组 977 209 59

### 977 有序数组的平方

题目链接：https://leetcode.cn/problems/squares-of-a-sorted-array/

文章讲解：https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html

视频讲解： https://www.bilibili.com/video/BV1QB4y1D7ep

#### 思路
数组是有序的，且存在负数，此时数组元素平方后的最大值**只会在数组的左右两端**出现，因此考虑使用**双指针法**

知道上面的关键后，这道题的代码并不难写出来，这里想要说明两点注意

##### 需要新建一个数组
开始的时候，我选择在原数组上直接进行修改：
1.  只使用一个指针指 `rear` 向末尾元素 `nums[rear]`
2.  与头元素 `nums[0]` 比较， 若是末尾元素 `nums[rear]` 绝对值大，直接计算平方并重新覆盖到末尾；若是 nums[0] 绝对值大，先交换两个元素，再计算平方覆盖
```go
rear := len(nums) - 1
for rear >= 0 {
    if abs(nums[0]) > abs(nums[rear]) {
        nums[0], nums[rear] = nums[rear], nums[0]    
    }
    nums[rear] = square(nums[rear])
    rear--
}
```
上面的代码在 [-5, -3, -2, -1] 的输入下，输出的结果为 [1, 9, 4, 25]

这是因为，上面的代码只能保证将头尾的较大值放入尾部，但是不能保证每次交换后，头尾元素的绝对值在整个数组中是最大的两个，因为元素交换后，数组可能不再有序

##### 使用平方值比较
代码中可以直接使用 **平方值** 代替 **绝对值** 去比较

虽然 **绝对值** 是第一反应，不过最终结果是计算平方，这一点可以作为考虑

##### 使用 index
若是不使用 index 标记新数组并将平方值直接放入对应位置，只能是使用 append 结果是平方值降序排序，最后还需要对 result 做一个逆序的操作

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day2/0977_squares_of_a_sorted_array.go)

### 209 长度最小的子数组
题目链接：https://leetcode.cn/problems/minimum-size-subarray-sum/

文章讲解：https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html

视频讲解：https://www.bilibili.com/video/BV1tZ4y1q7XE

#### 思路
使用滑动窗口的关键，就是要搞清楚其中的含义：

- 窗口代表着子数组
- 窗口的起始位置与终止位置要根据窗口内的总和来移动：若当前总和大于目标值，起始位置向后移动；若总和小于目标值，终止位置向后移动

> 其实，滑动窗口就是暴力解法-双层 for 循环的剪枝

1. 终止条件

首先，我们可以确定循环的终止条件：因为要寻找最小的子数组，所以当窗口移动到数组的最后一个元素上时，循环结束
```go
for left < len(nums) || right < len(nums){
    // ...
}
```

2. 窗口移动

题目要求我们寻找最小的子数组，并且数组元素都为正数，也就是说，如果当前窗口 A 内的数组元素总和已经达到目标值，那么再扩大窗口到 A1 也一定是大于目标值的，
但是扩大后的子数组 A1 我们不考虑，因为 A1 不是最小的子数组，例如

> target = 7, nums = [2,3,1,2,4,3]
> 
> 子数组 A = [2, 3, 1, 2] 总和已经大于 7，我们就不再考虑包含 A 的数组 A1 = [2, 3, 1, 2, 4] 以及 A2 = [2, 3, 1, 2, 4, 3]

在我们得到符合条件的一组子数组后，要考虑的是，是否有更小的子数组符合题意

而数组 A 是由数组 A0 = [2, 3, 1] right 向后移动得到的，因此，想要在 A 之后继续寻找更小的子数组，只能将 left 向后移动

由此，我们可以得到窗口的移动规律：

- 窗口总和 sum 大于目标值 target 时，窗口的起始位置 left 向后移动
- 窗口总和 sum 小于目标值 target 时，窗口的终止位置 right 向后移动

```go
if sum < target {
    right++
    // ...
} else if sum <= target {
    // ...
    left++
}
```

3. 计算总和

由于窗口的每次移动都只涉及一个元素，所以计算窗口内总和时，我们不需要每次都从头开始计算

- right 向后移动，就是向窗口内增加一个元素
```go
right++
sum += nums[right]
```
- left 向后移动，就是向窗口内减去一个元素
```go
sum -= nums[left]
left++
```

4. 最小子数组的长度

同理，我们不需要计算每一次移动后的长度，而只需要计算符合条件的长度

第一次找到目标子数组后，将长度计入 length 中，后续取目标子数组与 length 的最小值即可

##### 滑动窗口-优化
通过上面的方法我们可以看出来，滑动窗口实际上就是**终止位置**从数组下标为 0 开始，一直到下标为 `len(nums) - 1`停止，
不会出现向前移动的情况，也不会出现跳过某一个元素的情况，因此，我们可以使用 `for-range` 来代替终止位置的指针
>  `for-range` 同样可以代替起始位置

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day2/0209_minimum_size_subarray_sum.go)

### 59 螺旋矩阵II
题目链接：https://leetcode.cn/problems/spiral-matrix-ii/

文章讲解：https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html

视频讲解：https://www.bilibili.com/video/BV1SL4y1N7mV/

#### 思路
手动画一画图，确定好边界，坚持**循环不变量原则**

[完整代码](https://github.com/hd2yao/leetcode/tree/master/training/day2/0059_spiral_matrix_ii.go)