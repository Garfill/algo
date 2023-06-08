# 剑指 Offer 15. 二进制中1的个数
Q: [https://leetcode.cn/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/](https://leetcode.cn/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

解法1:
- 通过求余，不断求出低位数

```js
function hanmingWeight(n) {
    let res = 0
    while (n !== 0) {
        if (n%2) {
            // 求余得出最低位数字
            res++
        }
        n = Math.floor(n/2) // 只要整数
    }
    return res
}
```

解法2（通过位运算&）
- 通过逐位对比，求出 1 的个数
- 通过对 1 的左移(<<)操作，可以对比各个位数
```js
function hanmingWeight(n) {
    let res = 0
    for (let i = 0; i < 32; i++) {
        if (n & (1 << i)){
            res++
        }
    }
    return res
}
```

解法3（n&(n-1)
- n&(n-1) 把最低位的 1 变成 0
- 一直迭代 上一步，直到全变成 0
- 原理类似不断除2

```js
function hanmingWeight(n) {
    let res = 0
    while(n) {
        n = n&(n-1)
        res++
    }
    return res
}
```

