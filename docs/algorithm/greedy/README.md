# 贪心算法

> **概念**：在对问题求解时，总是做出在当前看来是最好的选择。也就是说，不从整体最优上加以考虑，他所做出的是在某种意义上的局部最优解。

## 121. 买卖股票的最佳时机
---
[原题链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

> 如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

```js
var maxProfit = function(prices) {
    var result = 0;
    var min = prices[0];
    for(var i = 1; i < prices.length; i++){
        var profit = prices[i] - min;
        if(profit > 0){
            result = Math.max(result,profit);
        } else {
            min = prices[i];
        }
    }
    return result;
};

```


## 122. 买卖股票的最佳时机 II
---
[原题链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

> 设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

思路： 只要收益为+，就加入到收益结果中

```js
var maxProfit = function(prices) {
    var result = 0;
    for(var i = 1 ;i < prices.length; i++){
        var profit = prices[i] - prices[i - 1];
        if(profit > 0) result += profit;
    }
    return result;
};
```
