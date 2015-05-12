Bean工厂使用Bean的构造函数创建Bean对象之后，紧接着它会做一件非常重要的工作——Bean的初始化。它会根据配置信息设置Bean的属性和依赖对象，执行相应的初始化方法。

#### 自动装配

一般不推荐在大型的应用系统中使用自动装配。当然，它可以很好的用于小型应用系统。如果一个bean声明被标志为“autowire（自动装配）”，bean工厂会自动将其他的受管对象与其要求的依赖关系进行匹配，从而完成对象的装配——当然，只有当对象关系无歧义时才能完成自动装配。因为不需要明确指定某个协作对象，所以可以带来很多的便利性。

举个例子，如果在Bean工厂中有一个SessionFactory类型的实例，HibernateUserDao的sessionFactory属性就可以获得这个实例。这里可以使用<bean>的autowire属性，就象这样：

<bean id="userDao" class="com.dev.spring.simple.HibernateUserDao" autowire=”byType”>

</bean>

<bean id="sessionFactory"

class="org.springframework.orm.hibernate.LocalSessionFactoryBean">

       …..

       </bean>

注意，在userDao的定义中并没有明确引用sessionFactory。由于它的“autowire”被设置为“byType”，所有只要userDao有一个类型为SessionFactory的属性并有一个set方法，Bean工厂就会自动将sessionFactory组装到userDao中。

如果一个应用有两个数据库，这时就对应有两个SessionFactory。这时autowire="byType"就无法使用了。我们可以使用另外一种自动装配方式“byName”。它将根据属性的名称来匹配依赖对象，这样如果你的配置文件中可以同时存在多个类型相同的SessionFactory，只要他们定义的名称不同就可以了。这种方式的缺点是：需要精确匹配Bean的名称，即必须要保证属性的名称和它所依赖的Bean的名称相等，这样比较容易出错。

（举例：Aa对象依赖Bb对象。）

<table cellspacing="0" cellpadding="0" width="100%">

<tbody>

<tr>

<td>

<div class="shape">

**注意：我们还是强烈推荐手工指定Bean****之间的依赖关系。这种用法最强大，因为它允许按名称引用特定的Bean****实例，即使多个Bean****具有相同类型也不会混淆。同时，你可以清楚的知道一个Bean****到底依赖哪些其它的Bean****。如果使用自动装载，你只能去Bean****的代码中了解。甚至，Bean****工厂也许会自动装载一些你根本不想依赖的对象。**

</div>

</td>

</tr>

</tbody>

</table>

#### 依赖检查

如果你希望Bean严格的设置所有的属性，“dependency-check”（依赖检查）属性将会非常有用。它默认为“none”，不进行依赖检查。“simple”会核对所有的原始类型和String类型的属性。“objects”只做对象间的关联检查（包括集合）。“all”会检查所有的属性，包括“simple”和“objects”。

举个例子：一个Bean有如下的一个属性：

private int intVar = 0;

public void setIntVar(int intVar) {

        this.intVar = intVar;

}

这个Bean的配置文件设置了“dependency-check=”simple””。如果这个Bean的配置中没有定义这个属性“intVar”，则在进行这个Bean的依赖检查时就会抛出异常：org.springframework.beans.factory.UnsatisfiedDependencyException。

#### setXXX()

set方法非常简单，它会给class注入所有依赖的属性。这些属性都必须是在配置文件中使用<property>元素定义，它们可以是原始类型，对象类型（Integer,Long），null值，集合，其它对象的引用。

#### afterPropertiesSet()

有两种方法可以实现Bean的之前初始化方法。1、使用“init-method”属性，在Spring的配置文件中定义回调方法。下面将会具体描述。2、实现接口InitializingBean并实现它的afterPropertiesSet()方法。接口InitializingBean的代码如下：

public interface InitializingBean {

void afterPropertiesSet() throws Exception;

}

在JavaBean的所有属性设置完成以后，容器会调用afterPropertiesSet()方法，应用对象可以在这里执行任何定制的初始化操作。这个方法允许抛出最基本的Exception异常，这样可以简化编程模型。

在Spring框架内部，很多bean组件都实现了这些回调接口。但我们的Bean组件最好不要通过这种方式实现生命周期的回调，因为它依赖于Spring的API。无疑，第一种方法是我们的最佳选择。

#### init-method

init-method的功能和InitializingBean接口一样。它定义了一个Bean的初始化方法，在Bean的所有属性设置完成之后自动调用。这个初始化方法不用依赖于Spring的任何API。它必须是一个无参数的方法，可以抛出Exception。

例如：我们的Bean组件UserManger中定义一个初始化方法init()。这样，我们就可以在Bean定义时指定这个初始化方法：

<bean id=”userManger” class=”com.dev.spring.um.DefaultUserManager”

init-method=”init”>

……

</bean>

#### setBeanFactory()

### Bean的准备就绪（Ready）状态

Bean完成所有的之前初始化之后，就进入了准备就绪(Ready)状态。这就意味着你的应用程序可以取得这些Bean，并根据需要使用他们。