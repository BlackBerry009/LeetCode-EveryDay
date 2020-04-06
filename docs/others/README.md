# 其他

## 整数反转
[原题链接](https://leetcode-cn.com/problems/reverse-integer/)
> 给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

```js
var reverse = function(x) {
    const border = 2**31
    const max = border - 1
    const min = -border
    const result = (x > 0 ? 1 : -1) * String(x).split('').filter(x => x !== '-').reverse().join('')
    return result > max || result < min ? 0 : result 
};
```
