# 剑指Offer 04 二维数组中的查找

Q：[https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

1. 暴力算法（循环每行，每行用二分法查找）

```js
function find(matrix, target) {
    for (const rows of matrix) {
        let index = binarySearch(rows, target)
        if (index >= 0) return true
    }
    return false
}

function binarySearch(nums, target) {
    let i = 0, j = nums.length - 1
    
    while (i <= j) {
        let mid = Math.floor((j-i)/2) + i
        let num = nums[mid]
        if (target < num) {
            j = mid - 1
        } else if (target > num) {
            i = mid + 1
        } else {
            return mid
        }
    }
    return -1
}

// O(nlogm)
```

2. 利用标志数（z字查找）

从某个极大值开始，根据大小减少行列数，知道找到为止
```js
function find(nums, target) {
    if (nums.length === 0) return false // 极端空数组情况
    let m = nums.length-1, n = nums[0].length - 1
    // 取 [0, n]开始，从右到左，从上到下收缩
    let i = 0, j = n
    while (i < m && j >=0) {
        let current = nums[i][j]
        if (target < current) {
            // 往左
            j--
        } else if (target > current) {
            // 往下
            i++
        } else {
            return true
        }
    }
    
    return false
}
```
