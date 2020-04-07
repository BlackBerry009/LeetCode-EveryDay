# 其他

## 7. 整数反转
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

## 48. 旋转图像
---
[原题链接](https://leetcode-cn.com/problems/rotate-image/)

> 给定一个 n × n 的二维矩阵表示一个图像。  
 将图像顺时针旋转 90 度。

|1|2|3|         |7|4|1|    
|-|-|-|         |-|-|-|    
|4|5|6|    =>   |8|5|2|     
|7|8|9|         |9|6|3|

我们首先可以观察到，原先的数字在第i行第j列  
那么转变后数字变成了第j行，倒数第i列

所以可以得到关系`newArr[j][len-1-i] = arr[i][j]`

#### 解一

 ```js
 var rotate = arr => {
    var len = arr.length;
    var newArr = new Array(len).fill(0).map( () => new Array(len).fill(0));
    for(let i = 0 ; i < len ; i++){
        for(let j = 0; j < len; j++){
            newArr[j][len-1-i] = arr[i][j]
        }
    }
    return newArr;
}
```
#### 解二
翻转 + 对称交换

|1|2|3|         |7|8|9|        |7|4|1|
|-|-|-|         |-|-|-|        |-|-|-|
|4|5|6|    =>   |4|5|6|    =>  |8|5|2|
|7|8|9|         |1|2|3|        |9|6|3|

经过第一步翻转，可以发现，做一次关于左上到右下的对称即可得到答案
```js
var rotate = arr => {
    let len = arr.length;
    // 翻转
    for(let i = 0 ; i < len / 2; i++){
        [arr[i],arr[len-1-i]] = [arr[len-1-i],arr[i]]
    }
    // 对称
    for(let i = 0 ; i < arr.length; i++){
        for(let j = i ; j < arr[0].length; j++){
            let temp = arr[i][j];
            arr[i][j] = arr[j][i];
            arr[j][i] = temp;
        }
    }
    return arr;
}
```
#### 解三
这样一种方法也是挺简单的一种，先做对称，然后把每一行逆置即可。
```js
var rotate = matrix => {
    for (let i = 0; i < matrix.length; i++) {
        for (let j = i; j < matrix[i].length; j++) {
            [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]]
        }
    }
    matrix.forEach(row => row.reverse())
    return matrix;
};
```


