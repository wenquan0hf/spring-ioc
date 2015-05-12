# 重构第四步——IoC 容器

使用 IoC 容器，用户注册类`UserRegister`不用主动创建`UserDao`实现类的实例。由 IoC 容器主动创建`UserDao`实现类的实例，并注入到用户注册类中。我们下面将使用 Spring 提供的 IoC 容器来管理我们的用户注册类。

用户注册类`UserRegister`的部分代码如下：

```
public class UserRegister {

    private UserDao userDao = null;//由容器注入的实例对象

    public void setUserDao(UserDao userDao){

        this.userDao = userDao;

    }

       // UserRegister的业务方法

}
```

在其它的`UserRegister`方法中就可以直接使用`userDao`对象了，它的实例由`Spring`容器主动为它创建。但是，如何组装一个`UserDao`的实现类到`UserRegister`中呢？哦，Spring 提供了配置文件来组装我们的组件。Spring 的配置文件 applicationContext.xml 代码片断如下：

```
<bean id="userRegister" class="com.dev.spring.simple.UserRegister">

       <property name="userDao"><ref local="userDao"/></property>

</bean>

<bean id="userDao" class="com.dev.spring.simple.MemoryUserDao"/>
```
