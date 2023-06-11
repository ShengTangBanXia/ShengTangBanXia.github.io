---
layout: default
title: Spring
nav_order: 1
---

# 1、Spring框架是什么？

Spring是一个开源的**一站式轻量级**JavaEE框架，是为了解决企业应用程序开发复杂性而创建的。Spring框架旨在提供一种**简单、灵活、易于扩展的开发模式**，帮助开发人员快速搭建企业级应用。Spring使用基本的Java Bean来完成以前只能由EJB(Enterprise Java Beans,企业Java Bean)完成的事情。Spring的用途很广泛，从简单性、可测试性、和松耦合的角度而言，任何Java应用都能从中受益。
Spring的核心是**面向切面编程(AOP)和控制反转(IOC)容器**
# 2、Spring框架的好处有哪些？

1. 轻量级：模块化设计，可以根据自身需要选择模块，避免冗余。
2. IOC容器：将Bean的创建和依赖关系的管理交由Spring容器负责，简化了工作
3. 面向切面编程：可以在程序运行期间对方法进行动态增强，提高了代码的可维护性和可扩展性
4. 事务管理：提供了声明式事务管理和编程式事务管理，可以轻松管理事务
5. 高度集成：可以和其他框架无缝集成，提高开发效率和应用扩展性
6. 松耦合：各个模块可以独立进行开发测试和部署，进一步提供系统的可维护性和可扩展性
7. 易于测试：面向接口编程的方式，可以很方便的进行单元测试和集成测试
# 3、Spring由哪些模块组成？
![image.png](https://cdn.nlark.com/yuque/0/2023/png/22013077/1686280762674-0dd42a08-e66e-49df-bf8b-ebcb8de0962c.png#averageHue=%23c0bfbe&clientId=u815c7a35-5f9e-4&from=paste&height=542&id=u3e651361&originHeight=677&originWidth=1043&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=117268&status=done&style=none&taskId=u08afd91d-4ac3-4e90-87b5-c8c8481289a&title=&width=834.4)
主要分为以下五个部分

1. **Test模块：**Spring 支持 Junit 和 TestNG 测试框架，而且还额外提供了一些基于 Spring 的测试功能，比如在测试 Web 框架时，模拟 Http 请求的功能。
2. **核心容器模块：**
   1. **Beans：**提供了框架的基础部分，包括控制反转和依赖注入
   2. **Core：**封装了框架的底层部分，并提供了一些资源访问、类型转换的常用工具类
   3. **Conetext：**上下文模块在前两个模块的基础上，集成了Beans模块的功能并添加了资源绑定、数据验证、国际化、Java EE支持、容器生命周期、事件传播等功能
   4. **SpEL：**提供了强大的表达语言支持。支持访问和修改属性值，方法调用，支持访问和修改数组、容器和索引器，命名变量，算数和逻辑运算，从Spring容器获取Bean等功能
3. **AOP和** **Instrumentation：**
   1. **AOP模块：**提供了面向切面编程的实现，支持日志记录、权限控制、性能统计等功能，能动态的增强方法，降低业务逻辑和通用功能的耦合
   2. **Aspects：**提供AspectJ的集成，是一个功能强大且成熟的面向切面编程的AOP框架
   3. **Instrumentation：**提供了类工具的支持和类加载器的实现
   4. **Messaging：**提供了对消息传递体系结构和协议的支持
   5. **jcl模块：Spring5.x中新增了日志框架集成的模块**
4. **数据访问与集成：**
   1. **JDBC：**提供了一个JDBC的样例模板，消除了冗长的JDBC编码和必须的事务控制，并能享受到Spring管理事务的好处
   2. **ORM模块：**提供了主流的ORM框架集成，包括JPA、Hbernate、MyBatis、JDO等
   3. **OXM模块：**提供了一个Object/XML映射的抽象层实现，支持将Java对象转换为XML数据，将XML数据转化为Java对象
   4. **JMS模块：**Java消息服务，用于在两个应用程序或者分布式系统中的异步通信，Spring提供了一套生产者、消费者的模板用于更加简单的使用JMS服务
   5. **Transactions模块：**提供了声明式事务和编程式事务的支持，以便进行事务管理
5. **Web：**
   1. **Web模块：**提供了基本的Web开发集成特性，支持多文件上传、servert监听器的容器初始化、web应用上下文等功能
   2. **Servert模块：**提供了一个Spring MVC web 框架的实现，提供了基于注解的请求资源注入、数据绑定、数据验证以及一套非常易用的JSP标签
   3. **WebSocket模块：**提供了简单的可以快速搭建WebSocket Server的接口，用于实现基于Socket的双向通讯
   4. **Portlet模块：**提供了在Portlet环境使用MVC的实现
   5. **Webflux模块：Spring5.0引入的响应式web框架，用于创建基于事件循环执行模型的完全异步且非阻塞的应用程序，并且通过Reactor项目实现了Reactive Streams规范**
# 4、Spring常用的注解有哪些？
| **注解** | **作用** |
| --- | --- |
| @Autowired | 自动装配Bean对象，可以用在字段、方法和构造函数上 |
| @Component | 将类定义为Spring Bean，并由Spring托管 |
| @Controller | 将类声明为Spring MVC控制器 |
| @Service | 将类声明为业务逻辑组件 |
| @Repository | 将类声明为数据访问组件 |
| @Configuration | 将类声明为Spring配置类，用于配置和定义Bean |
| @Bean | 定义Bean，通常用于Spring配置类中 |
| @Value | 注入属性值或外部配置文件中的值 |
| @Qualifier | 当存在多个相同类型的Bean时，使用该注解指定要注入的Bean |
| @Scope | 指定Bean的作用域 |
| @PostConstruct | 在Bean的初始化方法中执行，一般用于对Bean执行自定义的初始化操作 |
| @PreDestory | 在Bean的销毁方法中执行，一般用于自定义销毁Bean时的操作 |
| @RequestMapping | 声明映射URL到控制器的方法 |
| @PathVariable | 将URL中的占位符映射到方法参数 |
| @RequestParam | 将自定义的请求参数映射到方法参数 |
| @ResponseBody | 在 HTTP Body中输出数据 |
| @ExceptionHandler | 定义异常处理方法 |

# 5、Spring IOC容器是什么？
IOC即控制反转，指的的是将对象的创建、装配、配置、生命周期以及对象之间的依赖关系交由Spring容器进行管理。Spring IOC容器则是IOC设计思想的具体实现。
# 6、IOC的优点有哪些？

1. **降低组件之间的耦合度：**IOC将组件之间的依赖关系交由容器管理，减少了组件之间的耦合度
2. **方便管理对象的生命周期：**IOC可以使对象的生命周期更加可控
3. **提高了代码的可测试性：**可以灵活切换对象，提高了代码的可测试性
4. **提高了代码的可维护性：**IOC使得组件之间的依赖关系清晰明了，易于理解和维护，降低了代码的复杂性
5. **方便实现切面编程：**可以是切面逻辑很方便的插入到应用程序的各个地方，实现代码的解耦和复用
# 7、Spring中的BeanFactory是什么？
BeanFactory是Spring框架中最基本的接口，也是Spring容器的底层接口之一，负责管理Bean的生命周期、配置元信息、依赖关系、AOP、事件等，是Spring的核心组件之一。
BeanFactory的主要作用如下：

1. **加载Bean的定义文件，并创建Bean实例**
2. **管理Bean的生命周期，包括初始化、装配、销毁等操作**
3. **实现依赖注入和AOP等高级功能**
4. **提供基础的事件和异常处理机制**
# 8、Spring中的ApplicationContext是什么？
Spring中的ApplicationContext是Spring框架中的核心容器，是管理Bean的高级容器，也是**BeanFcatory的子接口**。它可以读取配置文件、管理Bean的生命周期、装配Bean之间的关系，并且提供了许多企业级应用所需要的服务，如远程访问、EJB集成、JNDI等。
ApplicationContext提供了许多高级特性，如：**事件传播、国际化支持、Bean生命周期的控制等。**
# 9、Spring常用的ApplicationContext有哪些？
主要有以下几种：

| **ApplicationContext** | **作用** |
| --- | --- |
| ClassPathXmlApplicationContext | 从类路径下的XML文件中加载上下文 |
| FileSystemXmlApplicationContext | 从文件系统中的XML文件加载上下文 |
| AnnotationConfigApplicationContext | 根据注解创建上下文 |
| WebApplicationContext | 用于web应用程序的上下文 |
| XmlWebApplicationContext | 用于web应用程序的XML上下文 |
| StaticApplicationContext | 不依赖于外部资源的上下文实现 |
| GenericApplicationContext | 可以集成任何BeanFactory和ApplicationContext的实现 |
| GenericXmlApplicationContext | 在上一个上下文的基础下，增加了XML加载上下文定义 |

# 10、Spring中BeanFactory于与ApplicationContext的区别？

- **BeanFactory：**提供了简单的容器实现，是Spring的底层容器，负责创建、装配Bean以及管理Bean的生命周期等基本功能。
- **ApplicationContext：**BeanFactory的子接口，提供了更多的企业级功能，如：国际化支持、Bean生命周期控制、事件传播、AOP等高级功能。在加载配置文件时，ApplicationContext会预先实例化所有单例Bean，提供更快的访问和响应速度。
| **BeanFactory** | **ApplicationContext** |
| --- | --- |
| 懒加载 | 即时加载 |
| 使用语法显提供资源对象 | 自己创建和管理资源对象 |
| 不支持国际化 | 支持国际化 |
| 不支持基于依赖的注解 | 支持基于依赖的注解 |

# 11、Spring获取ApplicationContext的方法

1. **直接注入**
```java
/* 盛唐半夏 博客 */
@Resource
private ApplicationContext ctx;
```

2. **实现ApplicationContextAware接口**
```java
public class ContextUtil implements ApplicationContextAware {

    public static ApplicationContext ctx;

    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        ContextUtil.ctx = applicationContext;
    }

    public <A> A getBean (String name, Class<A> cls) {
        return ctx.getBean(name, cls);
    }

}
```

3. **继承WebApplicationObjectSupport、ApplicationObjectSupport，继承加强耦合性，不推荐**
```java
public class ContextUtil extends WebApplicationObjectSupport {

    public <A> A getBean (String name, Class<A> cls) {
        return this.getBean(name, cls);
    }

}
```

4. **使用WebApplicationContextUtils工具类**
```java
WebApplicationContext context = WebApplicationContextUtils.getWebApplicationContext(servletContext);
```

5. **从当前线程获取**
```java
 WebApplicationContext context = ContextLoader.getCurrentWebApplicationContext();
```
# 12、依赖注入是什么？
应用程序从IOC容器中获取依赖的Bean注入到应用程序的过程就叫依赖注入**(Dependency Injection，DI)；**所以说控制反转是通过依赖注入实现的，其实它们是同一个概念的不同角度描述。通俗来说就是**IOC是设计思想，DI是实现方式**
# 13、依赖注入有哪几种方式？
有三种方式，如下：

1. **构造器注入：**通过构造函数来进行依赖注入，构造函数的参数就是需要注入的依赖对象
2. **setter方法注入：**Spring容器在实例化Bean后会调用相应的setter方法为属性赋值
3. **注解注入：**在字段上添加注解或在XML文件中配置来进行依赖注入。以@Autowired（自动注入）注解注入为例，修饰符有三个属性：Constructor，byType，byName。默认按照byType注入。
   1. **constructor**：通过构造方法进行自动注入，spring会匹配与构造方法参数类型一致的bean进行注入，如果有一个多参数的构造方法，一个只有一个参数的构造方法，在容器中查找到多个匹配多参数构造方法的bean，那么spring会优先将bean注入到多参数的构造方法中
   2. **byName**：被注入bean的id名必须与set方法后半截匹配，并且id名称的第一个单词首字母必须小写，这一点与手动set注入有点不同。
   3. **byType**：查找所有的set方法，将符合符合参数类型的bean注入。
# 14、Spring中可以注入null和空字符串吗？
可以的，在使用@Autowired注解注入时，可以通过指定required参数来设置对象不一定必须存在
```java
@Autowired
private User user;
```
# 15、Spring Bean支持哪几种作用域？
支持五种作用域，如下：

| **作用域** | **描述** |
| --- | --- |
| singleton(默认) | 单例作用域，每个IOC容器中只能存在一个相同类型的实例 |
| prototype | 多例作用域，每次请求都会创建一个新的实例 |
| request | 请求作用域，每次HTTP请求都会创建一个新的实例，该实例仅在当前HTTP请求内有效 |
| session | 会话作用域，每次HTTP会话都会创建一个新的实例，该实例仅在当前HTTP会话内有效 |
| application | 应用作用域，每个Web应用程序都有一个唯一的实例，仅在当前应用程序生命周期内有效 |

# 16、Spring Bean的生命周期是怎样的？
生命周期如下：

1. Spring容器根据配置的Bean的定义**实例化Bean**
2. Spring使用**依赖注入填充所有属性**，如Bean中所定义的配置
3. **设置Bean名称，**如果Bean实现了BeanNameAware接口，则工厂通过传递Bean的ID来调用setBeanName()
4. **设置BeanFactory**，如果实现了BeanFactoryAware接口，工厂会通过传递自身实例来调用setBeanFactory
5. 如果存在与Bean关联的任何的BeanPostProcessors，则**调用postProcessBeforeInitialization()方法**
6. 如果为Bean指定了init方法，则**调用init方法**
7. 如果存在与Bean关联的任何的BeanPostProcessors，则**调用postProcessAfterInitialization()方法**
8. 如果Bean实现了DisposableBean接口，当Spring容器关闭时，会**调用destroy方法**
9. 如果为Bean指定了destroy方法()的destroy-method属性，则会调用该方法
10. 
{: .note }
💡 **生命周期主要分为四个阶段：实例化---->属性赋值---->初始化---->销毁**

# 17、Spring Bean默认是单例还是多例？
Spring Bean默认是单例的，即每次从容器中获取同一类型的Bean时，都会返回同一个实例。如果想设置为多例可以将该Bean的作用域设置为prototype即可
# 18、Spring Bean 为什么默认为单例？
主要有两个原因，如下：

1. 减少对象的创建与销毁，提高程序的性能，降低资源的消耗
2. 可以确保对象状态的一致性和可控性
# 19、Spring Bean怎么配置为多例模式？
使用@Scope注解来实现，如下：
```java
//在构造函数上添加注解
@Bean
@Scope("prototype")
public User user () {
    return new User();
}

//在类上添加注解
@Component
@Scope("prototype")
public class User {
}

```

# 20、Spring Bean是线程安全的吗？
不是线程安全的，Spring Bean是默认单例的，在多个线程同时使用一个Bean实例时，就可能产生线程安全问题。为了确保线程安全可以：

1. 使用线程安全的数据结构
2. 使用synchronized关键字
# 21、Spring Bean怎么设置为默认Bean？
可以在定义Bean的方法或者类上添加@Primary注解，来设置默认的Bean，这样在使用@Autowired注解按类型注入时，如果出现多个 相同类型的Bean注入时就不会报错
# 22、Spring怎么防止相同类型的Bean注入异常？
主要有三种方法，如下：

1. 使用@Autowired注解时，结合@Qualifier注解指定Bean的名称
2. 使用@Primary设置一个默认Bean
3. 使用@Resource注解代替@Autowired，它可以单独指定Bean的名称
# 23、Spring 如何在Bean初始化时进行操作？
有三种方法，如下：

1. 使用@PostConstruct注解
```java
public class User {
	//在Bean初始化时执行的方法
    @PostConstruct
    public void init () {
    }
}
```

2. 实现InitializingBean接口，并重写其afterPropertiesSet方法
```java
public class User implements InitializingBean {


    @Override
    public void afterPropertiesSet() throws Exception {
        //执行自定义的初始化操作
    }
}

```

3. 在Bean配置上指定initMethod方法
```java
@Bean(initMethod = "init")
public User user () {
    return new User();
}
```

{: .note }
💡 **初始化顺序为：类构造器>@PostConstruct>InitalizingBean>initMethod**

# 24、Spring 如何在Bean销毁时进行操作？
有三种方法，如下：

1. 使用@PreDestroy注解
```java
public class User {
	//在Bean销毁时执行的方法
    @PreDestroy
    public void destroy () {
    }
}
```

2. 实现DisposableBean接口，并重写其destroy方法
```java
public class User implements DisposableBean {


    @Override
    public void destroy() throws Exception {
        //执行自定义的销毁操作
    }
}

```

3. 在Bean配置上指定destroyMethod方法
```java
@Bean(destroyMethod = "destroy")
public User user () {
    return new User();
}
```

{: .note }
💡**初始化顺序为：@PreDestroy>DisposableBean>destroyMethod**

# 25、Spring中的@Component、@Service、@Respository、@Controller的区别？
@Service、@Respository、@Controller这三个注解都组合@Component注解，可用于标识MVC的不同层以实现更多功能

- **@Component注解：**可以标记任何类为Spring组件，将被Spring自动扫描并注册为Bean
- **@Service注解：**用于标记业务逻辑组件，实现业务逻辑
- **@Respository注解：**用于标记数据访问组件
- **@Controller注解：**用于标记Spring MVC控制器，处理HTTP请求和响应
# 26、Spring中的@Bean与@Component注解的区别
区别如下：

| **@Bean** | **@Component** |
| --- | --- |
| 用在方法和属性上 | 用在类上 |
| 用于手动创建一个Bean实例 | 用于自动扫描生成一个Bean实例 |

# 27、Spring中的@Bean与@Component注解用在同一个类上，容器中会有几个Bean?
一般情况下，Spring容器中只会存在一个名字唯一的Bean，在名字相同的情况下，则看是否可以覆盖，在Spring Boot中可以通过以下参数设置是否可以覆盖：
```properties
spring.main.allow-bean-definition-overriding=true
```
**该参数默认为true，即允许覆盖，容器中只会有一个Bean**
# 28、Spring中的@Autowired注解有什么用？
用于自动装配注入Bean，可以将符合条件的Bean注入到指定的对象当中
# 29、Spring中的@Autowired注解有哪几种用法？
有三种用法，如下：

1. 用在属性上
```java
@Autowired
private UserDao userDao;
```

2. 用在构造方法上
```java
@Autowired
public UserService (UserDao userDao) {
    this.userDao = userDao;
}
```

3. 用在set方法上
```java
@Autowired
public void setUserDao (UserDao userDao) {
    this.userDao = userDao;
}
```

# 30、Spring中的@Autowired注解默认按什么方式装配？
默认按照**类型装配Bean**，当有多个符合条件的Bean时会抛出NoUniqueBeanDefinitionException异常，此时需要指定需要注入的Bena名称或者指定一个默认Bean
# 31、Spring中的@Autowired注入request线程安全吗？
Spring中的@Autowired注入request是线程安全的，同时也包括注入response、session对象。
这是因为Spring并不是真正注入了一个request对对象，而是注入了一个代理对象，当真正需要使用request对象时，会通过该代理对象获取真正的request对象。
# 32、Spring中使用@Resource、@Autowired、@Inject的区别？
主要有如下区别：

1. 来源不同
| **注解** | **包** | **来源** |
| --- | --- | --- |
| @Resource | javax.annotation | Java JSR-250 |
| @Inject | javax.inject | Java JSR-330 |
| @Autowired | org.springframwork.bean.factory | Spring 2.5+ |

2. 装配方式不同
| **注解** | 按Type装配 | 按Name装配 | 默认方式 |
| --- | --- | --- | --- |
| @Resource | 支持 | 支持 | 按名称装配，找不到则按类型装配 |
| @Inject | 支持 | 需要结合@Named注解 | 按类型装配，Bean不能为空 |
| @Autowired | 支持 | 需要结合@Qualifier注解 | 按类型装配，Bean可以为空 |

# 33、Spring中的@Required注解有什么用？
Spring中的@Required注解**用于标注Bean属性的setter方法**，**表示该属性是必须的**，否则会抛出BeanInitializationException异常。使用@Required注解可以让Spring在装配过程中检查是否正确配置了属性，确保Bean被正确初始化。
```java
public class User {
    
    private String name;

    public String getName() {
        return name;
    }

    @Required
    public void setName(String name) {
        this.name = name;
    }
}
```

{: .note }
💡**@Required注解只能用于setter方法不能用于字段或者构造方法**

# 34、Spring中的@Qualifier注解有什么用？
@Qualifier是Spring中的限定符注解，用于限定在Spring容器中存在多个同类型的Bean时，指定需要注入哪个Bean。一般与@Autowired注解配合使用
# 35、Spring怎么注入Java集合类型？
通过@Autowired和@Qualifier注解实现
```java
@Component
public class User {
    
    @Autowired
    @Qualifier("userList")
    private List<String> userList;
    
}

@Configuration
public class AppConfig {
    @Bean
    @Qualifier("userList")
    public List<String> userList () {
        return Arrays.asList("Jack", "July", "June");
    }
}

```

# 36、Spring中的装配是指什么？
在Spring中，装配指的是**将各个组件(Bean)之间的依赖关系建立起来，**使得组件之间可以相互写作，实现应用程序的功能。装配的目的是将应用程序中的组件组装成一个完整的应用程序，并使它们之间可以协同工作，实现业务逻辑。
# 37、Spring中的自动装配方式有哪些？
Spring中主要有三种自动装配方式，如下：

1. **根据类型自动装配(byType)**
2. **根据名称自动装配(byName)**
3. **根据构造函数自动装配(Constructor)**
# 38、自动装配有哪些局限性？
主要有如下几点：

1. **命名冲突：**当多个Bean的名称相同或相似时，自动装配可能会导致命名冲突，需要手动指定注入的Bean
2. **类型不明确：**自动装配参数类型不明确时，可能会导致自动装配失败
3. **依赖关系不清晰：**自动装配时，很难看出依赖关系的来源，容易混淆。
4. **不能控制依赖关系**
5. **可能影响性能：**自动装配需要进行反射操作和类型匹配，当装配的Bean过多时，可能会影响程序的性能
# 39、Spring中的循环依赖是指什么？
Spring中的循环依赖是指两个及以上的Bean相互依赖形成一个循环引用的关系。如A依赖B，B依赖C，C又依赖A，这样就形成了一个循环依赖。
# 40、Spring允许循环依赖吗？
Spring默认情况下是允许循环依赖的
# 41、Spring如何解决循环依赖？
在Spring中是通过引入**三级缓存机制来解决循环依赖的**，以确保Bean能够正确的初始化和注入。
三级缓存主要包括以下三个缓存：

| **缓存** | **名称** | **描述** |
| --- | --- | --- |
| 一级缓存 | singletonObjects | 单例对象缓存，存放完成实例化、属性赋值、初始化好的Bean |
| 二级缓存 | earlySingletonObjects | 早期单例对象缓存，存放完成实例化但未属性赋值，未初始化的Bean |
| 三级缓存 | singletonFactories | 单例工厂缓存，存放完成实例化但未属性赋值，未初始化的Bean |

{: .note }
💡**Bean在调用createBeanInstance方法实例化后，会调用addSingleFactory方法将当前Bean的工厂放入三级缓存，即将Bean提前曝光给IOC容器**

举个例子，有两个对象A和B，它们互相依赖，则依赖注入的流程如下：

1. **创建对象 A，完成生命周期的第一步，即实例化（Instantiation），在调用createBeanInstance方法后，会调用addSingletonFactory方法，将已实例化但未属性赋值未初始化的对象A的工厂放入三级缓存 singletonFactories 中。即将对象A提早曝光给 IOC 容器。**
2. 继续，执行对象 A 生命周期的第二步，即属性赋值（Populate）。此时，发现对象 A 依赖对象B，所以就会尝试去获取对象 B。
3. 继续，发现 B 尚未创建，所以会执行创建对象 B 的过程。
4. 在创建对象 B 的过程中，执行实例化（Instantiation）和属性赋值（Populate）操作。此时发现，对象 B 依赖对象 A。
5. 继续，尝试在缓存中查找对象 A。先查找一级缓存，发现一级缓存中没有对象 A（因为对象 A 还未初始化完成）；转而查找二级缓存，二级缓存中也没有对象 A（因为对象 A 还未属性赋值）；转而查找三级缓存 singletonFactories，对象 B 可以通过 ObjectFactory.getObject 拿到对象 A。
6. 继续，对象 B 在获取到对象 A 后，继续执行属性赋值（Populate）和初始化（Initialization）操作。对象 B 完成初始化操作后，会被存放到一级缓存中。
7. 继续，转到对象 A 执行属性赋值过程并发现依赖了对象 B的场景。此时，对象 A 可以从一级缓存中获取到对象 B，所以可以顺利执行属性赋值操作。
8. 继续，对象 A 执行初始化（Initialization）操作，完成后，会被存放到一级缓存中。

Spring源码如下：
```java
//AbstractAutowireCapableBeanFactory

/**
	 * Actually create the specified bean. Pre-creation processing has already happened
	 * at this point, e.g. checking {@code postProcessBeforeInstantiation} callbacks.
	 * <p>Differentiates between default bean instantiation, use of a
	 * factory method, and autowiring a constructor.
	 * @param beanName the name of the bean
	 * @param mbd the merged bean definition for the bean
	 * @param args explicit arguments to use for constructor or factory method invocation
	 * @return a new instance of the bean
	 * @throws BeanCreationException if the bean could not be created
	 * @see #instantiateBean
	 * @see #instantiateUsingFactoryMethod
	 * @see #autowireConstructor
	 */
	protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args)
			throws BeanCreationException {

		// Instantiate the bean. 
        //实例化Bean
		BeanWrapper instanceWrapper = null;
		if (mbd.isSingleton()) {
			instanceWrapper = this.factoryBeanInstanceCache.remove(beanName);
		}
		if (instanceWrapper == null) {
			instanceWrapper = createBeanInstance(beanName, mbd, args);
		}
		Object bean = instanceWrapper.getWrappedInstance();
		Class<?> beanType = instanceWrapper.getWrappedClass();
		if (beanType != NullBean.class) {
			mbd.resolvedTargetType = beanType;
		}

		// Allow post-processors to modify the merged bean definition. 
        //初始化Bean之前的操作
		synchronized (mbd.postProcessingLock) {
			if (!mbd.postProcessed) {
				try {
					applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
				}
				catch (Throwable ex) {
					throw new BeanCreationException(mbd.getResourceDescription(), beanName,
							"Post-processing of merged bean definition failed", ex);
				}
				mbd.postProcessed = true;
			}
		}

		// Eagerly cache singletons to be able to resolve circular references
		// even when triggered by lifecycle interfaces like BeanFactoryAware.
        //判断是否是单例，是否允许循环依赖，并且当前Bean是否正在初始化，若是则将dangqiangBean放入三级缓存
		boolean earlySingletonExposure = (mbd.isSingleton() && this.allowCircularReferences &&
				isSingletonCurrentlyInCreation(beanName));
		if (earlySingletonExposure) {
			if (logger.isTraceEnabled()) {
				logger.trace("Eagerly caching bean '" + beanName +
						"' to allow for resolving potential circular references");
			}
            //将Bean的工厂放入三级缓存
			addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));
		}

		// Initialize the bean instance.
        //初始化Bean
        
		Object exposedObject = bean;
		try {
            //对属性进行赋值
			populateBean(beanName, mbd, instanceWrapper);
			exposedObject = initializeBean(beanName, exposedObject, mbd);
		}
		catch (Throwable ex) {
			if (ex instanceof BeanCreationException && beanName.equals(((BeanCreationException) ex).getBeanName())) {
				throw (BeanCreationException) ex;
			}
			else {
				throw new BeanCreationException(
						mbd.getResourceDescription(), beanName, "Initialization of bean failed", ex);
			}
		}

		if (earlySingletonExposure) {
			Object earlySingletonReference = getSingleton(beanName, false);
			if (earlySingletonReference != null) {
				if (exposedObject == bean) {
					exposedObject = earlySingletonReference;
				}
				else if (!this.allowRawInjectionDespiteWrapping && hasDependentBean(beanName)) {
					String[] dependentBeans = getDependentBeans(beanName);
					Set<String> actualDependentBeans = new LinkedHashSet<>(dependentBeans.length);
					for (String dependentBean : dependentBeans) {
						if (!removeSingletonIfCreatedForTypeCheckOnly(dependentBean)) {
							actualDependentBeans.add(dependentBean);
						}
					}
					if (!actualDependentBeans.isEmpty()) {
						throw new BeanCurrentlyInCreationException(beanName,
								"Bean with name '" + beanName + "' has been injected into other beans [" +
								StringUtils.collectionToCommaDelimitedString(actualDependentBeans) +
								"] in its raw version as part of a circular reference, but has eventually been " +
								"wrapped. This means that said other beans do not use the final version of the " +
								"bean. This is often the result of over-eager type matching - consider using " +
								"'getBeanNamesForType' with the 'allowEagerInit' flag turned off, for example.");
					}
				}
			}
		}

		// Register bean as disposable.
		try {
			registerDisposableBeanIfNecessary(beanName, bean, mbd);
		}
		catch (BeanDefinitionValidationException ex) {
			throw new BeanCreationException(
					mbd.getResourceDescription(), beanName, "Invalid destruction signature", ex);
		}

		return exposedObject;
	}


```

```java
// DefaultSingletonBeanRegistry

/**
	 * Return the (raw) singleton object registered under the given name.
	 * <p>Checks already instantiated singletons and also allows for an early
	 * reference to a currently created singleton (resolving a circular reference).
	 * @param beanName the name of the bean to look for
	 * @param allowEarlyReference whether early references should be created or not
	 * @return the registered singleton object, or {@code null} if none found
	 */
	@Nullable
	protected Object getSingleton(String beanName, boolean allowEarlyReference) {
		// Quick check for existing instance without full singleton lock
		Object singletonObject = this.singletonObjects.get(beanName);
		if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
			singletonObject = this.earlySingletonObjects.get(beanName);
			if (singletonObject == null && allowEarlyReference) {
				synchronized (this.singletonObjects) {
					// Consistent creation of early reference within full singleton lock
                    //从一级缓存取对象
					singletonObject = this.singletonObjects.get(beanName);
					if (singletonObject == null) {
                        //取不到则从二级缓存取对象
						singletonObject = this.earlySingletonObjects.get(beanName);
						if (singletonObject == null) {
                            //从三级缓存取对象
							ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
							if (singletonFactory != null) {
								singletonObject = singletonFactory.getObject();
                                //取到对象后放入二级缓存，并从三级缓存中删除Bean工厂
								this.earlySingletonObjects.put(beanName, singletonObject);
								this.singletonFactories.remove(beanName);
							}
						}
					}
				}
			}
		}
		return singletonObject;
	}

```

# 42、Spring怎么禁用循环依赖？
有两种方式禁用，如下：

1. **通过配置文件设置：**
```properties
spring.main.allow-circular-references=false
```

2. **手动通过上下文设置：**
```java
context.setAllowCircularReferences(false);
context.refresh();
```

# 43、Spring为何需要三级缓存解决循环依赖而不是二级缓存？
二级缓存也可以循环依赖的问题，若是选择二级缓存解决循环依赖的话，就意味着，所有的Bean都需要在实例化完成后就立马为其创建代理对象，而**Spring的设计原则是在Bean初始化完成后才为其创建代理对象。除此之外，出于对AOP的考虑，若使用二级缓存，则在AOP场景下，注入到其他Bean的对象将不是代理对象而是原始对象。**
# 44、Spring能否解决构造器注入的循环依赖？
不能解决，因为在调用构造函数时，对象还未实例化，也就无法将对象放入三级缓存中。在构造函数注入中，对象 A 需要等对象 B 的构造函数中完成初始化，对象 B 也需要等对象 A的构造函数中完成初始化。此时两个对象都不在三级缓存中，最终结果就是两个 Bean 都无法完成初始化，无法解决循环依赖问题。
# 45、Spring能否解决多例的循环依赖？
不能，Spring IOC 容器只会管理单例 Bean 的生命周期，并将单例 Bean 存放到缓存池中（三级缓存）。**Spring 并不会管理 prototype作用域的 Bean，也不会缓存该作用域的Bean**，而 Spring 中循环依赖的解决正是通过缓存来实现的。
# 46、Spring AOP是什么？
AOP全称为：Aspect Oriented Programming，即**面向切面编程**，是一种编程范式，它作为OOP面向对象编程的一种补充，用于处理系统中各个模块的横切关注点，以实现一些通用功能，如：事务管理、权限控制、缓存控制、日志打印等。
Spring AOP是Spring提供的一种轻量级的AOP框架，**可以在不更改原有代码的情况下，通过在程序运行期间，动态的将操作插入到代码中来实现横切关注点的功能**。
Spring AOP支持多种增强类型包括**前置增强、后置增强、环绕增强、异常增强以及最终增强等。**
# 47、Spring AOP 有什么作用？
AOP可以有以下作用：

1. 提供声明式事务
2. 实现资源访问控制
3. 实现缓存机制
4. 实现日志记录
5. 事项性能监控
# 48、Spring AOP有哪些实现方式？
有两种实现方式，如下：

1. **Spring AOP：**这是Spring AOP的默认实现方式，可以基于JDK动态代理或CGLIB来创建代理对象并在代理对象上增强逻辑
2. **@AspectJ：**这是一个主流的AOP框架，使用AspectJ注解可以让Spring AOP支持更灵活的切面配置，以及实现一些高级特性，如切点表达式的灵活性和切面织入的优先级等
# 49、Spring AOP 和 AspectJ AOP的区别？
| **Spring AOP** | **AspectJ** |
| --- | --- |
| 纯Java实现 | 使用Java编程语言的扩展实现 |
| 只能运行时织入 | 支持编译时、编译后和加载时织入 |
| 仅支持方法级织入 | 支持字段、方法、构造函数、final类等织入 |
| 只能由Spring容器实现 | 可以在所有域对象上实现 |
| 仅支持方法执行切入点 | 支持所有切入点 |
| 代理是由目标对象创建的 | 在程序运行前直接在代码中进行织入 |
| 性能不高 | 更好的性能 |
| 易于学习和应用 | 相对更加复杂 |

# 50、Spring AOP有哪几种通知注解？
主要有5种通知注解，如下：

| **注解** | **描述** |
| --- | --- |
| @Before | 前置通知，在方法执行前执行 |
| @Around | 环绕通知，围绕方法执行 |
| @After | 后置通知，在方法执行后执行 |
| @AfterReturning | 返回通知，在方法返回结果后执行 |
| @AfterThrowing | 异常通知，在方法抛出异常后执行 |

# 51、Spring AOP通知注解的执行顺序是怎样的？
代码正常执行的顺序如下：

1. **Spring4：**
   1. @Around通知之前
   2. @Before前置通知
   3. 方法调用
   4. @Around环绕通知之后
   5. @After后置通知
   6. @AfterReturning返回通知
2. **Spring5：**
   1. @Around通知之前
   2. @Before前置通知
   3. 方法调用
   4. @AfterReturning返回通知
   5. @After后置通知
   6. @Around环绕通知之后

代码执行异常时的顺序，如下：

1. **Spring4：**
   1. @Around通知之前
   2. @Before前置通知
   3. 方法调用
   4. @After后置通知
   5. @AfterThrowing异常通知
2. **Spring5：**
   1. @Around通知之前
   2. @Before前置通知
   3. 方法调用
   4. @AfterThrowing异常通知
   5. @After后置通知
# 52、Spring支持哪些事务管理类型？
有两种事务管理类型，如下：

1. **编程式事务管理：**通过编写代码来管理事务，需要手动控制事务的所有细节
2. **声明式事务管理：**使用AOP和事务拦截器来管理事务，无需手动控制事务，而是通过在配置文件中声明事务属性来实现。声明式事务管理可以使用XML或注解配置。
# 53、Spring用什么注解开启事务？
@Transactional注解
# 54、Spring事务的实现原理？
Spring的事务管理是基于AOP和JDBC的事务处理机制实现的，具体如下：

1. **事务管理器实现事务控制**

事务管理器负责实现事务控制，包括：**开启事务、提交事务、回滚事务等，Spring**

2. 











