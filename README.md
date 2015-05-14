# Spring-IoC 容器

控制反转（Inversion of Control，英文缩写为 IoC ）是一个重要的面向对象编程的法则来削减计算机程序的耦合问题，也是轻量级的 Spring 框架的核心（所谓 IoC 就是一个用 XML 来定义生成对象的模式）。Spring 的模块化是很强的，各个功能模块都是独立的，因为大多数应用程序都是由两个或是更多的类通过彼此的合作来实现业务逻辑，这使得每个对象都需要获取与其合作的对象（也就是它所依赖的对象）的引用。如果这个获取过程要靠自身实现，那么这将导致代码高度耦合并且难以维护和调试，本教程将通过示例代码，像你展示控制反转及依赖注入的实现方法及 Spring BeanFactory 实例化 Bean 的过程。

参考技术文档地址：[http://www.cnblogs.com/linzheng/archive/2011/01/03/1925052.html](http://www.cnblogs.com/linzheng/archive/2011/01/03/1925052.html)

Spring-IoC 编程示例地址：[http://www.cnblogs.com/linzheng/archive/2011/01/03/1925062.html](http://www.cnblogs.com/linzheng/archive/2011/01/03/1925062.html) 

## 适合人群

本教程为 Java 中高级人员准备，可以帮助你更好的理解 Spring 框架里的 IoC 容器的实现，帮助你在采用 Spring 框架做开发时解决程序模块间高耦合的问题。

## 学习条件

对于本教程，我们假定你已经对 Java 面向对象编程思想有了深刻的了解，对 Spring 框架及 XML 有了一定接触。
