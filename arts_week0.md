### ARTS 分享第0周
耗子哥的专栏买了很久，看一部分，也有关注到arts，但是一直没有付出行动，希望培养持续学习的能力，把学习当成一种习惯。

#### Algorithm

**2.Add Two Numbers**

level: Medium

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**:

**Input**: (2 -> 4 -> 3) + (5 -> 6 -> 4)

**Output**: 7 -> 0 -> 8

**Explanation**: 342 + 465 = 807.
```python
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        num1 = str(l1.val)
        num2 = str(l2.val)
        while l1.next or l2.next:
            if l1.next:
                num1 = str(l1.next.val) + num1
                l1 = l1.next
            if l2.next:
                num2 = str(l2.next.val) + num2
                l2 = l2.next
        result = [ListNode(int(ele)) for ele in str(int(num1) + int(num2))[::-1]]
        for index, i in enumerate(result[1:], 1):
            result[index - 1].next = i

        return result[0]
```
golang version
```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    result := &ListNode{}
	current := result
	each_sums := 0

	for l1 != nil || l2 != nil || each_sums != 0{
		if l1 != nil{
			each_sums += l1.Val
			l1 = l1.Next
		}
		if l2 != nil{
			each_sums += l2.Val
			l2 = l2.Next
		}
		current.Next = &ListNode{Val: each_sums % 10}
		each_sums /= 10
		current = current.Next
	}

	return result.Next
}
```
#### Review

https://dzone.com/articles/five-key-cloud-technologies-for-kubernetes


五个可以用于K8S的关键技术 文章介绍了可以构建在K8S之上的5个模块，分别涉及监控(prometheus)，治理(lstio)，容器存储，集成流程(weave flux)和服务管理。K8S加上这5个模块，可以组成一套非常完善的且可扩展的基础架构，可以作为基础运维的起点


#### Tips
数据一致性问题：面试经常被问到redis 与mysql 数据如何保持同步
1.写：先写mysql，再写redis

2.基于binlog使用mysql_udf_redis,将数据库中的数据同步到Redis

缓存更新： 先更新数据库，成功后，让缓存失效。(Cache Aside)

https://coolshell.cn/articles/17416.html


#### Share
#### 为什么我们需要pod？
Pod的实现原理： 首先，关于Pod最重要的一个事实是：它只是一个逻辑概念。Pod，其实是一组共享了某些资源的容器。具体的说，Pod里的所有容器，共享的是同一个Network Namespace，并且可以声明共享同一个Volume。在kubernetes项目里，Pod的实现需要使用一个中间容器，这个容器叫做Infra容器（pause)，则通过Join Network Namespace的方式,与Infra容器关联在一起。

明白了Pod的实现原理后，我们再来讨论“容器设计模式”，就容易多了。Pod这种“超亲密关系”容器的设计思想，实际上就是希望，当用户想在一个容器里跑多个功能并不相关的应用时，应该优先考虑它们是不是更应该被描述成一个Pod里的多个容器。

第一个最典型的例子是：war包与web服务器

我们现在有一个Java Web应用的WAR包，它需要被放在Tomcat的webapps目录下运行起来。

假如用docker来做这件事情

*.一种方法是，把WAR包直接放Tomcat镜像的webapps目录下，做成一个新的镜像运行起来，可是，如果你要更新WAR包的内容或要升级Tomcat镜像，就要重新制作一个新的发布镜像，非常麻烦

*.另一种方法是，你不管WAR包，永远只发布一个Tomcat容器，不过这个容器的webapps目录，就必须声明一个hostPath类型的Volume，从而把宿主机上的WAR包挂载进Tomcat容器中运行起来。不过，这样你就必须要解决一个问题，即：如何让每一台宿主机，都预先准备好这个存储WAR包的目录呢？这样来看，你只能独立维护一套分布式存储系统

实际上，有了Pod之后，我们可以把WAR包和Tomcat分别做成镜像，然后把它们作为一个Pod的两个容器“组合”在一起。

```
apiVersion: v1
kind: Pod
metadata:
   name: javaweb-2
spec:
  initContainers:
  - image: geektime/sample:v2
    name: war
    command: ["cp","/sample.war","/app"]
    volumeMounts:
    - mountPath: /app
      name: app-volume 
  containers:
   - image: geektime/tomcat:7.0
     name: tomcat
     command: ["sh","-c","/root/apache-tomcat-7.0.42-v2/bin/start.sh"]
     volumeMounts:
     - mountPath: /root/apache-tomcat-7.0.42-v2/webapps
       name: app-volume
    ports:
    - containerPort: 8080
      hostPort: 8001
  volumes:
  - name: app-volume
    emptyDir: {}
```
war包容器的类型不再是一个普通容器，而是一个Init Container类型的容器。在Pod中，所有Init Container定义的容器，都会比spec.containers定义的用户容器先启动。并且，Init Containers容器会按顺序逐一启动，而直到它们都启动并且退出了，用户容器才会启动。

所以，这个Init Container类型的WAR包容器启动后，我执行了一句"cp /sample.war/app",把应用的WAR包拷贝到/app目录下，然后退出。而后这个/app目录，就挂载了一个名叫app-volume的Volume。Tomcat容器，同样声明了挂载app-volume到自己的webapps目录下。所以，等Tomcat容器启动时，它的webapps目录下就一定会存在sample.war文件:这个文件正是WAR包容器启动时拷贝到这个Volume里面的，而这个Volume是被这两人容器共享的。

像这样，我们用一种”组合“的方式，解决了WAR包与Tomcat容器之间耦合关系的问题。
实际上，这个所谓的”组合“操作，正是容器设计模式里最常用的一种模式，它的名字叫： **sidecar**,顾名思义，sidecar指的就是我们可以在一个Pod中，启动一个辅助容器，来完成一些独立于主进程（主容器）之外的工作。

比如，在我们的这个应用Pod中，Tomcat容器是我们要使用的主容器，而WAR包容器的存在，只是为了给它提供一个WAR包而已。所以，我们用Init Container的方式优先运行WAR包容器，扮演了一个sidewar的角色。

第二个例子，则是容器的日志收集。

比如，我现在有一个应用，需要不断地把日志文件输出到容器的/var/log目录中。

这时，我就可以把一个Pod里的Volume挂载到应用容器的/var/log目录上。

然后，我在这个Pod里同时运行一个sidecar容器，它是声明挂载同一个Volume到自己的/var/log目录上。

这样，接下来sidecar容器就只需要做一件事，那就是不断从自己的/var/log目录里读取日志文件，转发到MongoDB或者Elasticsearch中存储起来，这样，一个最基本的日志收集工作就完成了

不要忘记，Pod的另一个重要特性是，它的所有容器都共享同一个Network Namespace。这就使得很多与Pod网络相关的配置和管理，也都可以交给sidecar完成，而完全无须干涉用户容器，这里最典型的例子莫过于lstio这个微服务治理项目。