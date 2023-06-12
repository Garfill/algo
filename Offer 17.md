# 剑指 Offer 17. 打印从1到最大的n位数
 Q：[https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/](https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)
 
 思路：
 1. 如果只是小数字，直接计算出最大值，for 循环打印

```js
/**
 * @param {number} n
 * @return {number[]}
 */
var printNumbers = function(n) {
  let res = []

  for (let i = 1; i <= 10**n - 1; i++) {
    res.push(i)
  }
  return res
};
```

2. 对于大数字，考虑通过字符串表达
    - 从 个位 到 第n位，都有 0 - 9 的排列组合
    - 较小的数字前面是 一串0，从低位向高位进一位，就会少一个0
    - 进位的时机是 **数字中含有 9 的个数 + 0 的个数 = n**
    - 需要排除 全是0 的情况
    - 利用 n 长度字符串数组，模拟 大数字 的每一位排列情况
```js
var printNums = function(n) {
  let res = []
  let start = n - 1 // 0的个数
  let nine = 0 // 9的个数
  
  const num = new Array(n).fill('0') // 模拟数组
  
  function dfs(x) {
    if (x == n) {
        // 一次排列组合到达了最后一位（个位数)
        let current = res.join('')
        current = current.replace(/^0*/, '') // 去除前一段的0
        // current = num.slice(num).join('')
        // if (current !== '0') 
        // if (n = start + nine) start-- 
        // 可以通过这个来判断字符串数组截取的长度 [start:] 这里的要在 start-1 之前截取，取代上一句的正则去除
        if (current) {
            res.push(current)
        }
    } else {
        // x 表示第几位
        for (let i = 0; i < 10; i++) {
            // 某一位数的全排列情况
            num[x] = i
            if (i == 9) nine++
            dfs(x+1) // 全排列 低一位的数字
        }
        // nine-- // 用于截取法,某一位数循环排列完了之后，下次再从高位到这一位的循环过程中，又是从0 开始，因此减去该轮循环过程中的 +1
    }
  }
  
  dfs(0) // 从最高位开始
}
```