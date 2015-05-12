<p>我们将组件的依赖关系由容器实现，那么容器如何知道一个组件依赖哪些其它的组件呢？例如用户注册的例子：容器如何得知UserRegister依赖于UserDao呢。这样，我们的组件必须提供一系列所谓的回调方法（这个方法并不是具体的Java类的方法），这些回调方法会告知容器它所依赖的组件。根据回调方法的不同，我们可以将IoC分为三种形式：</p>
<h4>Type1－接口注入（Interface Injection）</h4>
<p>它是在一个接口中定义需要注入的信息，并通过接口完成注入。Apache Avalon是一个较为典型的Type1型IOC容器，WebWork框架的IoC容器也是Type1型。</p>
<p>当然，使用接口注入我们首先要定义一个接口，组件的注入将通过这个接口进行。我们还是以用户注册为例，我们开发一个InjectUserDao接口，它的用途是将一个UserDao实例注入到实现该接口的类中。InjectUserDao接口代码如下：</p>
<p>public interface InjectUserDao {</p>
<p>&nbsp;&nbsp;&nbsp; public void setUserDao(UserDao userDao);</p>
<p>}</p>
<p>UserRegister需要容器为它注入一个UserDao的实例，则它必须实现InjectUserDao接口。UserRegister部分代码如下：</p>
<p>public class UserRegister implements InjectUserDao{</p>
<p>&nbsp;&nbsp;&nbsp; private UserDao userDao = null;//该对象实例由容器注入</p>
<p>&nbsp;&nbsp;&nbsp; public void setUserDao(UserDao userDao) {</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; this.userDao = userDao;</p>
<p>&nbsp;&nbsp;&nbsp; }</p>
<p>// UserRegister的其它业务方法</p>
<p>}</p>
<p>&nbsp;</p>
<p>同时，我们需要配置InjectUserDao接口和UserDao的实现类。如果使用WebWork框架则配置文件如下：</p>
<p>&lt;component&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;scope&gt;request&lt;/scope&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;class&gt;com.dev.spring.simple.MemoryUserDao&lt;/class&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;enabler&gt;com.dev.spring.simple.InjectUserDao&lt;/enabler&gt;</p>
<p>&lt;/component&gt;</p>
<p>这样，当IoC容器判断出UserRegister组件实现了InjectUserDao接口时，它就将MemoryUserDao实例注入到UserRegister组件中。</p>
<p>&nbsp;</p>
<h4>Type2－设值方法注入（Setter Injection）</h4>
<p>在各种类型的依赖注入模式中，设值注入模式在实际开发中得到了最广泛的应用（其中很大一部分得力于Spring框架的影响）。</p>
<p>基于设置模式的依赖注入机制更加直观、也更加自然。前面的用户注册示例，就是典</p>
<p>型的设置注入，即通过类的setter方法完成依赖关系的设置。</p>
<p>&nbsp;</p>
<h4>Type3－构造子注入（Constructor Injection）</h4>
<p>构造子注入，即通过构造函数完成依赖关系的设定。将用户注册示例该为构造子注入，UserRegister代码如下：</p>
<p>public class UserRegister {</p>
<p>&nbsp;&nbsp;&nbsp; private UserDao userDao = null;//由容器通过构造函数注入的实例对象</p>
<p>&nbsp;&nbsp;&nbsp; public UserRegister(UserDao userDao){</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; this.userDao = userDao;</p>
<p>&nbsp;&nbsp;&nbsp; }</p>
<p>&nbsp;&nbsp;&nbsp; //业务方法</p>
<p>}</p>
<p>&nbsp;</p>
