#### Algorithm

level: easy
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

```python
#
# @lc app=leetcode id=21 lang=python3
#
# [21] Merge Two Sorted Lists
#
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1 or not l2:
            return l1 or l2
        if l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return  l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return  l2
```

#### Review

#### Tips
迭代和递归的区别
```lisp
# 两堆弹珠相加，从一堆挪到另一堆
(define (+ x y)
(if  (= x 0)
      y
     (+ (-1 + x) (1+ y))))
# 直接看最后的表达式
空|(+ 3 4)
间|(+ 2 5)
复|(+ 1 6)
杂|(+ 0 7)
  _________时间复杂度
迭代的概念：a - b(计算3+4)- c(计算2+5) - d(计算1+6)- e(计算0+7)
```
```lisp
两堆弹珠相加，先搬空一堆，再慢慢放入另一堆
(define ( + x y)
(if (= x 0)
    y
    (1 + (+(-1 + x) y)))

(+ 3 4)
(1 + (+ 2 4))
(1 + (1 +(+ 1 4)))
(1 + (1+ (1 + (+ 0 4)))
(1 + (1 +(1 +4)))
(1 + (1 + 5))
(1 + 6)
```
递归的概念: a- b(计算1+(+2 4 )) - c(计算(1 +(+ 1 4)))-d((1+(1+(+ 0 4))))需要回传
#### Share
用go写的kv database 
https://github.com/xujiajun/nutsdb