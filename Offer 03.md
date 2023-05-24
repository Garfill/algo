# 剑指 Offer 03. 数组中重复的数字

Q: [https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

1. 简单思路：遍历数组，找出重复的数字返回，利用哈希表存储已经访问过的

```js
function traverse(list) {
    const set = new Set()
    
    for (let i=0;i<list.length;i++){
        if (set.has(list[i]) return list[i]
        set.add(list[i])
    }
}
// O(n) 时间空间
```

1. 交换位置：有一个前提点是 **数组长度为n，数组元素大小范围0～n-1**，因此 数组下标和元素大小一一对应

```js
function find(list) {
    let i=0
    while (i<list.length) {
        if (i == list[i]) {
            // 元素和下标对应
            i++
            continue
        } else if (list[i] == list[list[i]]) {
            // 出现两个下标重复的元素
            return list[i]
        } else {
            // 交换两个不同下标元素
            let temp = list[list[i]]
            list[list[i]] = list[i]
            list[i] = temp
        }
    }
}
// O(n) 时间，O(1)时间
```