SpringBoot是基于Spring框架的开发框架，用于简化Spring框架的流程，更快更简单地使用SpringBoot框架。



##### 三层架构

- controller：控制层，接收前端发送的请求，对请求进行处理，并相应数据
- service：业务逻辑层，处理具体的业务逻辑
- dao：数据访问层（data access object），负责数据的访问，包括增删改查等操作



##### 分层解耦

内聚：软件中各个功能模块内部的功能联系

耦合：衡量软件中各个层/模块之间的依赖、关联的程度

软件设计原则：高内聚低耦合



**控制反转**：Inversion Of Control，简称IOC。对象创建控制权由程序自身转移至外部

**依赖注入**：Dependency Injection，简称DI。容器为应用程序提供运行时所依赖的资源

*Bean对象：IOC容器中创建、管理的对象，称之为bean*

​	控制反转的注解

| 注解        | 说明               | 位置                       |
| ----------- | ------------------ | -------------------------- |
| @Component  | 声明bean的基础注解 | 不属于下面三类时，用此注解 |
| @Controller | @Component的衍生   | 标注在控制器类上           |
| @Service    | @Component         | 标注在业务类上             |
| @Repository | @Component         | 标注在数据访问类上         |



​	依赖注入的注解

- `@Autowired`：默认按照类型自动装配
- 如果同类型的bean存在多个：
  - `@Primary`：指定
  - `@Autowired`+`@Qualifiter("bean的名称")`
  - 不使用`@Autowired`，使用`@Resource(name = "bean的名称")`



- `@Autowired`是spring框架提供的注解，而`@Resource()`是JDK提供的注解
- `@Autowired`默认按照类型注入，而`@Resource()`默认按照名称注入











#### SpringBoot



























