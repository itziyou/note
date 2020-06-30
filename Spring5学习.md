# Spring5学习

### 62集，一天看5集    12天看完

day1	周三	1-5

day2	周四	6-10

day3	周五	11-15

day4	周六	16-25

day5	周日	26-30

day6	周一	31-35

day7	周二	36-40

day8	周三	45-50

day9	周四	51-55

day10	周五	56-62



62/5 = 12天

P7<br/>

## Spring框架概述

1. Spring是轻量级的开源的JavaEE框架
2. Spring可以解决企业应用开发的复杂性
3. Spring有两个核心部分：IOC和AOP
   1. IOC：控制反转，把创建对象过程交给Spring管理
   2. AOP：面向切面，不修改源代码进行功能增强
4. Spring特点
   1. 方便解耦，简化开发
   2. AOP编程支持
   3. 方便程序测试
   4. 方便和其他框架整合
   5. 方便进行事务操作
   6. 降低API开发难度

## IOC容器

### IOC底层原理

1. 什么是IOC
   1. 控制反转，把对象创建和对象之间的调用过程，交给Spring进行管理
   2. 使用IOC的目的：降低耦合度
2. IOC底层原理
   1. xml解析、工厂模式、反射

### IOC接口（BeanFactory）

1. IOC思想基于IOC容器完成，IOC容器底层就是对象工厂
2. Spring提供IOC容器实现的两种方式：（两个接口）
   1. BeanFactory：IOC容器的基本实现，是Spring内部的使用接口，不提供开发人员使用（加载配置文件时不会创建对象，在获取对象（使用）才去创建对象）
   2. ApplicationContext：BeanFactory的子接口，提供更多更强大的功能，一般由开发人员进行使用（加载配置文件的时候会把在配置文件的对象进行创建）
3. ApplicationContext接口的两个实现类
   1. ClassPathXmlApplicationContext 采用相对路径方式加载xml
   2. FileSystemXmlApplicationContext 采用绝对路径方式加载xml

### IOC操作Bean

1. 什么是Bean管理
   1. Bean管理指的是两个操作：Spring创建对象、Spring注入属性

