### ARTS分享第六周

####  algorithms

level: easy

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
        res =[]
        self.dfs(root,0,res)
        return res

    def dfs(self,root,level,res):
        if root:
            if len(res) <level +1:
                res.insert(0,[])
            res[-(level+1)].append(root.val)
            self.dfs(root.left,level+1,res)
            self.dfs(root.right,level+1,res)
```


#### Review
python在netflix内部的使用
https://medium.com/netflix-techblog/python-at-netflix-bba45dae649e
1.open-connect
 open-connect 是netfilx的cdn平台，设计，构建和操作这个CDN基础设施需要各种软件系统，其中很多都是用Python编写的。
 构成CDN的大部分网络设备主要由python应用程序管理,这些应用程序跟踪网络设备的库存，那些设备，那些型号，那么硬件组件，
 位于那些站点。python长期是网络领域的流行语言。

2.Demand Engineering
 Demand Engineering负责Netflix云的区域故障转移，流量分配，容量运营和车队效率，协调故障转移的服务使用numpy和scipy
 来执行数值分析，boto3用于更改我们的AWS基础架构，rq用于运行异步工作负载，我们将它们全部包含在Flask API的薄层中  

3.核心
CORE团队在我们的警报和统计分析工作中使用Python。 我们依靠许多统计和数学库（numpy，scipy，ruptures，pandas）
来帮助在我们的警报系统指示问题时自动分析1000个相关信号。 我们开发了一个时间序列关联系统，用于团队内部和外部，
以及分布式工作人员系统，以并行化大量分析工作，以快速提供结果

4.监控，警报和自动修复
5.信息安全
6.个性化算法
7.机器学习基础设施
8.Jupyter notebooks
9.Big Data Orchestration团队负责提供所有服务和工具来安排和执行ETL和Adhoc管道。业务流程服务的许多组件都是用Python编写的。
10.用于实验的科学计算团队正在为科学家和工程师创建一个分析AB测试和其他实验的平台

#### Tip

pv描述的是持久化存储数据卷,这个api对象主要定义的是一个持久化存储在宿主机
上的目录,比如一个 NFS 的挂载目录。通常情况下,PV 对象是由运维人员事先创建在
 Kubernetes 集群里待用的。比如,运维人员可
以定义这样一个 NFS 类型的 PV,如下所示:
```
apiVersion: v1
kind: PersistentVolume
metadata；
    name: nfs
spec:
    storgeClassName: manual
    capacity: 
        storage: 1Gi
    accessModes:
        - ReadWriteMany

    nfs:
        server： 10.244.1.4
        path: "/"

```

PVC描述的是Pod希望使用的持久性存储的属性，比如Vloume存储的大小，可读写属性
```
apiVersion: v1
kind :PersistentVloumeClaim
metadata:
    name: nfs
spec:
    accessMode:
        - ReadWriteMany
    storgeClassName: manual
    resoureces:
        requests:
            storage: 1Gi


```
比如,你在创建 Pod 的时候,系统里并没有合适的 PV 跟它定义的 PVC 绑定,也就是说此时容
器想要使用的 Volume 不存在。这时候,Pod 的启动就会报错。
所以在 Kubernetes 中,实际上存在着一个专门处理持久化存储的控制器,叫作 Volume
Controller。这个 Volume Controller 维护着多个控制循环,其中有一个循环,扮演的就是撮
合 PV 和 PVC 的“红娘”的角色。它的名字叫作 PersistentVolumeController。
PersistentVolumeController 会不断地查看当前每一个 PVC,是不是已经处于 Bound(已绑
定)状态。如果不是,那它就会遍历所有的、可用的 PV,并尝试将其与这个“单身”的 PVC
进行绑定。这样,Kubernetes 就可以保证用户提交的每一个 PVC,只要有合适的 PV 出现,它
就能够很快进入绑定状态,从而结束“单身”之旅。



#### Share
技术路线的选择重要但不具有决定性 - 孟岩 - CSDN博客
https://blog.csdn.net/myan/article/details/3247071