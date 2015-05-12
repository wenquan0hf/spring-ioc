# 控制反转（IoC）/依赖注入（DI）

## 什么是控制反转/依赖注入？

控制反转（IoC=Inversion of Control）IoC，用白话来讲，就是由容器控制程序之间的（依赖）关系，而非传统实现中，由程序代码直接操控。这也就是所谓“控制反转”的概念所在：（依赖）控制权由应用代码中转到了外部容器，控制权的转移，是所谓反转。

IoC 也称为好莱坞原则（Hollywood Principle）：“Don’t call us, we’ll call you”。即，如果大腕明星想演节目，不用自己去找好莱坞公司，而是由好莱坞公司主动去找他们（当然，之前这些明星必须要在好莱坞登记过）。

正在业界为 IoC 争吵不休时，大师级人物 Martin Fowler 也站出来发话，以一篇经典文章《Inversion of Control Containers and the Dependency Injection pattern》为 IoC 正名，至此，IoC 又获得了一个新的名字：“依赖注入 （Dependency Injection）”。

相对 IoC 而言，“依赖注入”的确更加准确的描述了这种古老而又时兴的设计理念。从名字上理解，所谓依赖注入，即组件之间的依赖关系由容器在运行期决定，形象的来说，即由容器动态的将某种依赖关系注入到组件之中。

例如前面用户注册的例子。`UserRegister`依赖于`UserDao`的实现类，在最后的改进中我们使用 IoC 容器在运行期动态的为`UserRegister`注入`UserDao`的实现类。即`UserRegister`对`UserDao`的依赖关系由容器注入，`UserRegister`不用关心`UserDao`的任何具体实现类。如果要更改用户的持久化方式，只要修改配置文件 applicationContext.xml 即可。

依赖注入机制减轻了组件之间的依赖关系，同时也大大提高了组件的可移植性，这意味着，组件得到重用的机会将会更多。
