# **Spring常见面试题总结**

***

## **Spring基础**

***

### **什么是Spring框架？**

Spring 是一款开源的**轻量级 Java 开发框架**，旨在提高开发人员的开发效率以及系统的可维护性。

我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发，比如说 Spring 支持 IoC（Inversion of Control:控制反转） 和 AOP(Aspect-Oriented Programming:面向切面编程)、可以很方便地对数据库进行访问、可以很方便地集成第三方组件（电子邮件，任务，调度，缓存等等）、对单元测试支持比较好、支持 RESTful Java 应用程序的开发。

Spring 最核心的思想就是不重新造轮子，开箱即用，提高开发效率。

### **Spring的模块有哪些**

以下是Spring5.x版本的模块结构图：

![Spring5.x主要模块](D:\Files\JavaWork\pictures\Spring5.x主要模块.png)

Spring5.x 版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。

Spring 各个模块的依赖关系如下：![Spring 各个模块的依赖关系](D:\Files\JavaWork\pictures\Spring各个模块依赖关系.png)

#### **Core Container模块**

Spring 框架的核心模块，主要提供 IoC 依赖注入功能的支持。Spring 其他所有的功能基本都需要依赖于该模块，我们从上面那张 Spring 各个模块的依赖关系图就可以看出来。

- **spring-core**：Spring 框架基本的核心工具类。
- **spring-beans**：提供对 bean 的创建、配置和管理等功能的支持。
- **spring-context**：提供对国际化、事件传播、资源加载等功能的支持。
- **spring-expression**：提供对表达式语言（Spring Expression Language） SpEL 的支持，只依赖于 core 模块，不依赖于其他模块，可以单独使用。

#### **AOP**

- **spring-aspects**：该模块为与 AspectJ 的集成提供支持。
- **spring-aop**：提供了面向切面的编程实现。
- **spring-instrument**：提供了为 JVM 添加代理（agent）的功能。 具体来讲，它为 Tomcat 提供了一个织入代理，能够为 Tomcat 传递类文件，就像这些文件是被类加载器加载的一样。没有理解也没关系，这个模块的使用场景非常有限。

#### **Data Access/Integration**

- **spring-jdbc**：提供了对数据库访问的抽象 JDBC。不同的数据库都有自己独立的 API 用于操作数据库，而 Java 程序只需要和 JDBC API 交互，这样就屏蔽了数据库的影响。
- **spring-tx**：提供对事务的支持。
- **spring-orm**：提供对 Hibernate、JPA、iBatis 等 ORM 框架的支持。
- **spring-oxm**：提供一个抽象层支撑 OXM(Object-to-XML-Mapping)，例如：JAXB、Castor、XMLBeans、JiBX 和 XStream 等。
- **spring-jms** ：消息服务。自 Spring Framework 4.1 以后，它还提供了对 spring-messaging 模块的继承。

#### **Spring Web**

- **spring-web**：对 Web 功能的实现提供一些最基础的支持。
- **spring-webmvc**：提供对 Spring MVC 的实现。
- **spring-websocket**：提供了对 WebSocket 的支持，WebSocket 可以让客户端和服务端进行双向通信。
- **spring-webflux**：提供对 WebFlux 的支持。WebFlux 是 Spring Framework 5.0 中引入的新的响应式框架。与 Spring MVC 不同，它不需要 Servlet API，是完全异步。

#### **Messaging**

**spring-messaging** 是从 Spring4.0 开始新加入的一个模块，主要职责是为 Spring 框架集成一些基础的报文传送应用。

#### **Spring Test**

Spring 团队提倡测试驱动开发（TDD）。有了控制反转 (IoC)的帮助，单元测试和集成测试变得更简单。

Spring 的测试模块对 JUnit（单元测试框架）、TestNG（类似 JUnit）、Mockito（主要用来 Mock 对象）、PowerMock（解决 Mockito 的问题比如无法模拟 final, static， private 方法）等等常用的测试框架支持的都比较好。

### **Spring，Spring MVC，Spring Boot 之间什么关系？**

Spring 是一个**轻量级 Java 开源框架**，目的是解决企业级应用开发的复杂性，简化 Java 开发。Spring 通过一个 IoC 容器，来管理 Bean 对象，使用依赖注入实现控制反转，可以很方便的整合各种框架，提供 AOP 机制弥补 OOP 的代码重复问题、更方便将不同类不同方法中的共同处理抽取成切面、自动注入给方法执行，比如日志、异常等。

Spring MVC 是 Spring 中的一个很重要的模块，主要赋予 Spring 快速构建 MVC 架构的 Web 程序的能力。MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，**其核心思想是通过将业务逻辑、数据、显示分离来组织代码**。

![img](D:\Files\JavaWork\pictures\SpringMVC.png)

使用 Spring 进行开发各种配置过于麻烦比如开启某些 Spring 特性时，需要用 XML 或 Java 进行显式配置。Spring Boot 旨在**简化 Spring 开发（减少配置文件，开箱即用！）**。Spring Boot 只是简化了配置，如果你需要构建 MVC 架构的 Web 程序，你还是需要使用 Spring MVC 作为 MVC 框架，只是说 Spring Boot 帮你简化了 Spring MVC 的很多配置，真正做到开箱即用！

### **Spring的优缺点是什么？**

#### **优点**

