# 剑指 Offer 22. 链表中倒数第k个节点

Q: [https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/description/](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/description/)

思路：
快慢指针，快指针向前走 k 步，当快指针到头（null），慢指针就是倒数第k

k 为 3 => [slow, T, T, fast]

```js
var getKthFromEnd = function(head, k) {
    let fast = head, slow = head;
    while (fast && k > 0) {
        fast = fast.next
        k--
    }
    while (fast) {
        slow = slow.next
        fast = fast.next
    }
    
    return slow
}
```