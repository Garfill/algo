# Offer21 调整数组顺序使奇数位于偶数前面

Q: [https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/description/](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/description/)

思路1
遍历两次原数组，先后添加奇偶数字
```js
var exchange = function(nums) {
    const ret = []
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] %2 === 1) { ret.push(nums[i])} 
    }
    for (let i = 0; i < nums.length; i++) {
      if (nums[i] %2 === 0) { ret.push(nums[i])} 
    }
    return ret
}
```


思路2
双指针：一头一尾指向新数组，奇数添加到新数组前面，偶数添加到新数组后面
```js
var exchange = function(nums) {
    const ret = new Array(nums.length).fill(0)
    let i = 0, j = nums.length - 1
    for (const num of nums) {
        if (num % 2 === 1) {
            ret[j--] = num // 同时 j 往前走一步
        } else if (num % 2 === 0) {
            ret[i++] = num
        }
    }
    
    return ret
}
```


思路3
原地交换：头尾双指针向中间靠近，两边停下后交换数，直至相遇
```js
var exchange = function(nums) {
    let i = 0, j = nums.length - 1
    while (i < j) {
        while(i < j && nums[i] % 2 === 1) {
            i++
            // 一直是奇数，往后递进
        }
        while(i < j && nums[j] % 2 === 0) {
            j--
        }
        // 双指针靠近到停下
        if (i < j) {
            let temp = nums[i]
            nums[i] = nums[j]
            nums[j] = temp
            i++
            j--
        }
    }
    
    return nums
}
```