1. **轻量级**：Spring 框架不需要使用繁重的 EJB 组件，可以在轻量级容器中运行，因此开发和部署更为简单。
2. **面向切面编程**（AOP）：Spring 提供了很好的 AOP 支持，使得开发者可以更加容易地实现事务管理、安全、日志等功能，降低了代码的复杂度。
3. **控制反转**（IOC）：Spring 提供了依赖注入（DI）的支持，通过容器管理对象之间的依赖关系，降低了耦合度，使得代码更加可维护。
4. **支持多种开发框架**：Spring 对各种开发框架（如 Struts、Hibernate、MyBatis 等）都提供了很好的支持，使得开发者可以更加容易地集成这些框架。
5. **提高开发效率**：Spring 提供了很多实用的工具和模板，如 JDBC 模板、ORM 模板等，使得开发者可以更加快速地开发出高质量的应用。

#### **缺点**

1. **学习曲线较陡峭**：Spring 框架是一个比较复杂的框架，需要开发者学习很多概念和 API，因此学习曲线较陡峭。
2. **过度封装**：Spring 提供了很多封装，使得开发者很难理解其中的原理，也使得一些简单的操作变得复杂。
3. **运行效率**：Spring 框架由于需要进行大量的依赖注入和 AOP 操作，因此在运行时会消耗一定的系统资源，可能会影响应用的运行效率。
4. **容器过重**：Spring 的容器较重，启动速度较慢，可能会对应用的性能造成一定的影响。

### **Spring中用到了哪些设计模式？**

- **工厂模式**：Spring中通过BeanFactory、ApplicationContext创建Bean对象。
- **代理模式**：Spring AOP基于代理模式实现的。
- **单例模式**：Spring中的Bean默认都是单例的。
- **模板方法**：Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
- **包装器模式**：我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
- **观察者模式**：Spring 事件驱动模型就是观察者模式很经典的一个应用。
- **适配器模式**：Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配`Controller`。

## **Spring IoC**

***

### **谈谈自己对于 Spring IoC 的了解**

**IoC（Inversion of Control：控制反转）** 是一种设计思想，而不是一个具体的技术实现。**IoC 的思想就是将原本在程序中手动创建对象的控制权，交由 Spring 框架来管理。**不过， IoC 并非 Spring 特有，在其他语言中也有应用。

### **为什么叫控制反转？**

- **控制**：指的是对象创建（实例化、管理）的权力
- **反转**：控制权交给外部环境（Spring 框架、IoC 容器）

![IoC 图解](D:\Files\JavaWork\pictures\IoC图解.png)

将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。

在实际项目中一个 Service 类可能依赖了很多其他的类，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。

**在 Spring 中， IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个 Map（key，value），Map 中存放的是各种对象。**

Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。

#### **IoC有什么作用？**

1. 管理对象的创建和依赖关系的维护。
2. 解耦，由容器去维护具体的对象。
3. 托管了类的整个生命周期。

### **什么是 Spring Bean？**

简单来说，Bean 代指的就是那些被 IoC 容器所管理的对象。

我们需要告诉 IoC 容器帮助我们管理哪些对象，这个是通过配置元数据来定义的。配置元数据可以是 XML 文件、注解或者 Java 配置类。

```xml
<!-- Constructor-arg with 'value' attribute -->
<bean id="..." class="...">
   <constructor-arg value="..."/>
</bean>
```

下图简单地展示了 IoC 容器如何使用配置元数据来管理对象。

![img](D:\Files\JavaWork\pictures\IoC容器管理对象.png)

### **将一个类声明为 Bean 的注解有哪些?**

- `@Component`：通用的注解，可标注任意类为 `Spring` 组件。如果一个 Bean 不知道属于哪个层，可以使用`@Component` 注解标注。
- `@Repository`：对应持久层即 Dao 层，主要用于数据库相关操作。
- `@Service`：对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。
- `@Controller`：对应 Spring MVC 控制层，主要用于接受用户请求并调用 `Service` 层返回数据给前端页面。

### **@Component 和 @Bean 的区别是什么？**

- `@Component` 注解作用于**类**，而`@Bean`注解作用于**方法**。
- `@Component`通常是通过类路径扫描来自动侦测以及自动装配到 Spring 容器中（我们可以使用 `@ComponentScan` 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。`@Bean` 注解通常是我们在标有该注解的方法中定义产生这个 bean，`@Bean`告诉了 Spring 这是某个类的实例，当我需要用它的时候还给我。
- `@Bean` 注解比 `@Component` 注解的自定义性更强，而且很多地方我们只能通过 `@Bean` 注解来注册 bean。比如当我们引用第三方库中的类需要装配到 `Spring`容器时，则只能通过 `@Bean`来实现。

`@Bean`注解使用示例：

```java
@Configuration
public class AppConfig {
    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }

}
```

上面的代码相当于下面的 xml 配置

```xml
<beans>
    <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```

### **注入 Bean 的注解有哪些？**

Spring 内置的 `@Autowired` 以及 JDK 内置的 `@Resource` 和 `@Inject` 都可以用于注入 Bean。

### **使用@Autowired 注解自动装配 bean 的过程是怎样的?**

在使用`@Autowired` 注解之前需要在 Spring 配置文件进行配置标签，然后在启动Spring IoC 时，容器就会自动装载一个`AutowiredAnnotationBeanPostProcessor`后置处理器，当容器扫描到`@Autowied`、`@Resource` 或`@Inject` 时，就会在 IoC 容器自动查找需要的 bean， 并装配给该对象的属性。

在使用`@Autowired` 时，首先在容器中查询对应类型的 Bean：

 如果查询的结果为**空**，那么会抛出异常；

 如果查询结果**刚好为一个**，就将该 Bean 装配给`@Autowired` 指定的属性；

 如果查询的结果**不止一个**，需要配合`@Qualifier` 注解根据名称来查找；

 如果配合`@Qualifier` 注解根据名称来查找的结果为空，会抛出异常，可以将`@Autowire` 注解的 `required` 属性设置为 `false`。

