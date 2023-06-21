# 剑指 Offer 24. 反转链表

Q:[https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/description/](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/description/)

1. 迭代法

```js
var reverseList = function(head) {
    let prev = null;
    let curr = head;
    
    while (curr) {
        // 记住原来的curr.next，防止翻转过程丢失
        const tmp = curr.next
        // 翻转
        curr.next = prev
        // 迭代
        prev = curr
        curr = tmp
    }
    
    return prev;
}
```

2. 递归法

思路：
分割成一个head，和后面的链表，对后面的链表重复递归
(a, rest) => (a, (b, rest))...

```js
var reverseList = function(head) {
    if (head == null || head.next == null) {
        // 递归终止条件
        // 只剩最后一个节点返回
        return head
    }
    // 递归
    const newHead = reverseList(head.next)
    
    // 每个递归项操作
    head.next.next = head
    head.next = null
    
    return newHead
}
```

