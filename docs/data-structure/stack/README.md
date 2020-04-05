# 栈

## 20. 有效的括号
--- 
[原题链接](https://leetcode-cn.com/problems/valid-parentheses/)

> 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。  

#### 解一： 
用栈解决，每次push时，判断当前和栈顶元素的关系。

```javascript
var isValid = function(str) {
    var mp = new Map([
        [
            '{', 1
        ], [
            '}', -1
        ], [
            '[', 2
        ], [
            ']', -2
        ], [
            '(', 3
        ], [
            ')', -3
        ]
    ])
    var arr = str.split('');
    var result = [];
    arr.forEach(item => {
        //括号相等
        if( mp.get( ...result.slice(-1) ) + mp.get(item) === 0){
            result.pop()
        } else {
            result.push(item)
        }
    })
    return result.length === 0;
}
```

#### 解二：  
> 取自LeetCode评论 思路清奇

```javascript
var isValid = function (s) {
    while (s.length) {
        var temp = s;
        s = s.replace('()', '');
        s = s.replace('[]', '');
        s = s.replace('{}', '');
        if (s == temp) return false
    }
    return true;
};
```