### **@Autowired和@Resource的区别是什么？**

**`Autowired` 属于 Spring 内置的注解，默认的注入方式为`byType`（根据类型进行匹配）**，也就是说会**优先根据接口类型去匹配并注入 Bean （接口的实现类）。**

**这会有什么问题呢？** 

当一个接口存在多个实现类的话，`byType`这种方式就无法正确注入对象了，因为这个时候 Spring 会同时找到多个满足条件的选择，默认情况下它自己不知道选择哪一个。

这种情况下，**注入方式会变为 `byName`（根据名称进行匹配）**，这个名称通常就是**类名（首字母小写）**。就比如说下面代码中的 `smsService` 就是我这里所说的名称，这样应该比较好理解了吧。

```java
// smsService 就是我们上面所说的名称
@Autowired
private SmsService smsService;
```

举个例子，`SmsService` 接口有两个实现类: `SmsServiceImpl1`和 `SmsServiceImpl2`，且它们都已经被 Spring 容器所管理。

```java
// 报错，byName 和 byType 都无法匹配到 bean
@Autowired
private SmsService smsService;
// 正确注入 SmsServiceImpl1 对象对应的 bean
@Autowired
private SmsService smsServiceImpl1;
// 正确注入  SmsServiceImpl1 对象对应的 bean
// smsServiceImpl1 就是我们上面所说的名称
@Autowired
@Qualifier(value = "smsServiceImpl1")
private SmsService smsService;
```

我们还是建议通过 `@Qualifier` 注解来显式指定名称而不是依赖变量的名称。

**`@Resource`属于 JDK 提供的注解，默认注入方式为 `byName`**。如果无法通过名称匹配到对应的 Bean 的话，注入方式会变为`byType`。

`@Resource` 有两个比较重要且日常开发常用的属性：`name`（名称）、`type`（类型）。

```java
public @interface Resource {
    String name() default "";
    Class<?> type() default Object.class;
}
```

如果仅指定 `name` 属性则注入方式为`byName`，如果仅指定`type`属性则注入方式为`byType`，如果同时指定`name` 和`type`属性（不建议这么做）则注入方式为`byType`+`byName`。

```java
// 报错，byName 和 byType 都无法匹配到 bean
@Resource
private SmsService smsService;
// 正确注入 SmsServiceImpl1 对象对应的 bean
@Resource
private SmsService smsServiceImpl1;
// 正确注入 SmsServiceImpl1 对象对应的 bean（比较推荐这种方式）
@Resource(name = "smsServiceImpl1")
private SmsService smsService;
```

简单总结一下：

- **`@Autowired` 是 Spring 提供的注解，`@Resource` 是 JDK 提供的注解。**
- **`Autowired` 默认的注入方式为`byType`（根据类型进行匹配），`@Resource`默认注入方式为 `byName`（根据名称进行匹配）。**
- **当一个接口存在多个实现类的情况下，`@Autowired` 和`@Resource`都需要通过名称才能正确匹配到对应的 Bean。`Autowired` 可以通过 `@Qualifier` 注解来显式指定名称，`@Resource`可以通过 `name` 属性来显式指定名称。**

### **Bean 的作用域有哪些?**

Spring 中 Bean 的作用域通常有下面几种：

- **singleton** : IoC 容器中只有唯一的 bean 实例。Spring 中的 bean 默认都是单例的，是对单例设计模式的应用。
- **prototype** : 每次获取都会创建一个新的 bean 实例。也就是说，连续 `getBean()` 两次，得到的是不同的 Bean 实例。
- **request** （仅 Web 应用可用）: 每一次 HTTP 请求都会产生一个新的 bean（请求 bean），该 bean 仅在当前 HTTP request 内有效。
- **session** （仅 Web 应用可用） : 每一次来自新 session 的 HTTP 请求都会产生一个新的 bean（会话 bean），该 bean 仅在当前 HTTP session 内有效。
- **application/global-session** （仅 Web 应用可用）：每个 Web 应用在启动时创建一个 Bean（应用 Bean），该 bean 仅在当前应用启动时间内有效。
- **websocket** （仅 Web 应用可用）：每一次 WebSocket 会话产生一个新的 bean。

### **如何配置 bean 的作用域呢？**

xml 方式：

```xml
<bean id="..." class="..." scope="singleton"></bean>
```

注解方式：

```java
@Bean
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public Person personPrototype() {
    return new Person();
}
```

### **单例 Bean 的线程安全问题了解吗**

单例 Bean 存在线程问题，主要是因为当多个线程操作同一个对象的时候是存在资源竞争的。

常见的有两种解决办法：

1. 在 Bean 中尽量避免定义可变的成员变量。
2. 在类中定义一个 `ThreadLocal` 成员变量，将需要的可变成员变量保存在 `ThreadLocal` 中（推荐的一种方式）。

不过，大部分 Bean 实际都是无状态（没有实例变量）的（比如 Dao、Service），这种情况下， Bean 是线程安全的。

### Bean 的生命周期了解么?

