---
title: DFS和BFS算法
date: 2021-03-02 15:00
comments: true
tags:
    - js
---
#### DFS & BFS
+ DFS：深度优先算法（Deep First Search）
简单来说，从根节点出发，然后依次向下继续搜索，直到遇到叶子节点，此时就会向上回溯，继续向为访问过的点继续深度搜索。
+ BFS：广度优先搜索（Breath First Search）
简单的说，BFS是从根节点开始，沿着树的宽度遍历树的节点，如果发现目标，则演算终止。
<!-- more -->
#### 简单实现一个二叉树
为了方便演示，写了一个简单生成二叉树的方法，用于算法测试。

```javascript
// 二叉树节点
const Node = function(val) {
    this.value = val
    this.left = null
    this.right = null
}
// 二叉树数据（不考虑数据合理性）
const arr = [3, 9, 20, null, null, 15, 7, null, null, null, null, 6, 8, 4, 5];
// `
//        3
//     /     \
//     9     20
//         /    \
//        15     7
//       / \    / \
//       6  8   4  5
// `
// 生成二叉树递归
function generateNodeByRecursion(data, index = 0, val = 0) {
    let node = new Node(data[index]);
    let left = index * 2 + 1;
    let right = left + 1;
    if(data[left] !== null && data[left] !== undefined) {
        node.left = generateNodeByRecursion(data, left, val + 1)
    }
    if(data[right] !== null && data[right] !== undefined) {
        node.right = generateNodeByRecursion(data, right, val + 1)
    }
    return node;
}
console.log(generateNodeByRecursion(arr), '------------生成二叉树-递归');
// 生成二叉树非递归
function generateNodeNonRecursion(data) {
    let res =  new Node(data[0])
    let temp = [{ node: res, index: 0 }];
    while(temp.length) {
        let { node, index } = temp.shift();
        let left = index * 2 + 1;
        let right = left + 1;
        if(data[left] !== null && data[left] !== undefined) {
            node.left = new Node(data[left]);
            temp.push({ node: node.left, index: left });
        }
        if(data[right] !== null && data[right] !== undefined) {
            node.right = new Node(data[right]);
            temp.push({ node: node.right, index: right});
        }
    }
    return res;
}
console.log(generateNodeNonRecursion(arr), '------------生成二叉树-非递归');
```

举例如下：
```javascript
const tree = {
    name: 'root',
    children: [
        {
            name: 'a',
            children: [
                {
                    name: 'a1',
                    children: []		
                },
                {
                    name: 'a2',
                    children: []		
                }
            ]
        },
        {
            name: 'b',
            children: [
                {
                    name: 'b1',
                    children: []		
                },
                {
                    name: 'b2',
                    children: []		
                }
            ]
        }
    ]
}

// 深度优先的方式遍历 打印 name
// ['root', 'a','a1', 'a2', 'b', 'b1', 'b2']

// 深度优先 - 递归
function getDfsByRecursion(tree, res = []) {
    res.push(tree.name);
    if(tree.children.length) {
        tree.children.forEach(item => {
            getDfsByRecursion(item, res);
        })
    }
    return res
}
console.log(getDfsByRecursion(tree), '-----------深度优先递归');
// 深度优先 - 非递归
function getDfsNonRecursion(tree, res = []) {
    let temp = [tree];
    while(temp.length) {
        const node = temp.pop();
        if(!node) continue;
        res.push(node.name);
        for(let i = node.children.length -1; i >= 0; i--) {
            temp.push(node.children[i]);
        }
    }
    return res;
}
console.log(getDfsNonRecursion(tree), '-----------深度优先非递归');
```

获取二叉树的最大深度：
+ 递归（深度优先）
```javascript
// 获取二叉树的最大深度-递归（深度优先）
function getTreeDepthByRecursion(node) {
    if(!node) return 0;
    return Math.max(getTreeDepthByRecursion(node.left), getTreeDepthByRecursion(node.right)) + 1;
}
console.log(getTreeDepthByRecursion(binaryTree), '------------二叉树最大深度-递归');
```
+ 非递归（广度优先）
```javascript
function getTreeDepthNonRecursion(node) {
    if(!node) return 0;
    let total = 0;
    let queue = [node];
    while(queue.length) {
        let temp = [];
        queue.forEach(item => {
            if(item.left) temp.push(item.left);
            if(item.right) temp.push(item.right);
        })
        total += 1;
        queue = temp;
    }
    return total;
}
console.log(getTreeDepthNonRecursion(binaryTree), '------------二叉树最大深度-非递归');
```