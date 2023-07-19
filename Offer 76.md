# 剑指 Offer II 076. 数组中的第 k 大的数字

[Question](https://leetcode.cn/problems/xx4gT2/description/)

思路
1. 利用快排，将 k-1 个数移动到前面，对应第 k 个就是所求的值
2. 快排过程中，作为 pivot 的值在 每一次分区之后的index，就是最终index

```js
function findKthLargest(nums, k) {
    let l= 0, r = nums.length - 1, res = 0;
    
    function quickSort(nums, l, r) {
        if (l >= r) { return l }
        const index = partition(nums, l, r)
        if (index+1 === k) return index
        if (index + 1 > k) {
            return quickSort(nums, l, index - 1)
        } else {
            return quickSort(nums, index + 1, r)
        }
    }
    
    function partition(nums, l, r) {
        const pivot = nums[l]
        let i = l
        for (let j = i+1; j <= r; j++) {
            if (nums[j] >= pivot) {
                i++;
                [nums[i], nums[j]] = [nums[j], nums[i]];
            }
        }
        
        nums[l] = nums[i]
        nums[i] = pivot
        
        return i
    }
    
    const index = quickSort(nums, l, r)
    return nums[index]
    
}
```