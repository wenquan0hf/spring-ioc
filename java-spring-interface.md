1、  设计用户持久化类的接口UserDao，代码如下：

public interface UserDao {

    public void save(User user);

    public User load(String name);

}

2、  具体的持久化来必须要继承UserDao接口，并实现它的所有方法。我们还是首先实现内存持久化的用户类：

public class MemoryUserDao implements UserDao{

    private static Map users = new HashMap();;

    static{

        User user = new User("Moxie","pass");

        users.put(user.getName(),user);

    }

    public void save(User user) {

        users.put(user.getId(),user);

    }

    public User load(String name) {

        return (User)users.get(name);

    }

}

MemoryUserDao的实现代码和上面的MemoryUserPersist基本相同，唯一区别是MemoryUserDao类继承了UserDao接口，它的save()和load()方法是实现接口的方法。

这时，客户端UserRegister的代码又该如何实现呢？

UserDao userDao = new MemoryUserDao();

userDao.save(user);

（注：面向对象“多态”的阐述）

如果我们再切换到文本的持久化实现TextUserDao，客户端代码仍然需要手工修改。虽然我们已经使用了面向对象的多态技术，对象userDao方法的执行都是针对接口的调用，但userDao对象的创建却依赖于具体的实现类，比如上面MemoryUserDao。这样我们并没有完全实现前面所说的“Client不必知道其使用对象的具体所属类”。

如何解决客户端对象依赖具体实现类的问题呢？

下面该是我们的工厂（Factory）模式出场了！