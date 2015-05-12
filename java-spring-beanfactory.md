# BeanFactory

BeanFactory 是 Spring 的“心脏”。它就是 Spring IoC 容器的真面目。Spring 使用 BeanFactory 来实例化、配置和管理 Bean。但是，在大多数情况我们并不直接使用 BeanFactory，而是使用 ApplicationContext。它也是 BeanFactory 的一个实现，但是它添加了一系列“框架”的特征，比如：国际化支持、资源访问、事件传播等。ApplicationContext 我们将在后面章节中介绍。

BeanFactory 其实是一个接口－org.springframework.beans.factory.BeanFactory，它可以配置和管理几乎所有的 Java 类。当然，具体的工作是由实现 BeanFactory 接口的实现类完成。我们最常用的 BeanFactory 实现是 org.springframework.beans.factory.xml.XmlBeanFactory。它从 XML 文件中读取 Bean 的定义信息。当 BeanFactory 被创建时，Spring 验证每个 Bean 的配置。当然，要等 Bean 创建之后才能设置 Bean 的属性。单例(Singleton)Bean 在启动时就会被 BeanFactory 实例化，其它的 Bean 在请求时创建。根据 BeanFactory 的 Java 文档（Javadocs）介绍，“Bean 定义的持久化方式没有任何的限制：LDAP、RDBMS、XML、属性文件，等等”。现在 Spring 已提供了 XML 文件和属性文件的实现。无疑，XML 文件是定义 Bean 的最佳方式。

BeanFactory 是初始化 Bean 和调用它们生命周期方法的“吃苦耐劳者”。注意，BeanFactory 只能管理单例（Singleton）Bean 的生命周期。它不能管理原型(prototype,非单例)Bean 的生命周期。这是因为原型 Bean 实例被创建之后便被传给了客户端,容器失去了对它们的引用。
