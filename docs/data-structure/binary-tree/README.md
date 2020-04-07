# 二叉树

## 105. 从前序与中序遍历序列构造二叉树
---
[原题链接](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

```js
var buildTree = function (preorder, inorder) {
    if (preorder.length === 0 || inorder.length === 0) return;
    var root = new TreeNode(preorder[0]);
    var index = inorder.indexOf(root.val);
    var preLeft = preorder.slice(1, index + 1);
    var preRight = preorder.slice(index + 1);
    var inLeft = inorder.slice(0, index);
    var inRight = inorder.slice(index + 1);
    root.left = buildTree(preLeft, inLeft);
    root.right = buildTree(preRight, inRight);
    return root;
};
```

## 106. 从中序与后序遍历序列构造二叉树
---
[原题链接](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

```js
var buildTree = function(inorder, postorder) {
    if(inorder.length == 0 || postorder.length == 0) return null;
    var root = new TreeNode(postorder[postorder.length - 1]);
    var index = inorder.indexOf(root.val);
    var inLeft = inorder.slice(0,index);
    var inRight = inorder.slice(index+1);
    var postLeft = postorder.slice(0,index);
    var postRight = postorder.slice(index,postorder.length-1)
    root.left = buildTree(inLeft,postLeft);
    root.right = buildTree(inRight,postRight);
    return root;
};
```