# 重构第二步——工厂模式

我们使用一个工厂类来实现`userDao`对象的创建，这样客户端只要知道这一个工厂类就可以了，不用依赖任何具体的`UserDao` 实现。创建`userDao`对象的工厂类`UserDaoFactory`代码如下：

```
public class UserDaoFactory {

    public static UserDao createUserDao(){

          return new MemoryUserDao();

    }

}
```

客户端`UserRegister`代码片断如下：

```
UserDao userDao = UserDaoFactory. CreateUserDao();

userDao.save(user);
```

现在如果再要更换持久化方式，比如使用文本文件持久化用户信息。就算有再多的客户代码调用了用户持久化对象我们都不用担心了。因为客户端和用户持久化对象的具体实现完全解耦。我们唯一要修改的只是一个`UserDaoFactory`类。
