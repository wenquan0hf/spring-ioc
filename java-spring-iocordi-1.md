

我们将组件的依赖关系由容器实现，那么容器如何知道一个组件依赖哪些其它的组件呢？例如用户注册的例子：容器如何得知`UserRegister`依赖于`UserDao`呢。这样，我们的组件必须提供一系列所谓的回调方法（这个方法并不是具体的 Java 类的方法），这些回调方法会告知容器它所依赖的组件。根据回调方法的不同，我们可以将 IoC 分为三种形式：

## 接口注入（Interface Injection）

它是在一个接口中定义需要注入的信息，并通过接口完成注入。Apache Avalon 是一个较为典型的接口注入型 IOC 容器，WebWork 框架的 IoC 容器也是接口注入型。

当然，使用接口注入我们首先要定义一个接口，组件的注入将通过这个接口进行。我们还是以用户注册为例，我们开发一个`InjectUserDao`接口，它的用途是将一个`UserDao`实例注入到实现该接口的类中。`InjectUserDao`接口代码如下：

```
public interface InjectUserDao {

   public void setUserDao(UserDao userDao);

}
```

`UserRegister`需要容器为它注入一个`UserDao`的实例，则它必须实现`InjectUserDao`接口。`UserRegister`部分代码如下：

```
public class UserRegister implements InjectUserDao{

    private UserDao userDao = null;//该对象实例由容器注入

    public void setUserDao(UserDao userDao) {

       this.userDao = userDao;

    }

// UserRegister 的其它业务方法

}
```

同时，我们需要配置`InjectUserDao`接口和`UserDao`的实现类。如果使用`WebWork`框架则配置文件如下：

```
<component>

         <scope>request</scope>

         <class>com.dev.spring.simple.MemoryUserDao</class>

         <enabler>com.dev.spring.simple.InjectUserDao</enabler>

</component>
```

这样，当 IoC 容器判断出`UserRegister`组件实现了`InjectUserDao`接口时，它就将`MemoryUserDao`实例注入到`UserRegister`组件中。

## 设值方法注入（Setter Injection）

在各种类型的依赖注入模式中，设值注入模式在实际开发中得到了最广泛的应用（其中很大一部分得力于 Spring 框架的影响）。

基于设置模式的依赖注入机制更加直观、也更加自然。前面的用户注册示例，就是典

型的设置注入，即通过类的 setter 方法完成依赖关系的设置。

## 构造子注入（Constructor Injection）

构造子注入，即通过构造函数完成依赖关系的设定。将用户注册示例该为构造子注入，`UserRegister`代码如下：

```
public class UserRegister {

    private UserDao userDao = null;//由容器通过构造函数注入的实例对象

    public UserRegister(UserDao userDao){

         this.userDao = userDao;

    }

    //业务方法

}
```
