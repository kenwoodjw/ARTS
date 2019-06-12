#### Althgoimal
level: easy
Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

Example 1:

Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
Example 2:

Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false

```python
#
# @lc app=leetcode id=100 lang=python3
#
# [100] Same Tree
#
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if p and q:
            return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        return p is q
```
#### Reivew
kafka所有你需要知道的

https://medium.com/hacking-talent/kafka-all-you-need-to-know-8c7251b49ad0
kafka是一个发布/订阅消息系统，允许生产者写入记录，能够被一个或多个消费者读取，当消息发送到kafka,消息不允许删除或修改
records被推送到topics,topics就像一个(channel)频道，所有records都存储在channel,消费者可以订阅或多个频道，kafka有一个保留期，他会根据设置时间和大小存储record，并且指定topic
消费者使用消费组的标签，一个topic只能被消费组的一个实例消费
broker:kafka是分布式的，分布式的node叫做broker,负责records的存储，接受，发送，broker从生产者接受records,分配offset,持久化到硬盘。
运行kafka首先需要zookeeper,zookeeper的作用:
.controller选举，controller是broker其中之一，负责维护所有partitions(分区)的leader和follower的关系，当node崩掉之后，zookeeper负责选举新的controller,确保只有一个controller
.集群成员，zookeeper维护正在运行的所有broker list
.Topic 配置，topic存放在那里，有多少个partitions(分区)，有多少副本，谁是leader,每个topic的配置
.配额，每个客户端运行读取多少数据
.访问控制

深入
随着topic变大，它们被拆分为partitions(分区)，所以records被放到topic的单个partitions,消费者可以选择分区，不然由kafka选择
分区由单个broker拥有，叫做分区的leader, 分区可以被复制给多个broker,提供分区的冗余

#### Tips
keepalive原理？
#### Share