# 					回溯算法

## 回溯算法的术语

`路径` 已经做出的选择

`选择列表` 当前可以做的选择

`结束条件` 到达了决策树的底层，无法再做选择的条件

## 回溯算法代码框架

```c++
void backtrack(路径, 选择列表){
    if 满足结束条件:
        result.add(路径)
        return;
    
    for 选择 in 选择列表:
        做选择
        backtrack(路径, 选择列表)
        撤销选择
}
```

根据下述递归代码框架，`for`循环里面`做选择`属于前序遍历，而`撤销选择`属于后序遍历；之所以这样安排的原因可见下图所示

```c++
void traverse(TreeNode* root) {
    for (TreeNode* child : root->childern)
        // 前序遍历需要的操作
        traverse(child);
        // 后序遍历需要的操作
}
```

![img](https://labuladong.gitee.io/algo/images/backtracking/4.jpg)

## 我的理解

1. 回溯算法本质上是`DFS`的一种应用
2. 利用回溯算法解题时，往往分为两个函数，一个是`backtrace()`函数，用于解决回溯本身；另一个是主函数，用以解决问题本身

## Leetcode相关题目

