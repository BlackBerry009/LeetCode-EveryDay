# 广度优先搜索

## 面试题 13. 机器人的运动范围
从  `[0,0]`开始，向右或者向下走，走过的加入已访问记录，一直遍历即可。  

!> 不可以直接扫描数组，挑出所有符合条件的组合  
 因为符合条件的不一定能够走到！！

!> m = 20,n = 20,k = 5  
 尽管[20,0]符合要求，[19,x]这一行过不去  

```js
var movingCount = function(m, n, k) {
    var arr = [[0,0]];
    var res = 0;
    var isVisited = {};
    var helper = (m,n,k,arr) => {
        if(arr.length === 0) return;
        let next = [];
        for(var i = 0 ; i < arr.length; i++){
            let [x,y] = arr[i];
            let key = x + '-' + y;
            if(x >= m || y >= n || isVisited[key] || (''+x+y).split('').reduce( (a,b) => ~~a + ~~b ) > k ){
                continue;
            }
            res++;
            isVisited[key] = true;
            next.push([x+1,y],[x,y+1]);
            helper(m,n,k,next);
        }
    }
    helper(m,n,k,arr);
    return res;
};
```