- Bean 容器找到配置文件中 Spring Bean 的定义。
- Bean 容器利用 Java Reflection API 创建一个 Bean 的实例。
- 如果涉及到一些属性值 利用 `set()`方法设置一些属性值。
- 如果 Bean 实现了 `BeanNameAware` 接口，调用 `setBeanName()`方法，传入 Bean 的名字。
- 如果 Bean 实现了 `BeanClassLoaderAware` 接口，调用 `setBeanClassLoader()`方法，传入 `ClassLoader`对象的实例。
- 如果 Bean 实现了 `BeanFactoryAware` 接口，调用 `setBeanFactory()`方法，传入 `BeanFactory`对象的实例。
- 与上面的类似，如果实现了其他 `*.Aware`接口，就调用相应的方法。
- 如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessBeforeInitialization()` 方法
- 如果 Bean 实现了`InitializingBean`接口，执行`afterPropertiesSet()`方法。
- 如果 Bean 在配置文件中的定义包含 init-method 属性，执行指定的方法。
- 如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessAfterInitialization()` 方法
- 当要销毁 Bean 的时候，如果 Bean 实现了 `DisposableBean` 接口，执行 `destroy()` 方法。
- 当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法。

![Spring Bean 生命周期](D:\Files\JavaWork\pictures\bean生命周期.jpg)

### **Spring Bean中的循环依赖问题**

循环依赖（循环引用）其实就是两个或两个以上的bean互相持有对方，最终形成闭环。比如A依赖B，B依赖A。

循环依赖会导致内存溢出，因为A 时会先去执行属性 B 的初始化，而 B 的初始化又会去执行A 的初始化， 这样就形成了一个循环调用，最终导致调用栈内存溢出。

在Spring框架中根据三级缓存已经解决了大部分的循环依赖。

1. 一级缓存：单例池，缓存已经经历了完整的生命周期，已经初始化完成的bean对象；（解决不了循环依赖）
2. 二级缓存：缓存早期的bean对象（生命周期还没走完）；
3. 三级缓存：缓存的是ObjectFactory，表示对象工厂，用来创建某个对象的。

**具体流程**

![image-20230619152949493.png](D:\Files\JavaWork\pictures\循环依赖-三级缓存.png)

1. 先实例化A对象，同时会创建ObjectFactory对象存入三级缓存中；
2. A在初始化的时候需要B对象，这时候回去创建B对象；
3. B对象实例化完成，也会创建ObjectFactory对象存入三级缓存；
4. B对象需要注入A，可以通过三级缓存中的ObjectFactory对象生成A的半成品对象存入二级缓存；（此时的A对象可以是普通对象，也可以是代理对象）
5. B通过二级缓存获取到A的对象后，就可以正常注入A，然后B对象创建成功后，将对象B存入一级缓存；
6. 返回到A对象，因为此时B对象已经创建成功了，所以A对象可以直接注入B对象，完成对象A的创建，并存入一级缓存中；
7. 删除二级缓存中A的半成品对象；

#### **构造方法出现了循环依赖怎么解决？**

由于构造函数是在bean的生命周期中第一个执行的，三级缓存并不能解决构造函数的依赖注入问题。

所以**可以使用`@Lazy`懒加载注解解决**，什么时候需要对象，再进行bean对象的创建。

## **Spring AoP**

***

### **谈谈自己对于 AOP 的了解**

AOP(Aspect-Oriented Programming：面向切面编程)能够将那些**与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性。**

Spring AOP 就是**基于动态代理**的，如果要代理的对象，实现了某个接口，那么 Spring AOP 会使用 **JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候 Spring AOP 会使用 **Cglib** 生成一个被代理对象的子类来作为代理，如下图所示：

![SpringAOPProcess](D:\Files\JavaWork\pictures\SpringAop.jpeg)

### **AOP 切面编程的一些专业术语**

| 术语              |                             含义                             |
| :---------------- | :----------------------------------------------------------: |
| 目标(Target)      |                         被通知的对象                         |
| 代理(Proxy)       |             向目标对象应用通知之后创建的代理对象             |
| 连接点(JoinPoint) |         目标对象的所属类中，定义的所有方法均为连接点         |
| 切入点(Pointcut)  | 被切面拦截 / 增强的连接点（切入点一定是连接点，连接点不一定是切入点） |
| 通知(Advice)      | 增强的逻辑 / 代码，也即拦截到目标对象的连接点之后要做的事情  |
| 切面(Aspect)      |                切入点(Pointcut)+通知(Advice)                 |
| Weaving(织入)     |       将通知应用到目标对象，进而生成代理对象的过程动作       |

### **JDK动态代理和Cglib动态代理的区别？**

- JDK动态代理是**基于接口实现的代理**，使用**Java反射机制在运行时创建代理类**。JDK动态代理要求目标对象实现至少一个接口，代理类与目标类实现相同的接口，通过实现InvocationHandler接口并重写invoke()方法实现代理类的具体逻辑。
- Cglib动态代理是**基于继承实现的代理**，使用**字节码生成技术在运行时生成代理类**。Cglib动态代理不要求目标对象实现接口，可以**对任何类**进行代理。代理类继承目标类，通过重写目标类的方法实现代理类的具体逻辑。

相比于JDK动态代理，Cglib动态代理的**效率更高**，因为它不需要反射调用目标类的方法，而是通过直接调用代理类中重写的方法实现。但是Cglib动态代理也有一些限制，例如无法代理被final修饰的方法、类以及private、static等方法。

因此，**如果目标对象实现了接口，建议使用JDK动态代理；如果目标对象没有实现接口，或者需要代理被final修饰的方法，可以考虑使用Cglib动态代理**。

### **Spring AOP 和 AspectJ AOP 有什么区别？**

**Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。** Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。

Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，

如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比 Spring AOP 快很多。

### **AspectJ 定义的通知类型有哪些？**

