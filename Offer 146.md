# 146. LRU 缓存

Q: [https://leetcode.cn/problems/lru-cache/](https://leetcode.cn/problems/lru-cache/)

思路：
1. 由于要使用 O(1) 复杂度，因此需要有地方存储node位置，才能随机访问，而不是遍历列表
2. 基于 1 ，采用hash表映射 （key - node)
3. 采用双向链表，记录各个节点的 key/value
4. 采用数组记录，需要在hash表中记录每个node 位置，还需要在更新时通过遍历来更新位置O(n)

```js

/**
 * @param {number} capacity
 */
var LRUCache = function(capacity) {
  this.capacity = capacity
  this.size = 0
  this.keyMap = new Map()
  this.head = new LinkNode(0, 0)
  this.tail = new LinkNode(0, 0)
  this.head.next = this.tail
  this.tail.prev = this.head
};

var LinkNode = function(key, value) {
  this.prev = null
  this.next = null
  this.key = key
  this.value = value
}
/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
  let node = this.keyMap.get(key)
  if (!node) {
    return -1
  }
  this.moveHead(node)
  return node.value
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
  let node = this.keyMap.get(key)
  if (node) {
    node.value = value
    this.moveHead(node)
  } else {
    node = new LinkNode(key, value)
    this.addToHead(node)
    this.keyMap.set(key, node)
    this.size++
    if (this.size > this.capacity) {
      let tail = this.removeTail()
      this.size--
      this.keyMap.delete(tail.key)
    }
  }
};

LRUCache.prototype.addToHead =function(node) {
  node.next = this.head.next
  node.next.prev = node
  this.head.next = node
  node.prev = this.head
}

LRUCache.prototype.moveHead = function(node) {
  node.prev.next = node.next
  node.next.prev = node.prev
  
  node.next = this.head.next
  node.prev = this.head
  node.next.prev = node
  this.head.next = node
}

LRUCache.prototype.removeTail = function() {
  let node = this.tail.prev
  this.removeNode(node)
  return node
}

LRUCache.prototype.removeNode = function(node) {
  node.prev.next = node.next
  node.next.prev = node.prev
  node.next = null
  node.prev = null
  return node
}
/**
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
```