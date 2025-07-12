# 什么是IoC和DI

## IoC

I0C（Inversion of Control）控制反转

- 使用对象时，由主动new产生对象转换为由**外部**提供对象，此过程中对象创建控制权由程序转移到外部，此思想称为控制反转。
  - 业务层要用数据层的类对象，以前是自己`new`的
  - 现在自己不new了，交给`IoC容器`来创建对象
  - `IoC容器`就反转控制了数据层对象的创建权
  - 这种思想就是控制反转


## DI

DI（Dependency Injection）依赖注入

依赖注入（DI）是IoC的一种特殊形式，在容器中建立bean与bean之间的依赖关系的整个过程，称为依赖注入

- 业务层要用数据层的类对象，以前是自己`new`的
- 现在自己不new了，靠`IOC容器`来给注入进来
- 这种思想就是依赖注入
- IOC容器中哪些bean之间要建立依赖关系
  - 这个需要程序员根据业务需求提前建立好关系，如业务层需要依赖数据层，service就要和dao建立依赖关系


# 什么是Ioc容器

## IoC容器

**IoC 容器（Inversion of Control Container）** 是 Spring 框架的核心机制，负责**实例化、配置、组装**应用程序中的对象（即 **Bean**），并管理其**生命周期**。

它通过读取**配置元数据**（XML、Java 注解或代码）来获取 Bean 的定义及依赖关系，并基于**依赖注入（DI）** 原则自动完成对象之间的协作，从而实现**控制反转（IoC）**——即由容器（而非对象自身）掌控依赖的创建与绑定。

对象仅通过构造函数参数、工厂方法参数，或在对象实例构造后/从工厂方法返回后设置的属性来定义其依赖项（即与之协作的其他对象），随后IoC容器在创建bean时自动注入这些依赖项。这一过程从根本上逆转了bean通过直接构造类或使用服务定位器模式等机制来控制其依赖项实例化或定位的方式，因此称为控制反转。

## Bean

在 Spring 框架中，构成应用程序核心并由 Spring IoC 容器管理的对象称为 **Bean**。

Bean 是由 Spring IoC 容器实例化、组装和管理的对象。除此之外，Bean 与应用程序中的其他普通对象并无本质区别。

## IoC容器的API

`org.springframework.beans`和`org.springframework.context` 包是Ioc容器的基础。

`BeanFactory`是`org.springframework.beans.factory`包里的接口

`ApplicationContext`是`org.springframework.context` 包里的接口

`BeanFactory`接口 提供了管理各种类型对象的机制，`ApplicationContext`是`BeanFactory`的子接口，它还提供以下增强功能：

- 更便捷的Spring AOP功能集成

-  消息资源处理（用于国际化支持）

-  事件发布机制

-  特定应用层的上下文实现（如Web应用中使用的WebApplicationContext）

即BeanFactory提供了配置框架和基础功能，而ApplicationContext则在此基础上增加了更多企业级特性

# 为什么要引入IoC

![null](https://my--pic.oss-cn-beijing.aliyuncs.com/img/1751984180298-22718dcb-5bc2-46df-b9be-9d635e28383d.png)

(1)业务层需要调用数据层的方法，就需要在业务层new数据层的对象

(2)如果数据层的实现类发生变化，那么业务层的代码也需要跟着改变，发生变更后，都需要进行编译打包和重部署

(3)所以，现在代码在编写的过程中存在的问题是：耦合度偏高

![null](https://my--pic.oss-cn-beijing.aliyuncs.com/img/1751984180364-d6f16f58-7672-4dc8-98b8-32d0f5075fba.png)

如果能把框中的内容给去掉，就可以降低依赖了，但是又会引入新的问题，去掉以后程序不能运行，因为bookDao没有赋值为Null，强行运行就会出空指针异常。

所以现在的问题就是，业务层不想new对象，运行的时候又需要这个对象。

针对这个问题，Spring就提出了IoC:

- 使用对象时，在程序中不要主动使用new产生对象，转换为由外部提供对象

IoC和DI的最终目标就是:充分解耦，具体实现靠:

- 使用IoC容器管理bean（IoC)

- 在IOC容器内将有依赖关系的bean进行关系绑定（DI）

-  最终结果为:使用对象时不仅可以直接从IOC容器中获取，并且获取到的bean已经绑定了所有的依赖关系
