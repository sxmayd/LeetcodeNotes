# 								KMP算法

## 概念

- KMP 算法是一个快速查找匹配串的算法，它的作用其实就是[Leetcode 28](https://leetcode-cn.com/problems/implement-strstr/)问题：**如何快速在「原字符串」中找到「匹配字符串」**

- 暴力搜索不考虑剪枝的话复杂度是 O(m * n) 的，而 **KMP 算法的复杂度为 O(m + n)**

- **KMP 之所以能够在 O(m + n) 复杂度内完成查找，是因为其能在「非完全匹配」的过程中提取到有效信息进行复用，以减少「重复匹配」的消耗**

## 术语

`前缀`：对于字符串 abcxxxxefg，我们称 abc 属于 abcxxxxefg 的某个前缀。
`后缀`：对于字符串 abcxxxxefg，我们称 efg 属于 abcxxxxefg 的某个后缀。

