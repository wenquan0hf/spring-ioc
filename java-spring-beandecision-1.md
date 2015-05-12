# 配置 Bean 的属性值和 Bean 对象的组装

我们可以在 Spring 的配置文件中直接设置 Bean 的属性值。例如：你的 Bean 有一个“maxSize”属性，它表示每页显示数据的最大值，它有一个 set 方法。代码如下：

```
private int maxSize;

public void setMaxSize(int maxSize) {

this.maxSize = maxSize;

}
```

这样，你可以在Bean定义时设置这个属性的值：

```
<property name="maxSize"><value>20</value></property>
```

前面介绍了 Bean 原始类型的属性设置。这种方式已经可以非常有效而便利的参数化应用对象。然而，Bean 工厂的真正威力在于：它可以根据 bean 属性中描述的对象依赖来组装（wire）bean 实例。例如：userDao 对象的一个属性“sessionFactory”引用了另外一个 Bean 对象，即 `userDao`对象实例依赖于`sessionFactory`对象：

```
    <bean id="userDao" class="com.dev.spring.simple.HibernateUserDao">
    
    <property name="sessionFactory"><ref local="sessionFactory"/></property>

    </bean>

    <bean id="sessionFactory"

     class="org.springframework.orm.hibernate.LocalSessionFactoryBean">

     </bean>
```

在这个简单的例子中，使用<ref>元素引用了一个 sessionFactory 实例。在 ref 标签中，我们使用了一个“local”属性指定它所引用的Bean对象。除了 local 属性之外，还有一些其它的属性可以用来指定引用对象。下面列出<ref>元素的所有可用的指定方式：

**bean**：可以在当前文件中查找依赖对象，也可以在应用上下文（ApplicationContext）中查找其它配置文件的对象。

**local**：只在当前文件中查找依赖对象。这个属性是一个 XML IDREF，所以它指定的对象必须存在，否则它的验证检查会报错。

**external**：在其它文件中查找依赖对象，而不在当前文件中查找。

总的来说，<ref bean="..."/>和<ref local="..."/>大部分的时候可以通用。“bean”是最灵活的方式，它允许你在多个文件之间共享 Bean。而“local”则提供了便利的XML验证。
