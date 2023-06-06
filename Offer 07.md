# Offer 07 重建二叉树
Q：[https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

思路
1. 前序遍历：先读父节点，然后左右节点
2. 中序遍历：先读所有左节点，然后父节点，最后右节点
3. 子树也是和父级树 一样的遍历顺序
4. 构建出父节点，递归调用生成左右节点

```js
function buildTree(preOrder, inOrder) {
    if (preOrder.length === 0) return null // 空树
    root = new TreeNode(preOrder[0]) // 前序遍历第一个一定是根节点
    // 父节点在中序遍历中的位置，左边就是左子树
    const rootIndex = inOrder.findIndex(item => item === preOrder[0])
    // 子树的遍历方式和 父级树一致
    // 递归调用生成子树的根节点
    const leftTree = inOrder.slice(0, rootIndex)
    const rightTree = inOrder.slice(rootIndex + 1)
    root.left = buildTree(preOrder.slice(1, leftTree.length + 1), leftTree)
    root.right = buildTree(preOrder.slice(leftTree.length + 1), rightTree) 
    
    return root
}
```