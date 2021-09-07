# C++特性的一些题目

### [剑指 Offer 20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/) ★

题目描述：
部分数值列举如下：["+100", "5e2", "-123", "3.1416", "-1E-16", "0123"]

部分非数值列举如下：["12e", "1a3.14", "1.2.3", "+-5", "12e+5.4"]

`也就是说，表示数值的字符串遵循模式 A.[B][eC]​ 或者 .[B][eC]`​

```C++
class Solution {
public:
    string::iterator sEnd;

    bool isNumber(string s) {
        if(s.empty()) return false;

        auto iter = s.begin();
        sEnd = s.end();

        // 去除开头的空格，例如 " 0"
        while(*iter == ' ') iter++;

        // 寻找 A 整数位
        bool numeric = scanInteger(iter);

        // 如果出现 '.' 则接下来是 B 小数部分
        if(*iter == '.'){
            iter++;
            // 小数位 和 整数位 存在一个即可
            numeric = scanUnsignedInteger(iter) || numeric;
        }

        // 存在 e, 查找指数位
        if(*iter == 'e' || *iter == 'E'){
            iter++;
            // 如果有 e 则指数位 C 必须存在
            numeric = scanInteger(iter) && numeric;
        }

        // 去除数字最后的空格 例如： "1 "
        while(*iter == ' ') iter++;

        // 得同时判断是否到达字符串结尾 以免出现这种情况 "1 4"
        return numeric && (iter == s.end());
    }

    // 扫描 0-9 的数字
    bool scanUnsignedInteger(string::iterator& iter){
        bool have_number = false;
        while(iter != sEnd && (*iter) >= '0' && (*iter) <= '9'){
            have_number = true;
            iter++;
        }
        return have_number;
    }

    // 扫描含有 +/- 号的 0-9 的数字
    bool scanInteger(string::iterator& iter){
        if(*iter == '+' || *iter == '-') iter++;

        return scanUnsignedInteger(iter);
    }
};
```

`注`

1. 将字符串划分为3部分，A:小数点之前 B:小数点之后,e之前 C:e之后
   `A和B只需存在一个，若e存在，C必须存在。按照此规则处理，若成功到达字符串结尾，返回true`
   **使用STL的迭代器传递参数，达到和数组的指针同等的便利性和空间复杂度**
