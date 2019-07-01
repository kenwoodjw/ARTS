
#### Algorithm

Palindrome Number
level: easy
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        return str(x)==str(x)[::-1]
        
```

#### Review

#### Tip
flannel,calico,weave
host-gateway: three mode: UDP, xvlan, host-gw,  flannel througth flannel agent notify node refresh route table, two layer network，only change host machine route table
the route table message stoage in etcd
weave: improve flannel host-gateway, has own storage. udp,fastpass
calico: BGP route protocol equal have route machine in node, three layer network
pure three layer

node1(infra1)--- node(2)infra

node1: route
10.0.0.x  - eth0 -  next jump(mac address)
flannel subnet next jump is host machine ip
host two layer ping

calico: BGP: inside linux kernel,ip1- route1 -c -route2-b- ip2, brid,
route1 :
172.17.0.2 route2 c
route2:
172.17.0.2 B
172.17.0.3 C
BGP run a program throuth tcp transform route message
1.calico cni plugin:
2.felix daemonset  insert route table into host machine
3.bird bgp client
BGP trans route table, bgp client

daemonset:

istion share pod network namespace ,take 90% flow access to sidecar canary deploy


#### share
白话kubernetes网络
https://juejin.im/entry/599d33ad6fb9a0247804d430