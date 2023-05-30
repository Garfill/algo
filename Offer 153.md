# 153. 寻找旋转排序数组中的最小值

Q:[https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)

思路
- 原数组 **有序递增**，经过旋转后 **分为两段有序递增**
- 采用二分法，寻找中间值

```js
var findMin = function(nums) {
    let high = nums.length - 1
    let low = 0
    while (low < high) {
        // 不存在相同的，所以不可能相等，相等即为找到
        let mid = Math.floor((high - low) / 2) + low
        if (nums[mid] < nums[high]) {
            // 1. 中间点落在右边段
            high = mid
        } else {
            // 2. 中间点落在左边段 nums[low] < nums[mid]
            low = mid + 1
            // 这里 +1 因为找是最小值，肯定不是mid
        }
    }
    // 两个指针向中间收缩到同一个点
    return nums[low]
}

// O(logN)
```
