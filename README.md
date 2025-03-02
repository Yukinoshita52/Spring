[toc]

# Spring

>  本笔记基于[尚硅谷讲解视频](https://www.bilibili.com/video/BV1AP411s7D7/?spm_id_from=333.337.search-card.all.click&vd_source=31d39c465d959f9ebfb4e20fc1ca0a9d)作了一定修改。
>
> 原笔记链接请访问：[wolai链接](https://www.wolai.com/oacbJpH1wPzGNoMAVnoELR)。感谢atguigu提供的优秀教程及笔记。

TODOS：

- [ ] 

| 核心点              | 掌握目标                                           |
| ------------------- | -------------------------------------------------- |
| spring框架理解      | spring家族和spring framework框架                   |
| spring核心功能      | ioc/di , aop , tx                                  |
| **spring ioc / di** | **组件管理、ioc容器、ioc/di , 三种配置方式**       |
| spring aop          | aop和aop框架和代理技术、基于注解的aop配置          |
| spring tx           | 声明式和编程式事务、动态事务管理器、事务注解、属性 |

## 一、技术体系结构

### 1.1 总体技术体系

- 单一架构

    一个项目，一个工程，导出为一个war包，在一个Tomcat上运行。也叫all in one。

    <img src="./imgs/image.png" style="zoom:80%;" />

    单一架构，项目主要应用技术框架为：Spring , SpringMVC , Mybatis
- 分布式架构

    一个项目（对应 IDEA 中的一个 project），拆分成很多个模块，每个模块对应 IDEA 中的一个 module。每一个工程都是运行在自己的 Tomcat 上。模块之间可以互相调用。每一个模块内部可以看成是一个单一架构的应用。

    ![](./imgs/image-1.png)

    分布式架构，项目主要应用技术框架：SpringBoot (SSM), SpringCloud , 中间件等

### 1.2 框架概念和理解

框架( Framework )是一个集成了基本结构、规范、设计模式、编程语言和程序库等基础组件的软件系统，它可以用来构建更高级别的应用程序。框架的设计和实现旨在解决特定领域中的常见问题，帮助开发人员更高效、更稳定地实现软件开发目标。

<img src="./imgs/image-2.png" style="zoom: 33%;" />

框架的优点包括以下几点：

1. 提高开发效率：框架提供了许多预先设计好了的组件和工具，能够帮助开发人员快速进行开发。相较于传统手写代码，在框架提供的规范化环境中，开发者可以更快地实现项目的各种要求。
2. 降低开发成本：框架的提供标准化的编程语言、数据操作等代码片段，避免了重复开发的问题，降低了开发成本，提供深度优化的系统，降低了维护成本，增强了系统的可靠性。
3. 提高应用程序的稳定性：框架通常经过了很长时间的开发和测试，其中的许多组件、代码片段和设计模式都得到了验证。重复利用这些组件有助于减少bug的出现，从而提高了应用程序的稳定性。
4. 提供标准化的解决方案：框架通常是针对某个特定领域的，通过提供标准化的解决方案，可以为开发人员提供一种共同的语言和思想基础，有助于更好地沟通和协作。

框架的缺点包括以下几个方面：

1. 学习成本高：框架通常具有特定的语言和编程范式。对于开发人员而言，需要花费时间学习其背后的架构、模式和逻辑，这对于新手而言可能会耗费较长时间。
2. 可能存在局限性：虽然框架提高了开发效率并可以帮助开发人员解决常见问题，但是在某些情况下，特定的应用需求可能超出框架的范围，从而导致应用程序无法满足要求。开发人员可能需要更多的控制权和自由度，同时需要在框架和应用程序之间进行权衡取舍。
3. 版本变更和兼容性问题：框架的版本发布和迭代通常会导致代码库的大规模变更，进而导致应用程序出现兼容性问题和漏洞。当框架变更时，需要考虑框架是否向下兼容，以及如何进行适当的测试、迁移和升级。
4. 架构风险：框架涉及到很多抽象和概念，如果开发者没有足够的理解和掌握其架构，可能会导致系统出现设计和架构缺陷，从而影响系统的健康性和安全性。

站在文件结构的角度理解框架，可以将框架总结：**框架 = jar包+配置文件**

<img src="./imgs/image-3.png" style="zoom:80%;" />

莎士比亚说,"一千个观众眼中有一千个哈姆雷特" 即仁者见仁,智者见智.说每个人都会对作品有不同的理解，每个人对待任何事物都有自己的看法，同样的技术解决同样的问题会产生不同流程和风格的解决方案，而采用一种框架其实就是限制用户必须使用其规定的方案来实现，可以降低程序员之间沟通以及日后维护的成本！

常用的单一架构JavaEE项目框架演进，从SSH、SSH2过渡到了SSM：SpringMVC、Spring、MyBatis。

总之，框架已经对基础的代码进行了封装并提供相应的API，开发者在使用框架是直接调用封装好的API可以省去很多代码编写，从而提高工作效率和开发速度。

## 二、SpringFramework介绍

### 2.1 Spring和SpringFramework概念

[Spring官网](https://spring.io/)

- **广义的 Spring：Spring 技术栈**（全家桶）

  广义上的 Spring 泛指以 Spring Framework 为基础的 Spring 技术栈。

  经过十多年的发展，Spring 已经不再是一个单纯的应用框架，而是逐渐发展成为一个由多个不同子项目（模块）组成的成熟技术，例如 Spring Framework、Spring MVC、SpringBoot、Spring Cloud、Spring Data、Spring Security 等，其中 Spring Framework 是其他子项目的基础。

  这些子项目涵盖了从企业级应用开发到云计算等各方面的内容，能够帮助开发人员解决软件发展过程中不断产生的各种实际问题，给开发人员带来了更好的开发体验。

- **狭义的 Spring：Spring Framework**（基础框架）

  狭义的 Spring 特指 Spring Framework，通常我们将它称为 Spring 框架。

  Spring Framework（Spring框架）是一个开源的应用程序框架，由SpringSource公司开发，最初是为了解决企业级开发中各种常见问题而创建的。它提供了很多功能，例如：依赖注入（Dependency Injection）、面向切面编程（AOP）、声明式事务管理（TX）等。其主要目标是使企业级应用程序的开发变得更加简单和快速，并且Spring框架被广泛应用于Java企业开发领域。

  Spring全家桶的其他框架都是以SpringFramework框架为基础！

- **对比理解：**

  QQ 和 腾讯

  腾讯 = Spring

  QQ = SpringFramework

### 2.2 SpringFrameword主要功能模块

SpringFramework框架结构图：

<img src="./imgs/image-4.png" style="zoom: 25%;" />

| 功能模块       | 功能介绍                                                    |
| -------------- | ----------------------------------------------------------- |
| Core Container | 核心容器，在 Spring 环境下使用任何功能都必须基于 IOC 容器。 |
| AOP&Aspects    | 面向切面编程                                                |
| TX             | 声明式事务管理。                                            |
| Spring MVC     | 提供了面向Web应用程序的集成功能。                           |

### 2.3 SpringFramework核心优势

1. 丰富的生态系统：Spring 生态系统非常丰富，支持许多模块和库，如 Spring Boot、Spring Security、Spring Cloud 等等，可以帮助开发人员快速构建高可靠性的企业应用程序。
2. 模块化的设计：框架组件之间的松散耦合和模块化设计使得 Spring Framework 具有良好的可重用性、可扩展性和可维护性。开发人员可以轻松地选择自己需要的模块，根据自己的需求进行开发。
3. 简化 Java 开发：Spring Framework 简化了 Java 开发，提供了各种工具和 API，可以降低开发复杂度和学习成本。同时，Spring Framework 支持各种应用场景，包括 Web 应用程序、RESTful API、消息传递、批处理等等。
4. 不断创新和发展：Spring Framework 开发团队一直在不断创新和发展，保持与最新技术的接轨，为开发人员提供更加先进和优秀的工具和框架。

因此，这些优点使得 Spring Framework 成为了一个稳定、可靠、且创新的框架，为企业级 Java 开发提供了一站式的解决方案。

Spring 使创建 Java 企业应用程序变得容易。它提供了在企业环境中采用 Java 语言所需的一切，支持 Groovy 和 Kotlin 作为 JVM 上的替代语言，并且可以根据应用程序的需求灵活地创建多种架构。**从Spring Framework 6.0.6开始，Spring 需要 Java 17+。**

## 三、Spring IoC容器和核心概念

### 3.1 组件和组件管理概念

#### 3.1.1 什么是组件

回顾常规的三层架构处理请求流程：

![](./imgs/image-5.png)

整个项目就是由各种组件搭建而成的：

![](./imgs/image-6.png)

#### 3.1.2 我们的期待

- 有人替我们创建组件的对象
- 有人帮我们保存组件的对象
- 有人帮助我们自动组装
- 有人替我们管理事务
- 有人协助我们整合其他框架
- ......

#### 3.1.3 Spring 充当组件的管理角色（IoC）

那么谁帮我们完成我们的期待，帮我们管理组件呢？

当然是Spring 框架了！

组件可以完全交给Spring 框架进行管理，Spring框架替代了程序员原有的new对象和对象属性赋值动作等！

Spring具体的组件管理动作包含：

- 组件对象实例化
- 组件属性属性赋值
- 组件对象之间引用
- 组件对象存活周期管理
- ......

我们只需要编写元数据（配置文件）告知Spring 管理哪些类组件和他们的关系即可！

注意：组件是映射到应用程序中所有可重用组件的Java对象，应该是可复用的功能对象！

- 组件一定是对象
- 对象不一定是组件

综上所述，Spring 充当一个组件容器，创建、管理、存储组件，减少了我们的编码压力，让我们更加专注进行业务编写！

#### 3.1.4 组件交给Spring管理优势

1. 降低了组件之间的耦合性：Spring IoC容器通过依赖注入机制，将组件之间的依赖关系削弱，减少了程序组件之间的耦合性，使得组件更加松散地耦合。
2. 提高了代码的可重用性和可维护性：将组件的实例化过程、依赖关系的管理等功能交给Spring IoC容器处理，使得组件代码更加模块化、可重用、更易于维护。
3. 方便了配置和管理：Spring IoC容器通过XML文件或者注解，轻松的对组件进行配置和管理，使得组件的切换、替换等操作更加的方便和快捷。
4. 交给Spring管理的对象（组件），方可享受Spring框架的其他功能（AOP,声明事务管理）等

### 3.2 Spring Ioc容器和容器实现

#### 3.2.1 普通和复杂容器

**普通容器**

  生活中的普通容器

  <div style="text-align: center;">
    <img src="./imgs/img002.png" alt="Your Image" style="transform: scale(0.5);">
</div>

  > 普通容器只能用来存储，没有更多功能。

  程序中的普通容器

  - 数组
  - 集合：List
  - 集合：Set

**复杂容器**

  生活中的复杂容器

  ![](https://secure2.wostatic.cn/static/9DRSuBo1GprKVtd5Gu2GqU/img003.png?auth_key=1740881931-xmKqBZs5ABDDgs7JvTxPS7-0-b023b247ced4e16540feefd6c3b2dac2)

  > 政府管理我们的一生，生老病死都和政府有关。

  程序中的复杂容器

  Servlet 容器能够管理 Servlet(init,service,destroy)、Filter、Listener 这样的组件的一生，所以它是一个复杂容器。

| 名称       | 时机                                                         | 次数 |
| ---------- | ------------------------------------------------------------ | ---- |
| 创建对象   | 默认情况：接收到第一次请求  修改启动顺序后：Web应用启动过程中 | 一次 |
| 初始化操作 | 创建对象之后                                                 | 一次 |
| 处理请求   | 接收到请求                                                   | 多次 |
| 销毁操作   | Web应用卸载之前                                              | 一次 |


我们即将要学习的 SpringIoC 容器也是一个复杂容器。它们不仅要负责创建组件的对象、存储组件的对象，还要负责调用组件的方法让它们工作，最终在特定情况下销毁组件。

总结：Spring管理组件的容器，就是一个复杂容器，不仅存储组件，也可以管理组件之间依赖关系，并且创建和销毁组件等！

### 3.3 Spring IoC / DI概念总结

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

## 三层架构（以及其他旧内容）

1. controller
2. service
3. dao

> JdbcTemplate需要Druid连接池，Druid连接池需配置4个信息（驱动、url、用户名、密码）

## Spring-IoC/Di 概念+实践

概念：见上

实践：

1. XML配置：

   - 写在.xml文件内，主要写<bean id="" class=""
   - 如要注入属性信息，在<bean> </bean>中间加入<properties name="" value/ref二选一
   - 如要引入外部配置文件（e.g. jdbc.properties）使用命名空间<context:property-placeholder
   - 此时IoC容器选择ClassPathXmlApplicationContext

2. 注解方式配置：

   - 使用注解如——@Component、@Service、@Controller、@Repository以标记Ioc
   - 使用注解如——@Autowired、@Qualifier、@Resource、@Value标记di
   - 此时IoC容器选择ClassPathXmlApplicationContext
   - ps：第三方类需使用xml或者配置类方式（不能写上述注解解决）

3. 配置类方式配置：

   - 配置类是指有@Configuration标注的类
   - 标记IoC注解：@Component,@Service,@Controller,@Repository 
   2. 标记DI注解：@Autowired @Qualifier @Resource @Value
   3. <context:component-scan标签指定注解范围使用@ComponentScan(basePackages = {"com.atguigu.components"})替代
   4. <context:property-placeholder引入外部配置文件使用@PropertySource({"classpath:application.properties","classpath:jdbc.properties"})替代
   5. <bean 标签使用@Bean注解和方法实现

   - 此时IoC容器选择AnnotationConfigApplicationContext

## Spring-AOP

- AOP：概念理解——面向切面编程
  - 切面 = 切点 + ？
  - 底层使用技术：cglib、？（前者产生一个代理类，是目标类的子类；后者在ioc容器中产生的类对象，是与目标类实现了同一个接口的）
    - 因此总结：前者调用ioc容器获取bean对象时，需要使用目标类本身来接收这个bean对象；后者调用ioc容器获取bean对象时，只能使用这个接口lai'jie'sho

## Spring-Tx

声明式事务