- **Before**（前置通知）：目标对象的方法调用之前触发
- **After** （后置通知）：目标对象的方法调用之后触发
- **AfterReturning**（返回通知）：目标对象的方法调用完成，在返回结果值之后触发
- **AfterThrowing**（异常通知）：目标对象的方法运行中抛出 / 触发异常后触发。AfterReturning 和 AfterThrowing 两者互斥。如果方法调用成功无异常，则会有返回值；如果方法抛出了异常，则不会有返回值。
- **Around** （环绕通知）：编程式控制目标对象的方法调用。环绕通知是所有通知类型中可操作范围最大的一种，因为它可以直接拿到目标对象，以及要执行的方法，所以环绕通知可以任意的在目标对象的方法调用前后搞事，甚至不调用目标对象的方法

### **多个切面的执行顺序如何控制？**

1、通常使用`@Order` 注解直接定义切面顺序

```java
// 值越小优先级越高
@Order(3)
@Component
@Aspect
public class LoggingAspect implements Ordered {
```

**2、实现`Ordered` 接口重写 `getOrder` 方法。**

```java
@Component
@Aspect
public class LoggingAspect implements Ordered {
    // ....
    @Override
    public int getOrder() {
        // 返回值越小优先级越高
        return 1;
    }
}
```

## **Spring MVC**

***

### **说说自己对于 Spring MVC 了解？**

MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，其核心思想是通过将业务逻辑、数据、显示分离来组织代码。

![SpringMVC](D:\Files\JavaWork\pictures\SpringMVC.png)

Spring MVC 模式下我们一般把后端项目分为 Service 层（处理业务）、Dao 层（数据库操作）、Entity 层（实体类）、Controller 层(控制层，返回数据给前台页面)。

### **Spring MVC 的核心组件有哪些？**

- **`DispatcherServlet`**：**核心的中央处理器**，负责接收请求、分发，并给予客户端响应。
- **`HandlerMapping`**：**处理器映射器**，根据 uri 去匹配查找能处理的 `Handler` ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
- **`HandlerAdapter`**：**处理器适配器**，根据 `HandlerMapping` 找到的 `Handler` ，适配执行对应的 `Handler`；
- **`Handler`**：**请求处理器**，处理实际请求的处理器。
- **`ViewResolver`**：**视图解析器**，根据 `Handler` 返回的逻辑视图 / 视图，解析并渲染真正的视图，并传递给 `DispatcherServlet` 响应客户端

### **SpringMVC 工作原理了解吗?**

![img](D:\Files\JavaWork\pictures\SpringMVC原理.png)

**流程说明（重要）：**

1. 客户端（浏览器）发送请求， `DispatcherServlet`拦截请求。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping` 。`HandlerMapping` 根据 uri 去匹配查找能处理的 `Handler`（也就是我们平常说的 `Controller` 控制器） ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
3. `DispatcherServlet` 调用 `HandlerAdapter`适配器执行 `Handler` 。
4. `Handler` 完成对用户请求的处理后，会返回一个 `ModelAndView` 对象给`DispatcherServlet`，`ModelAndView` 顾名思义，包含了数据模型以及相应的视图的信息。`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
5. `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
6. `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
7. 把 `View` 返回给请求者（浏览器）

### **统一异常处理怎么做**

推荐使用注解的方式统一异常处理，具体会使用到 `@ControllerAdvice` + `@ExceptionHandler` 这两个注解 。

```java
@ControllerAdvice
@ResponseBody
public class GlobalExceptionHandler {

    @ExceptionHandler(BaseException.class)
    public ResponseEntity<?> handleAppException(BaseException ex, HttpServletRequest request) {
      //......
    }

    @ExceptionHandler(value = ResourceNotFoundException.class)
    public ResponseEntity<ErrorReponse> handleResourceNotFoundException(ResourceNotFoundException ex, HttpServletRequest request) {
      //......
    }
}
```

这种异常处理方式下，会给所有或者指定的 `Controller` 织入异常处理的逻辑（AOP），当 `Controller` 中的方法抛出异常的时候，由被`@ExceptionHandler` 注解修饰的方法进行处理。

`ExceptionHandlerMethodResolver` 中 `getMappedMethod` 方法决定了异常具体被哪个被 `@ExceptionHandler` 注解修饰的方法处理异常。

```java
@Nullable
	private Method getMappedMethod(Class<? extends Throwable> exceptionType) {
		List<Class<? extends Throwable>> matches = new ArrayList<>();
    //找到可以处理的所有异常信息。mappedMethods 中存放了异常和处理异常的方法的对应关系
		for (Class<? extends Throwable> mappedException : this.mappedMethods.keySet()) {
			if (mappedException.isAssignableFrom(exceptionType)) {
				matches.add(mappedException);
			}
		}
    // 不为空说明有方法处理异常
		if (!matches.isEmpty()) {
      // 按照匹配程度从小到大排序
			matches.sort(new ExceptionDepthComparator(exceptionType));
      // 返回处理异常的方法
			return this.mappedMethods.get(matches.get(0));
		}
		else {
			return null;
		}
	}
```

从源代码看出：**`getMappedMethod()`会首先找到可以匹配处理异常的所有方法信息，然后对其进行从小到大的排序，最后取最小的那一个匹配的方法(即匹配度最高的那个)。**

## **Spring 事务**

***

### **什么是事务？**

**事务是逻辑上的一组操作，要么都执行，要么都不执行。**

**事务能否生效数据库引擎是否支持事务是关键。比如常用的 MySQL 数据库默认使用支持事务的 `innodb`引擎。但是，如果把数据库引擎变为 `myisam`，那么程序也就不再支持事务了！**

### **Spring 管理事务的方式有几种？**

**编程式事务**：在代码中硬编码(不推荐使用) ： 通过 `TransactionTemplate`或者 `TransactionManager` 手动管理事务，实际应用中很少使用，但是对于你理解 Spring 事务管理原理有帮助。

