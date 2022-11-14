---
title: “software design”
collection: notes
type: "design"
permalink: /notes/2022-Principe
venue: "Uniontech. Company"
date: 2022-11-14
location: "WuHan, China"
---

六大原则的英文首字母拼在一起就是SOLID（稳定的），所以也称之为SOLID原则

# 单一职责原则（Single Responsiblility Principle） 

只干与名称初衷相关的事，只负责干一件事或者一种事，例如run（），干跑的业务，就不要把会飞的业务逻辑写进去

# 开闭原则（Open Closed Principle） 

像类、模块、函数、接口等应该对扩展开放，对修改关闭

# 里氏替换原则（Liskov Substitution Principle） 

所有引用基类的地方必须可以替换成其子类对象

# 迪米特法则（又称最少知道原则，Law Of Demeter） 

如果两个实体类无直接关联，不应该发生直接的相互调用，应该通过第三方转发该调用，以提高模块的独立性

# 接口隔离原则（Interface Segregation Principle） 

1、客户端不应该依赖继承它不使用的接口

2、类间的依赖关系应该建立在最小粒度的接口上

# 依赖倒转原则（Dependence Inversion Principel） 

1、上层模块应该直接依赖底层模块，应该依赖抽象层

2、抽象不该依赖与细节（即具体实现），细节（即具体实现）应依赖于抽像

