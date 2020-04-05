# 链表

## 2.两数相加
--- 
[原题链接](https://leetcode-cn.com/problems/add-two-numbers/)

> 给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。 

```javascript
var addTwoNumbers = function (l1, l2) {
    let head = new ListNode(0);
    let root = head;
    let carry = 0;
    while (l1 || l2 || carry) {
        let x,y;
        if (l1) {
            x = l1.val;
            l1 = l1.next;
        }
        if (l2) {
            y = l2.val;
            l2 = l2.next;
        }
        let result = x + y + carry;
        carry = ~~(result / 10);
        head.next = new ListNode(result % 10);
        head = head.next;
    }
    return root.next;
};
```


## 21. 合并两个有序链表
--- 
[原题链接](https://leetcode-cn.com/problems/add-two-numbers/)

> 将两个升序链表合并为一个新的升序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

```javascript
var mergeTwoLists = function(l1, l2) {
    if(!l1) return l2;
    if(!l2) return l1;
    var head = new ListNode();
    if(l1.val < l2.val){
        head = l1;
        head.next = mergeTwoLists(l1.next,l2);
    } else {
        head = l2;
        head.next = mergeTwoLists(l1,l2.next);
    }
    return head
};
```