**声明式事务**：在 XML 配置文件中配置或者直接基于注解（推荐使用）： 实际是通过 AOP 实现（基于`@Transactional` 的全注解方式使用最多）

#### `@Transactional` 事务注解原理

`@Transactional` 的工作机制是基于 AOP 实现的，AOP 又是使用动态代理实现的。如果目标对象实现了接口，默认情况下会采用 JDK 的动态代理，如果目标对象没有实现了接口,会使用 CGLIB 动态代理。

### **Spring 事务管理接口介绍**

Spring 框架中，事务管理相关最重要的 3 个接口如下：

- **`PlatformTransactionManager`**：（平台）事务管理器，Spring 事务策略的核心。
- **`TransactionDefinition`**：事务定义信息(事务隔离级别、传播行为、超时、只读、回滚规则)。
- **`TransactionStatus`**：事务运行状态。

我们可以把 **`PlatformTransactionManager`** 接口可以被看作是事务上层的管理者，而 **`TransactionDefinition`** 和 **`TransactionStatus`** 这两个接口可以看作是事务的描述。

**`PlatformTransactionManager`** 会根据 **`TransactionDefinition`** 的定义比如事务超时时间、隔离级别、传播行为等来进行事务管理 ，而 **`TransactionStatus`** 接口则提供了一些方法来获取事务相应的状态比如是否新事务、是否可以回滚等等。

#### **PlatformTransactionManager：事务管理接口**

**Spring 并不直接管理事务，而是提供了多种事务管理器** 。Spring 事务管理器的接口是：**`PlatformTransactionManager`** 。

通过这个接口，Spring 为各个平台如：JDBC(`DataSourceTransactionManager`)、Hibernate(`HibernateTransactionManager`)、JPA(`JpaTransactionManager`)等都提供了对应的事务管理器，但是具体的实现就是各个平台自己的事情了。

**为什么要定义或者说抽象出来`PlatformTransactionManager`这个接口呢？**

主要是因为要将事务管理行为抽象出来，然后不同的平台去实现它，这样我们可以保证提供给外部的行为不变，方便我们扩展。

#### **TransactionDefinition:事务属性**

事务管理器接口 **`PlatformTransactionManager`** 通过 **`getTransaction(TransactionDefinition definition)`** 方法来得到一个事务，这个方法里面的参数是 **`TransactionDefinition`** 类 ，这个类就定义了一些基本的事务属性。

**什么是事务属性呢？** 事务属性可以理解成事务的一些基本配置，描述了事务策略如何应用到方法上。

事务属性包含了 5 个方面：

- 隔离级别
- 传播行为
- 回滚规则
- 是否只读
- 事务超时

#### **TransactionStatus：事务状态**

`TransactionStatus`接口用来记录事务的状态 该接口定义了一组方法，用来获取或判断事务的相应状态信息。

`PlatformTransactionManager.getTransaction(…)`方法返回一个 `TransactionStatus` 对象。

### **事务属性详解**

#### 事务传播行为

**事务传播行为是为了解决业务层方法之间互相调用的事务问题**。

当事务方法被另一个事务方法调用时，必须指定事务应该如何传播。例如：方法可能继续在现有事务中运行，也可能开启一个新事务，并在自己的事务中运行。

举个例子：我们在 A 类的`aMethod()`方法中调用了 B 类的 `bMethod()` 方法。这个时候就涉及到业务层方法之间互相调用的事务问题。如果我们的 `bMethod()`如果发生异常需要回滚，如何配置事务传播行为才能让 `aMethod()`也跟着回滚呢？这个时候就需要事务传播行为的知识了，如果你不知道的话一定要好好看一下。

```java
@Service
Class A {
    @Autowired
    B b;
    @Transactional(propagation = Propagation.xxx)
    public void aMethod {
        //do something
        b.bMethod();
    }
}

@Service
Class B {
    @Transactional(propagation = Propagation.xxx)
    public void bMethod {
       //do something
    }
}
```

**正确的事务传播行为可能的值如下**：

**1.`TransactionDefinition.PROPAGATION_REQUIRED`**

使用的最多的一个事务传播行为，我们平时经常使用的`@Transactional`注解默认使用就是这个事务传播行为。如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。也就是说：

- 如果外部方法没有开启事务的话，`Propagation.REQUIRED`修饰的内部方法会新开启自己的事务，且开启的事务相互独立，互不干扰。
- 如果外部方法开启事务并且被`Propagation.REQUIRED`的话，所有`Propagation.REQUIRED`修饰的内部方法和外部方法均属于同一事务 ，只要一个方法回滚，整个事务均回滚。

```java
@Service
Class A {
    @Autowired
    B b;
    @Transactional(propagation = Propagation.REQUIRED)
    public void aMethod {
        //do something
        b.bMethod();
    }
}
@Service
Class B {
    @Transactional(propagation = Propagation.REQUIRED)
    public void bMethod {
       //do something
    }
}
```

**`2.TransactionDefinition.PROPAGATION_REQUIRES_NEW`**

创建一个新的事务，如果当前存在事务，则把当前事务挂起。也就是说不管外部方法是否开启事务，`Propagation.REQUIRES_NEW`修饰的内部方法会新开启自己的事务，且开启的事务相互独立，互不干扰。

举个例子：如果我们上面的`bMethod()`使用`PROPAGATION_REQUIRES_NEW`事务传播行为修饰，`aMethod`还是用`PROPAGATION_REQUIRED`修饰的话。如果`aMethod()`发生异常回滚，`bMethod()`不会跟着回滚，因为 `bMethod()`开启了独立的事务。但是，如果 `bMethod()`抛出了未被捕获的异常并且这个异常满足事务回滚规则的话，`aMethod()`同样也会回滚，因为这个异常被 `aMethod()`的事务管理机制检测到了。

