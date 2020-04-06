# 动态规划

## 64. 最小路径和
--- 
[原题链接](https://leetcode-cn.com/problems/minimum-path-sum/)

> 给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

思想： 初始化一个新的二维数组，从左上角开始进行遍历，每次取左边或上边与当前元素的最小和，二维数组右下角即为最小值。  
状态转移方程：` dp[i][j] = Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j];  `

要考虑边界情况
```javascript
var minPathSum = function(grid) {
    //初始化数组
    var row = grid.length;
    var col = grid[0].length;
    var dp = new Array(row);
    for(let i = 0 ; i < row; i++){
        dp[i] = new Array(col).fill(0);
    }
    for(let i = 0 ; i < row; i++){
        for(let j = 0 ; j < col; j++){
            //左上角
            if( i == 0 && j == 0){
                dp[i][j] = grid[i][j];
            //左边界
            } else if(i == 0 && j != 0){
                dp[i][j] = dp[i][j-1] + grid[i][j];
            // 右边界
            } else if(i != 0 && j == 0){
                 dp[i][j] = dp[i-1][j] + grid[i][j]
            } else if( i != 0 && j != 0){
                dp[i][j] = Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j];
            }
        }
    }
    return dp[row - 1][col - 1]
};
```

## 72. 编辑距离
---
[原题链接](https://leetcode-cn.com/problems/edit-distance/)

> 给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

思路： 对字符串有三种操作，插入、删除、替换。  
那么我们可以分析出来，每次的编辑距离都等于上一次最少的操作 +1。  
我们既可以对word1也可以对word2进行三种操作。那么复杂度达到了次方级别。      
所以可以如下优化  

!> word1的增加 === word2 的删除  
  word1的删除 === word2 的增加   


比如：eat --->  aaate  

| | |a|a|a|t|e|
|-|-|-|-|-|-|-|
| |0|1|2|3|4|5|
|e|1|-|-|-|-|-|
|a|2|-|-|-|-|-|
|t|3|-|-|-|-|-|

`dp[i][j-1]`   代表word1增加  
`dp[i-1][j]`   代表word2删除  
`dp[i-1][j-1]` 代表替换  

结果如下

| | |a|a|a|t|e|
|-|-|-|-|-|-|-|
| |0|1|2|3|4|5|
|e|1|1|2|3|4|5|
|a|2|1|1|2|3|4|
|t|3|2|2|2|2|3|  
  

```js
var minDistance = function (word1, word2) {
    var row = word1.length,
        col = word2.length;
    if (!row || !col) return row+col;
    //初始化
    var dp = new Array(row + 1).fill(0).map(() => new Array(col + 1).fill(0));
    for (var i = 0; i <= row; i++) {
        dp[i][0] = i;
    }
    for (var j = 0; j <= col; j++) {
        dp[0][j] = j;
    }
    //dp
    for (var i = 1; i < dp.length; i++) {
        for (var j = 1; j < dp[0].length; j++) {
            if (word1[i - 1] === word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1;
            }
        }
    }
    return dp[row][col]
};
```

## 300. 最长上升序列
--- 
[原题链接](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

> 给定一个无序的整数数组，找到其中最长上升子序列的长度。  

思想： 初始化长度相等的数组，两层循环，如果后面的数比前面的大，则`dp[i] = Math.max(dp[i],dp[j] + 1);`

```javascript
var lengthOfLIS = function(nums) {
    if(nums.length === 0) return 0;
    var dp = new Array(nums.length).fill(1);
    for(var i = 1; i < nums.length; i++){
        for(var j = 0 ; j < i ; j++){
            if(nums[i] > nums[j]){
                dp[i] = Math.max(dp[i],dp[j] + 1);
            }
        }
    }
    return Math.max(...dp)
};
```
