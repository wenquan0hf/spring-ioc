# BeanFactory 管理 Bean（组件）的生命周期

下图描述了 Bean 的生命周期。它是由 IoC 容器控制。IoC 容器定义 Bean 操作的规则，即 Bean 的定义（BeanDefinition）。Bean 的定义包含了 BeanFactory 在创建 Bean 实例时需要的所有信息。BeanFactory 首先通过构造函数创建一个 Bean 实例，之后它会执行 Bean 实例的一系列之前初始化动作，初始化结束 Bean 将进入准备就绪（ready）状态，这时应用程序就可以获取这些 Bean 实例了。最后，当你销毁单例（Singleton）Bean 时，它会调用相应的销毁方法，结束 Bean 实例的生命周期。

 ![图片描述性文字](images/beanlivetime.png)