```java
@Service
Class A {
    @Autowired
    B b;
    @Transactional(propagation = Propagation.REQUIRED)
    public void aMethod {
        //do something
        b.bMethod();
    }
}
@Service
Class B {
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void bMethod {
       //do something
    }
}
```

**3.`TransactionDefinition.PROPAGATION_NESTED`**：

如果当前存在事务，就在嵌套事务内执行；如果当前没有事务，就执行与`TransactionDefinition.PROPAGATION_REQUIRED`类似的操作。也就是说：

- 在外部方法开启事务的情况下，在内部开启一个新的事务，作为嵌套事务存在。
- 如果外部方法无事务，则单独开启一个事务，与 `PROPAGATION_REQUIRED` 类似。

这里还是简单举个例子：如果 `bMethod()` 回滚的话，`aMethod()`不会回滚。如果 `aMethod()` 回滚的话，`bMethod()`会回滚。

```java
@Service
Class A {
    @Autowired
    B b;
    @Transactional(propagation = Propagation.REQUIRED)
    public void aMethod {
        //do something
        b.bMethod();
    }
}

@Service
Class B {
    @Transactional(propagation = Propagation.NESTED)
    public void bMethod {
       //do something
    }
}
```

**4.`TransactionDefinition.PROPAGATION_MANDATORY`**

如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。（mandatory：强制性）

这个使用的很少，就不举例子来说了。

**若是错误的配置以下 3 种事务传播行为，事务将不会发生回滚，这里不对照案例讲解了，使用的很少。**

- **`TransactionDefinition.PROPAGATION_SUPPORTS`**: 如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。
- **`TransactionDefinition.PROPAGATION_NOT_SUPPORTED`**: 以非事务方式运行，如果当前存在事务，则把当前事务挂起。
- **`TransactionDefinition.PROPAGATION_NEVER`**: 以非事务方式运行，如果当前存在事务，则抛出异常。

#### 事务隔离级别

- **`TransactionDefinition.ISOLATION_DEFAULT`** :使用后端数据库默认的隔离级别，MySQL 默认采用的 `REPEATABLE_READ` 隔离级别，Oracle 默认采用的 `READ_COMMITTED` 隔离级别。
- **`TransactionDefinition.ISOLATION_READ_UNCOMMITTED`** :最低的隔离级别，使用这个隔离级别很少，因为它允许读取尚未提交的数据变更，**可能会导致脏读、幻读或不可重复读**
- *`TransactionDefinition.ISOLATION_READ_COMMITTED`** : 允许读取并发事务已经提交的数据，**可以阻止脏读，但是幻读或不可重复读仍有可能发生**
- *`TransactionDefinition.ISOLATION_REPEATABLE_READ`** : 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，**可以阻止脏读和不可重复读，但幻读仍有可能发生。**
- *`TransactionDefinition.ISOLATION_SERIALIZABLE`** : 最高的隔离级别，完全服从 ACID 的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，**该级别可以防止脏读、不可重复读以及幻读**。但是这将严重影响程序的性能。通常情况下也不会用到该级别。

#### 事务超时属性

所谓事务超时，就是指一个事务所允许执行的最长时间，如果超过该时间限制但事务还没有完成，则自动回滚事务。在 `TransactionDefinition` 中以 int 的值来表示超时时间，其单位是秒，默认值为-1，这表示事务的超时时间取决于底层事务系统或者没有超时时间。

#### 事务只读属性

对于只有读取数据查询的事务，可以指定事务类型为 readonly，即只读事务。只读事务不涉及数据的修改，数据库会提供一些优化手段，适合用在有多条数据库查询操作的方法中。

#### 事务回滚规则

这些规则定义了哪些异常会导致事务回滚而哪些不会。默认情况下，事务只有遇到运行期异常（`RuntimeException` 的子类）时才会回滚，`Error` 也会导致事务回滚，但是，在遇到检查型（Checked）异常时不会回滚。

### **@Transactional(rollbackFor = Exception.class)注解了解吗？**

`Exception` 分为运行时异常 `RuntimeException` 和非运行时异常。事务管理对于企业应用来说是至关重要的，即使出现异常情况，它也可以保证数据的一致性。

当 `@Transactional` 注解作用于类上时，该类的所有 public 方法将都具有该类型的事务属性，同时，我们也可以在方法级别使用该标注来覆盖类级别的定义。如果类或者方法加了这个注解，那么这个类里面的方法抛出异常，就会回滚，数据库里面的数据也会回滚。

在 `@Transactional` 注解中如果不配置`rollbackFor`属性，那么事务只会在遇到`RuntimeException`的时候才会回滚，加上 `rollbackFor=Exception.class`,可以让事务在遇到非运行时异常时也回滚。

## **Spring Boot**

***

### **什么是Spring Boot**

Spring Boot 是 Spring 源组织下的子项目，是 Spring 组件一站式解决方案，主要是简化了使用 Spring 的难度，**简化了繁重的配置**，**提供了各种启动器，开发者能快速上手**。

### **Spring Boot的优点**

1. 容易上手，提升开发效率，为 Spring 开发提供一个更快、更广泛的入门体验。
2. 开箱即用，远离繁琐的配置。
3. 没有代码生成，也不需要 XML 配置。
4. 提供了一系列大型项目通用的非业务性功能，例如：内嵌服务器、安全管理、运行数据监控、运行状况检查和外部化配置等。
5. 避免大量的 Maven 导入和各种版本冲突。

