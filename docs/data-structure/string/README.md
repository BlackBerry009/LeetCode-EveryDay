# 字符串

## 3. 无重复最长字符串
--- 
[原题链接](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

>  给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

思想： 维护一个str变量，扫描字符串并添加进str中，如果str有重复的元素则进行截取。  

```javascript
var lengthOfLongestSubstring = function(s) {
    let result = 0;
    let str = '';
    for(var i = 0 ; i < s.length; i++){
        let index = str.indexOf(s[i]); 
        str += s[i]; 
        //处理str中有当前字符的情况
        if(index != -1){
            str = str.substring(index+1);
            result = Math.max(result,str.length);
        }
    }
    //处理只有一个字符的情况
    result = Math.max(result,str.length);
    return result;
};
```


## 5. 最长回文字符串
--- 
[原题链接](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

> 给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000

解一： 暴力法  

双层循环截取字符串，判断是否为回文。

```javascript
var longestPalindrome = function(s) {
    //判断是否为回文
    var isPalindrome = function (str){
        for(let i = 0, j = str.length - 1; i < j; i++,j--){
            if(str[i] != str[j]) return false;
        }
        return true;
    }
    let result = '';
    let str = '';
    for(let i = 0 ; i < s.length; i++){
        for(let j = i; j < s.length; j++){
            str = s.substring(i,j+1);
            //处理是回文字符串
            if(isPalindrome(str)){
                result = result.length > str.length ? result : str;
                // 暴力法会超出时间限制，要加个判断
                // if(result.length === s.length) return result;
            }
        }
    }
    return result;
};
```

## 14.最长公共前缀
--- 
[原题链接](https://leetcode-cn.com/problems/longest-common-prefix/)

> 编写一个函数来查找字符串数组中的最长公共前缀。如果不存在公共前缀，返回空字符串 ""。  
  
思想： 两两取公共前缀，再把结果作为新字符串往后轮询。

```javascript
var longestCommonPrefix = function(strs) {
    if(strs.length === 0) return '';
    var result = strs[0];
    for(var i = 1; i < strs.length; i++){
        for(var j = 0; j < result.length && j < strs[i].length; j++){
            if(result[j] != strs[i][j]){
                break;
            }
        }
        result = result.slice(0,j);
        if(!result){
            return '';
        }
    }
    return result;
};
```