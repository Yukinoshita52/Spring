# Spring
>  Spring学习笔记
>
> 不完全正确版（想到什么写什么（后续再做系统整理、复习））

- [ ] 待完善该部分笔记
- [ ] 待上传代码案例（还是用项目的形式吧）

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

