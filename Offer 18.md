# 剑指 Offer 18. 删除链表的节点
Q: [https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

思路
- 通过节点的值，确定某个节点
- 改变起前节点的next 指向
- 由于用到了 前节点，考虑到极端情况（第一个节点就是），添加一个头节点


```js
var deleteNode = function(head, val) {
  let headNode = new ListNode()
  headNode.next = head
  let current = headNode
  while (current.next) {
    if (current.next.val === val) {
      current.next = current.next.next
      break
    }
    current = current.next
  }
  // 通过返回添加的头节点的next，也就指向新链表的原头节点
  return headNode.next
};
```

思路2:双指针
- 前后指针，判断前指针的值
- 需要处理极端情况

```js
var deleteNode = function(head, val) {
  let prev = head;
  let current = head.next;
  // 极端情况：头节点就是
  if (prev.val === val) {
    return prev.next;
  }
  while (current) {
    if (current.val === val) {
      prev.next = current.next
      break;
    } else {
      current = current.next
      prev = prev.next
    }
  }
  return head;
}
```