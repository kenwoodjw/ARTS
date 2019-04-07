### ARTS  分享第1周

#### Algorithm

929. Unique Email Addresses

     level: Easy


Every email consists of a local name and a domain name, separated by the @ sign.

For example, in alice@leetcode.com, alice is the local name, and leetcode.com is the domain name.

Besides lowercase letters, these emails may contain '.'s or '+'s.

If you add periods ('.') between some characters in the local name part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, "alice.z@leetcode.com" and "alicez@leetcode.com" forward to the same email address.  (Note that this rule does not apply for domain names.)

If you add a plus ('+') in the local name, everything after the first plus sign will be ignored. This allows certain emails to be filtered, for example m.y+name@email.com will be forwarded to my@email.com.  (Again, this rule does not apply for domain names.)

It is possible to use both of these rules at the same time.

Given a list of emails, we send one email to each address in the list.  How many different addresses actually receive mails? 

 

Example 1:

Input: ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
Output: 2
Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails

```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        def parse(email):
            local,domain = email.split('@')
            local = local.split('+')[0].replace('.',"")
            return f"{local}@{domain}"
        return len(set(map(parse, emails)))
```

#### Review

https://medium.com/@kent.rancourt/go-pointers-why-i-use-interfaces-in-go-338ae0bdc9e4

go 为什么使用interface？

1,等级设定：

使用接口，方法或行为的集合在任何语言 ，创建一个抽象层在函数和调用者间，使用接口，您可以实现许多其他方式无法实现的功能。例如，您可以创建多个调用代码的组件，这些组件可以以统一的方式进行交互，即使这些组件的底层实现相差很大。这样就可以在编译时交换实现公共接口的组件，甚至在运行时动态地交换组件。

2.go没有构造函数

构造函数允许用户定义类型的作者（在许多OO语言中，一个类）
```golang
#widgets.go
package widgets

type Widget struct{
    id string
}

func (w Widget) ID() string{
    return w.id
}
```

```golang
package main

import (
    "fmt"
    "github.com/krancour/widgets"
)

func main(){
    w : = widgets.Widget{}
    fmt.Println(w.ID())
}
```
如果运行此示例，（可能）不足为奇的结果是打印的标识符是空字符串 - 因为它从未初始化，空字符串是字符串的“零值”。

增加类似构造函数来初始化
```golang
package widgets

import uuid "github.com/satori/go/uuid"

type Widget struct{
    id string
}

func NewWidget() Widget{
    return Widget{
        id: uuid.NewV4().String(),
    }   
}

func (w Widget) ID()string{
    return w.id
}
```

3,使用interface

```golang
package widgets

import uuid "github.com/satori/go.uuid"

// Widget is a ...
type Widget interface {
	// ID returns a widget's unique identifier
	ID() string
}

type widget struct {
	id string
}

// NewWidget() returns a new Widget
func NewWidget() Widget {
	return widget{
		id: uuid.NewV4().String(),
	}
}

func (w widget) ID() string {
	return w.id
}

```

#### Tip

为什么python存在GIL锁？
由于CPython实现的内存管理不是线程安全的。比如修改一个字典的值，如果不是线程安全，就可能导致错误，所以需要加锁。

官方wiki

**https://wiki.python.org/moin/GlobalInterpreterLock**



#### Share

为什么Python不用设计模式？

https://mp.weixin.qq.com/s/HMZ0UJCGOS4GihjX_A5iNw

