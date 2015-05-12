# Bean 的定义

前面的用户注册的例子中，我们已经使用 Spring 定义了一个用户持久化类：

```
<bean id="userDao" class="com.dev.spring.simple.MemoryUserDao"/>
```

这是一个最简单的 Bean 定义。它类似于调用了语句：

```
MemoryUserDao userDao = new MemoryUserDao()。
```

**id**属性必须是一个有效的 XML ID,这意味着它在整个 XML 文档中必须唯一。它是一个 Bean 的“终身代号（9527）”。同时你也可以用 name 属性为 Bean 定义一个或多个别名（用逗号或空格分开多个别名）。name 属性允许出现任意非法的 XML 字母。例如：

```
<bean id="userDao" name="userDao*_1, userDao*_2"

class="com.dev.spring.simple.MemoryUserDao"/>。
```

**class**属性定义了这个 Bean 的全限定类名（包名＋类名）。Spring 能管理几乎所有的 Java 类。一般情况，这个 Java 类会有一个默认的构造函数，用`set`方法设置依赖的属性。

Bean 元素出了上面的两个属性之外，还有很多其它属性。说明如下：

```
<bean

    id="beanId"（1）

    name="beanName"（2）

    class="beanClass"（3）

    parent="parentBean"（4）

    abstract="true | false"（5）

    singleton="true | false"（6）

    lazy-init="true | false | default"（7）

    autowire="no | byName | byType | constructor | autodetect | default"（8）

    dependency-check = "none | objects | simple | all | default"（9）

    depends-on="dependsOnBean"（10）

    init-method="method"（11）

    destroy-method="method"（12）

    factory-method="method"（13）

    factory-bean="bean">（14）

</bean>
```

（1）.id: Bean 的唯一标识名。它必须是合法的 XML ID，在整个 XML 文档中唯一。

（2）.name: 用来为 id 创建一个或多个别名。它可以是任意的字母符合。多个别名之间用逗号或空格分开。

（3）.class: 用来定义类的全限定名（包名＋类名）。只有子类 Bean 不用定义该属性。

（4）.parent: 子类 Bean 定义它所引用它的父类 Bean。这时前面的 class 属性失效。子类 Bean 会继承父类 Bean 的所有属性，子类 Bean 也可以覆盖父类 Bean 的属性。注意：子类 Bean 和父类 Bean 是同一个 Java 类。

（5）.abstract（默认为”false”）：用来定义 Bean 是否为抽象 Bean。它表示这个 Bean 将不会被实例化，一般用于父类 Bean，因为父类 Bean 主要是供子类 Bean 继承使用。

（6）.singleton（默认为“true”）：定义 Bean 是否是 Singleton（单例）。如果设为“true”,则在 BeanFactory 作用范围内，只维护此 Bean 的一个实例。如果设为“flase”，Bean将是 Prototype（原型）状态，BeanFactory 将为每次 Bean 请求创建一个新的 Bean 实例。

（7）.lazy-init（默认为“default”）：用来定义这个 Bean 是否实现懒初始化。如果为“true”，它将在 BeanFactory 启动时初始化所有的 Singleton Bean。反之，如果为“false”,它只在 Bean 请求时才开始创建 Singleton Bean。

（8）.autowire（自动装配，默认为“default”）：它定义了 Bean 的自动装载方式。

- “no”:不使用自动装配功能。
- “byName”:通过 Bean 的属性名实现自动装配。
- “byType”:通过 Bean 的类型实现自动装配。
- “constructor”:类似于 byType，但它是用于构造函数的参数的自动组装。
- “autodetect”:通过 Bean 类的反省机制（introspection）决定是使用“constructor”还是使用“byType”。

（9）.dependency-check（依赖检查，默认为“default”）：它用来确保 Bean 组件通过 JavaBean 描述的所以依赖关系都得到满足。在与自动装配功能一起使用时，它特别有用。

- none：不进行依赖检查。
- objects：只做对象间依赖的检查。
- simple：只做原始类型和 String 类型依赖的检查
- all：对所有类型的依赖进行检查。它包括了前面的 objects 和 simple。

（10）.depends-on（依赖对象）：这个 Bean 在初始化时依赖的对象，这个对象会在这个 Bean 初始化之前创建。

（11）.init-method:用来定义 Bean 的初始化方法，它会在 Bean 组装之后调用。它必须是一个无参数的方法。

（12）.destroy-method：用来定义 Bean 的销毁方法，它在 BeanFactory 关闭时调用。同样，它也必须是一个无参数的方法。它只能应用于singleton Bean。

（13）.factory-method：定义创建该 Bean 对象的工厂方法。它用于下面的“factory-bean”，表示这个 Bean 是通过工厂方法创建。此时，“class”属性失效。

（14）.factory-bean:定义创建该 Bean 对象的工厂类。如果使用了“factory-bean”则“class”属性失效。
