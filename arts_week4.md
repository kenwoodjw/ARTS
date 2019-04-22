### ARTS分享第四周

#### Algorithm
[35] Search Insert Position 

https://leetcode.com/problems/search-insert-position/description/

Tags: algorithms array binary-search 

Langs: c cpp csharp golang java javascript kotlin php python python3 ruby rust scala swift 

* algorithms
* Easy (40.64%)
* Total Accepted: 385.5K
* Total Submissions: 947.5K
* Testcase Example: '[1,3,5,6]\n5'

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. 

You may assume no duplicates in the array. 

Example 1: 


Input: [1,3,5,6], 5 
Output: 2 


Example 2: 


Input: [1,3,5,6], 2 
Output: 1 


Example 3: 


Input: [1,3,5,6], 7 
Output: 4 


Example 4: 


Input: [1,3,5,6], 0 
Output: 0 

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)-1
        while left <= right:
            mid = int((left +right)/2)
            if nums[mid]== target:
                return mid
            elif nums[mid] <target:
                left = mid +1
            else:
                right = mid -1
        return left
```
#### Review

https://www.projectatomic.io/blog/2018/02/reintroduction-podman/

重新介绍podman

Podman曾经是CRI-O project中的一部分,后来被分离出成为一个独立project,

[libpod]: https://github.com/containers/libpod

Podman(Pod Manager)的目标是提供一个跟docker相似体验的container CLI,提供给使用者创立和运行c

container

Why Podman?

没有肥大的Daemons

Podman不像docker Engine一样有一个daemon

在使用Docker CLI的时候，Dcoker CLI会透过API去跟Docker Engine说[我要开一个container]，这时

Docker Engine才会透过OCI Contianer runtime(预设是runc)来启动一个container，这代表Container

的process 不会是Docker CLI的child process,而是Docker Engine的child process.

Podman就不使用daemon,而是直接透过OCI runtime(预设也是runc)来开启container,所以container

 process 会直接是podman的child process.这比较像Linux 的fork/exec的模式，这也代表系统管理员可以知道那个container process到底是谁启动的，同时，如果利用cgroups对podman command 做一些限制，同样的所有container也会被这些限制，

这个模式也使podman可以透过podman 放进systemd unit file来利用systemd中的一些进阶功能。

例如,systemd中可以透过notify去实现serivice的启动顺序，当有container中的service需要在其他service之前先启动的话，后续的service会等待container送一个notify signal给systemd，确认container已经启动完成之后才会开始运行。透过Docker CLI这件事是没办法去实现的，但是Podman会forward systemd的消息给child process,所以container process在启动完成后可以notify systemd它已经准备运作了。

#### Tip

链表在redis中的应用非常广泛，列表的底层实现之一就是链表。当一个列表键包含了数量比较多的元素，又或者列表中包含的元素都是比较长的字符串时，redis就会使用链表作为底层实现。发布与订阅，慢查询，监视器等功能也用到了链表

```c
typedef struct listNode {
    //前置节点
    struct listNode *prev;
    //后置节点
    struct listNode *next;
    //节点的值
    void * value;
}listNode
```

特性总结:双端：链表节点带有prev和next指针，获取某个节点的前置节点和后置节点的复杂度都是O(1)

无环： 表头节点的prev指针和表尾节点的next指针都指向NULL，对链表的访问以NULL为终点。

带表头指针和表尾指针：通过list结构的head指针和tail指针，程序获取链表的表头节点和表尾节点的复杂度为O(1)

#### Share

作者分享他成为前端工程师的四周年回顾。

<https://medium.com/hulis-blog/4-years-review-7fb7edc52687>