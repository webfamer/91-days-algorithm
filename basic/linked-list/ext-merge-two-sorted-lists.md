# 21. 合并两个有序链表

https://leetcode-cn.com/problems/merge-two-sorted-lists/

## 题目描述

```
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-two-sorted-lists
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 方法 1: 迭代

### 思路

-   用两个指针分别遍历两个链表，比较两个指针节点的大小。
    -   将较小的那个节点加到新链表中，然后指针后移。
    -   较大的那个节点指针不动，下一轮继续比较。
-   如果两个链表长度不一样，继续遍历将多出来的节点加到新链表中就好了。

### 复杂度分析

-   时间复杂度：$O(N)$, N 为链表长度。
-   空间复杂度：$O(1)$。

### 代码

JavaScript Code

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function (l1, l2) {
    const dummy = new ListNode();
    let p1 = l1,
        p2 = l2,
        cur = dummy;

    while (p1 || p2) {
        if (!p2 || (p1 && p1.val <= p2.val)) {
            cur.next = new ListNode(p1.val);
            p1 = p1.next;
        } else {
            cur.next = new ListNode(p2.val);
            p2 = p2.next;
        }
        cur = cur.next;
    }

    return dummy.next;
};
```

## 方法 2: 递归

### 思路

-   如果 `l1 < l2`，那就把 l1 作为合并链表的头部返回，然后继续合并 `l1.next` 和 `l2` 之后的节点。
-   如果 `l2 < l1`，那就把 l2 作为合并链表的头部返回，然后继续合并 `l2.next` 和 `l1` 之后的节点。
-   递归出口：
    -   没有节点了。
    -   只剩一个节点，不用比较，返回那个节点就行。

### 复杂度分析

-   时间复杂度：$O(N)$, N 为链表长度。
-   空间复杂度：$O(N)$, N 为链表长度，递归栈的空间。

### 代码

JavaScript Code

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function (l1, l2) {
    if (!l1) return l2;
    if (!l2) return l1;

    if (l1.val < l2.val) {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    } else {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
};
```
