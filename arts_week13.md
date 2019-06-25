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
网络分层模式概念    
https://www.lifewire.com/layers-of-the-osi-model-illustrated-818017
OSI Model
第一层:物理层，使用电压，射频，脉冲或普通光传递信号
第二层:数据链路层，当物理层获得数据后，数据链路层检查数据并将其封装成帧
第三层: 网络层，在数据链路层上添加路由的概念，当数据到达网络层，检查每一帧中的源和目的地址，逻辑地址和物理地址的映射，ARP
第四层：传输层，常见的是tcp。错误恢复，流量控制，重传支持
第五层: 会话层，管理和拆除网络连接事件的顺序和流程
第六层: 表示层，处理消息数据的语法处理，支持应用层所需的格式转换，加密和解密
第7层: 应用层，为最终用户提供网络服务，比如HTTP协议
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