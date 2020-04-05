# 动态规划

## 64. 最小路径和
--- 
[原题链接](https://leetcode-cn.com/problems/minimum-path-sum/)

> 给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

思想： 初始化一个新的二维数组，从左上角开始进行遍历，每次取最小和，二维数组右下角即为最小值。  
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
