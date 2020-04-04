# 数组

## 1.两数之和 
--- 
[原题链接](https://leetcode-cn.com/problems/two-sum/)

> 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

这里就不用暴力法解决啦，讲一下利用哈希进行的登记表办法。  

思想： 扫描一遍nums数组，对每个值所需要的另外一个值进行登记，并记住其索引。
```javascript
var twoSum = function (nums,target){
    var map = new Map();
    for (let i = 0; i < nums.length; i++) {
        //得到每个元素所需要的值
        const key = target - nums[i];
        //判断map中是否已有登记过的值
        if(map.has(key)){
            return [map.get(key),i]
        } else {
            map.set(nums[i],i)
        }
    }
}
```