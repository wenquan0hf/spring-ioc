# Bean 的销毁

在你关闭（或重启）应用程序时，单例（Singleton）Bean 可以再次获得生命周期的回调，你可以在这时销毁 Bean 的一些资源。第一种方法是实现`DisposableBean`接口并实现它的`destroy()`方法。更好的方法是用“destroy-method”在 Bean 的定义时指定销毁方法。
