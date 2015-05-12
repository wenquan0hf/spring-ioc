### Bean的定义

前面的用户注册的例子中，我们已经使用Spring定义了一个用户持久化类：

<bean id="userDao" class="com.dev.spring.simple.MemoryUserDao"/>

这是一个最简单的Bean定义。它类似于调用了语句：MemoryUserDao userDao = new MemoryUserDao()。

**id**属性必须是一个有效的XML ID,这意味着它在整个XML文档中必须唯一。它是一个Bean的“终身代号（9527）”。同时你也可以用name属性为Bean定义一个或多个别名（用逗号或空格分开多个别名）。name属性允许出现任意非法的XML字母。例如：

<bean id="userDao" name="userDao*_1, userDao*_2"

class="com.dev.spring.simple.MemoryUserDao"/>。

**class**属性定义了这个Bean的全限定类名（包名＋类名）。Spring能管理几乎所有的Java类。一般情况，这个Java类会有一个默认的构造函数，用set方法设置依赖的属性。

Bean元素出了上面的两个属性之外，还有很多其它属性。说明如下：

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

（1）、id: Bean的唯一标识名。它必须是合法的XML ID，在整个XML文档中唯一。

（2）、name: 用来为id创建一个或多个别名。它可以是任意的字母符合。多个别名之间用逗号或空格分开。

（3）、class: 用来定义类的全限定名（包名＋类名）。只有子类Bean不用定义该属性。

（4）、parent: 子类Bean定义它所引用它的父类Bean。这时前面的class属性失效。子类Bean会继承父类Bean的所有属性，子类Bean也可以覆盖父类Bean的属性。注意：子类Bean和父类Bean是同一个Java类。

（5）、abstract（默认为”false”）：用来定义Bean是否为抽象Bean。它表示这个Bean将不会被实例化，一般用于父类Bean，因为父类Bean主要是供子类Bean继承使用。

（6）、singleton（默认为“true”）：定义Bean是否是Singleton（单例）。如果设为“true”,则在BeanFactory作用范围内，只维护此Bean的一个实例。如果设为“flase”，Bean将是Prototype（原型）状态，BeanFactory将为每次Bean请求创建一个新的Bean实例。

（7）、lazy-init（默认为“default”）：用来定义这个Bean是否实现懒初始化。如果为“true”，它将在BeanFactory启动时初始化所有的Singleton Bean。反之，如果为“false”,它只在Bean请求时才开始创建Singleton Bean。

（8）、autowire（自动装配，默认为“default”）：它定义了Bean的自动装载方式。

    1、“no”:不使用自动装配功能。

    2、“byName”:通过Bean的属性名实现自动装配。

    3、“byType”:通过Bean的类型实现自动装配。

    4、“constructor”:类似于byType，但它是用于构造函数的参数的自动组装。

    5、“autodetect”:通过Bean类的反省机制（introspection）决定是使用“constructor”还是使用“byType”。

（9）、dependency-check（依赖检查，默认为“default”）：它用来确保Bean组件通过JavaBean描述的所以依赖关系都得到满足。在与自动装配功能一起使用时，它特别有用。

1、 none：不进行依赖检查。

2、 objects：只做对象间依赖的检查。

3、 simple：只做原始类型和String类型依赖的检查

4、 all：对所有类型的依赖进行检查。它包括了前面的objects和simple。

（10）、depends-on（依赖对象）：这个Bean在初始化时依赖的对象，这个对象会在这个Bean初始化之前创建。

（11）、init-method:用来定义Bean的初始化方法，它会在Bean组装之后调用。它必须是一个无参数的方法。

（12）、destroy-method：用来定义Bean的销毁方法，它在BeanFactory关闭时调用。同样，它也必须是一个无参数的方法。它只能应用于singleton Bean。

（13）、factory-method：定义创建该Bean对象的工厂方法。它用于下面的“factory-bean”，表示这个Bean是通过工厂方法创建。此时，“class”属性失效。

（14）、factory-bean:定义创建该Bean对象的工厂类。如果使用了“factory-bean”则“class”属性失效。