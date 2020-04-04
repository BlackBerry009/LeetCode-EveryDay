# 动态规划

## 64. 最小路径和
--- 
[原题链接]

> 

思想： 
```javascript
var minPathSum = function(grid) {
    //初始化
    var row = grid.length;
    var col = grid[0].length;
    var dp = new Array(row);
    for(let i = 0 ; i < row; i++){
        dp[i] = new Array(col).fill(0);
    }

    for(let i = 0 ; i < row; i++){
        for(let j = 0 ; j < col; j++){
            if( i == 0 && j == 0){
                dp[i][j] = grid[i][j];
            } else if(i == 0 && j != 0){
                dp[i][j] = dp[i][j-1] + grid[i][j];
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
[原题链接]

> 

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