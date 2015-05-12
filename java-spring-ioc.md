使用IoC容器，用户注册类UserRegister不用主动创建UserDao实现类的实例。由IoC容器主动创建UserDao实现类的实例，并注入到用户注册类中。我们下面将使用Spring提供的IoC容器来管理我们的用户注册类。

用户注册类UserRegister的部分代码如下：

public class UserRegister {

    private UserDao userDao = null;//由容器注入的实例对象

    public void setUserDao(UserDao userDao){

        this.userDao = userDao;

    }

       // UserRegister的业务方法

}

在其它的UserRegister方法中就可以直接使用userDao对象了，它的实例由Spring容器主动为它创建。但是，如何组装一个UserDao的实现类到UserRegister中呢？哦，Spring提供了配置文件来组装我们的组件。Spring的配置文件applicationContext.xml代码片断如下：

<bean id="userRegister" class="com.dev.spring.simple.UserRegister">

       <property name="userDao"><ref local="userDao"/></property>

</bean>

<bean id="userDao" class="com.dev.spring.simple.MemoryUserDao"/>