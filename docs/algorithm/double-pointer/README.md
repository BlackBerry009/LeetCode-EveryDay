# 双指针
## 11. 盛水最多的容器
--- 
[原题链接](https://leetcode-cn.com/problems/container-with-most-water/)

![img](../../static/img/water1.jpg)  

> 我们可以很直观的看出来，盛水最多的面积取决与两板之中最短的那个，所以我们可以设置前后指针，每次移动短的那一边，取最大面积即可。

```javascript
var maxArea = function(height) {
    let i = 0, j = height.length-1;
    let square, max = 0;
    while(j-i >= 1){
        if(height[i]>height[j]){
            square = height[j] * (j-i);
            j--;
        }else{
            square = height[i] * (j-i);
            i++;
        }
        max = Math.max(square,max);
    }
    return max;
};
```


## 15. 三数之和
--- 
[原题链接](https://leetcode-cn.com/problems/3sum/)


> 给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

思路： 排序 + 双指针， 因为不可以重复，所以我们扫描的时候过滤掉已经算过的元素。如果三数之和大于0，那么尾指针--，小于0，首指针++；

```javascript
var threeSum = function (nums) {
    var len = nums.length;
    var result = [];
    nums.sort((a, b) => a - b);
    for (var i = 0; i < len - 2; i++) {
        //首部去重
        if (i >= 1 && nums[i] === nums[i - 1]) {
            continue;
        }
        var L = i + 1;
        var R = len - 1;
        while (L < R) {
            var sum = nums[i] + nums[L] + nums[R];
            if (sum === 0) {
                result.push( [nums[i], nums[L], nums[R]] );
                while (L < R && nums[L] === nums[L + 1]) L++;
                while (L < R && nums[R] === nums[R - 1]) R--;
                L++;
                R--;
            } 
            else if(sum > 0) R--;
            else if(sum < 0) L++;
        }
    }
    return result;
};
```


## 16. 最接近的三数之和
--- 
[原题链接](https://leetcode-cn.com/problems/3sum-closest/)


> 给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

思路： 此题和三数之和类似，只不过每次存 结果与目标值差值的绝对值最小 的元素

```javascript
var threeSumClosest = function(nums, target) {
    nums.sort( (a,b) => a - b);
    var len = nums.length;
    var result = nums[0] + nums[1] + nums[2];
    for(var i = 0; i < len - 2; i++){
        var L = i + 1;
        var R = len - 1;
        while(L < R){
            var sum = nums[i] + nums[L] + nums[R];
            if(Math.abs(result - target) > Math.abs(sum -target)){
                result = sum;
            } 
            if(sum == target) return result;
            if(sum > target) R--;
            if(sum < target) L++;
        }
    }
    return result
};

```