### **谈谈Spring Boot自动装配原理 ？**

在 SpringBoot 应用的每个启动类上都会有个注解`@SpringBootApplication`

```java
@SpringBootApplication
public class SpringSecurityJwtGuideApplication {
      public static void main(java.lang.String[] args) {
        SpringApplication.run(SpringSecurityJwtGuideApplication.class, args);
    }
}
```

我们可以把 `@SpringBootApplication`看作是 `@SpringBootConfiguration`、`@EnableAutoConfiguration`、`@ComponentScan` 注解的集合。

根据 SpringBoot 官网，这三个注解的作用分别是：

- `@EnableAutoConfiguration`：开启 SpringBoot 的自动配置机制
- `@ComponentScan`： 扫描被`@Component` (`@Repository`,`@Service`,`@Controller`)注解的 bean，注解默认会扫描该类所在的包下所有的类。
- `@SpringBootConfiguration`：允许在 Spring 上下文中注册额外的 bean 或导入其他配置类

其中`@EnableAutoConfiguration`注解是实现自动配置的核心注解。该注解**通过`@Import`注解导入对应的配置选择器**，关键的是内部读取了该项目和该项目引用的jar包的classpath路径下**META-INF/spring.factories**文件中**所配置的类的全类名**。

这些配置类中所定义的Bean会**根据条件注解所指定的条件**来决定是否要将其导入到Spring容器中。

比如`@ConditionalOnClass`注解，判断是否有对应的class文件，如果有则加载该类，把这个配置类的所有Bean放入到Spring中使用。

------

具体来说SpringBoot的自动装配是通过注解实现的，当满足某些条件时，自动装配相应的组件。

1. 判断自动装配开关是否打开。默认`spring.boot.enableautoconfiguration=true`，可在 `application.properties` 或 `application.yml` 中设置；

2. 用于获取`EnableAutoConfiguration`注解中的 `exclude` 和 `excludeName`；

3. 获取需要自动装配的所有配置类，读取`META-INF/spring.factories`；

4. 到这里可能面试官会问你:“`spring.factories`中这么多配置，每次启动都要全部加载么？”。

   **很明显，这是不会的**。因为，这一步有经历了一遍筛选，`@ConditionalOnXXX` 中的所有条件都满足，该类才会生效。

值得注意的是，Spring Boot的自动装配仅限于Spring框架本身提供的组件和第三方库中的Spring组件，对于其他的组件，需要手动进行配置。

### **Spring Boot Starter是什么？如何自定义？**

Spring Boot Starter 是 Spring boot 的核心，可以理解为一个可拔插式的插件。

例如，想使用Reids插件，那么可以导入spring-boot-starter-redis 依赖 Starter 的命名。官方对 Starter 项目的 jar 包定义的 artifactId 是有要求的 ， 当然也可以不遵守 。

Spring 官 方 Starter 通 常 命 名 为 `spring-boot-starter-{name}`如：`spring-boot-starter-web`，Spring 官方建议非官方的 starter 命名应遵守`{name}-spring-boot-starter` 的格式。

------

自定义starter的步骤如下：

1. 新建一个maven项目，在pom.xml文件中定义好所需要的依赖；
2. 新建配置类，写好配置项和默认值，使用`@ConfigurationProperties`指明配置前缀；
3. 新建自动装配类，使用`@Configuration`和`@Bean`进行自动装配；
4. 新建Spring.factories文件，用于指定自动装配类的路径；
5. 将starter安装到maven仓库，让其他项目能够引用。

### **Spring Boot核心配置文件**

Spring boot 核心的两个配置文件 ：

1. ` bootstrap` (. yml 或 者 . properties)：bootstrap 由父 ApplicationContext 加载的，比 applicaton 优先加载，配置在应用程序上下文的引导阶段生效。一般来说我们在 Spring Cloud Config 或者 Nacos 中会用到它。且 bootstrap 里面的属性不能被覆盖；

2. `application `(. yml 或者 . properties)：由 ApplicatonContext 加 载，用于 Spring boot 项目的自动化配置。

   `application.properties `是基于属性文件的配置格式，支持 key-value 形式的键值对。在 Spring Boot 中，可以在 application.properties 文件中配置各种应用程序属性，如端口号、数据库连接、日志级别等等。

   `application.yml` 是基于 YAML 格式的配置文件，支持层级结构的配置形式，可以更加清晰地表达配置项之间的关系。与 `application.properties` 相比，`application.yml` 更易读、易维护，也更加灵活。

### **Spring Boot打成jar和普通jar有什么区别？**

Spring Boot 打成的 jar **无法被其他项目依赖**，主要还是他和普通 jar 的结构不同。

普通的 jar 包，解压后直接就是包名，包里就是我们的代码，而 Spring Boot 打包成的可执行 jar 解压后，在\BOOT-INF\classes 目录下才是我们的代码，因此无法被直接引用。如果非要引用，可以在 pom.xml 文件中增加配置， 将 Spring Boot 项目打包成两个 jar ，一个可执行，一个可引用

### **Spring Boot和Spring Cloud的区别？**

SpringBoot 专注于快速、方便的开发**单个微服务个体**，SpringCloud 关注**全局的服务治理框架**。

SpringCloud 将 SpringBoot 开发的一个个单体微服务整合并管理起来，为各个微服务之间提供配置管理、服务发现、断路器、路由、 微代理、事件总线、全局锁、决策竞选、分布式会话等等集成服务。

SpringBoot 可以离开SpringCloud 独立开发项目 ， 但是 SpringCloud 离不开 SpringBoot ，**属于依赖的关系**。