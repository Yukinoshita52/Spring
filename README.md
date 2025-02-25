# Spring
>  Spring学习笔记
>
> 不完全正确版（想到什么写什么（后续再做系统整理、复习））

## Spring框架理解以及一些关键概念

1. Spring是什么？（框架=.jar+文档(可配置的，可自定义配置文件的)）
   - 同时还要分清楚俗话讲地Spring是指什么？可以指广义地指这个框架大家族，也可以狭义的指Spring Framework这个框架……
2. Ioc是什么？控制反转（通俗讲就是把创建一个类、实例化的权力交给了Spring中的容器来管理）
3. Di是什么？依赖注入（emm……大概是给某个类中的某个对象赋值（有参构造的的参数赋值过程也是di、setter方法也是di）【肯定有表达不准确的地方】）
4. bean是什么？（翻译：组件）

## Spring框架配置方案

1. Spring中有一些接口和实现类
   - Bean...
   - ApplicationContext
   - ClassPathXmlApplicationContext、FileSystemXmlApplicationContext、WebApplicationContext、?

2. 在以.xml格式配置的方案中，里面内容怎么写？（先是如何快速创建这样一个.xml文件）
   - 要创建一个组件，就写一个<bean id="" class= "".../>
   - 当然分组件类型的：
     1. 默认构建<bean id="" class=""/>即可
     2. 静态工厂构造
     3. 非静态工厂构造
     4. 有参数构造（涉及到di了）（ps：上述三种还只是创建ioc容器）

## 如何获取（容器中的）Bean

1. 第一种
2. 第二种
3. 第三种

> 刚学过就不立马回忆了……
