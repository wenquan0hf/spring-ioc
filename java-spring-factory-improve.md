到这里人生的浩劫已经得到了拯救。但我们仍不满足，因为假如将内存持久化改为文本文件持久化仍然有着硬编码的存在——UserDaoFactory类的修改。代码的修改就意味着重新编译、打包、部署甚至引入新的Bug。所以，我们不满足，因为它还不够完美！

如何才是我们心目中的完美方案？至少要消除更换持久化方式时带来的硬编码。具体实现类的可配置不正是我们需要的吗？我们在一个属性文件中配置UserDao的实现类，例如：

在属性文件中可以这样配置：userDao = com.test.MemoryUserDao。UserDao的工厂类将从这个属性文件中取得UserDao实现类的全名，再通过Class.forName(className).newInstance()语句来自动创建一个UserDao接口的具体实例。UserDaoFactory代码如下：

public class UserDaoFactory {

    public static UserDao createUserDao(){

        String className = "";

// ……从属性文件中取得这个UserDao的实现类全名。

        UserDao userDao = null;

        try {

            userDao = (UserDao)Class.forName(className).newInstance();

        } catch (Exception e) {

            e.printStackTrace();

        }

        return userDao;

   }

通过对工厂模式的优化，我们的方案已近乎完美。如果现在要更换持久化方式，不需要再做任何的手工编码，只要修改配置文件中的userDao实现类名，将它设置为你需要更换的持久化类名即可。

我们终于可以松下一口气了？不，矛盾仍然存在。我们引入了接口，引入了工厂模式，让我们的系统高度的灵活和可配置，同时也给开发带来了一些复杂度：1、本来只有一个实现类，后来却要为这个实现类引入了一个接口。2、引入了一个接口，却还需要额外开发一个对应的工厂类。3、工厂类过多时，管理、维护非常困难。比如：当UserDao的实现类是JdbcUserDao，它使用JDBC技术来实现用户信息从持久化。也许要在取得JdbcUserDao实例时传入数据库Connection，这是仍少UserDaoFactory的硬编码。

当然，面接口编程是实现软件的可维护性和可重用行的重要原则已经勿庸置疑。这样，第一个复杂度问题是无法避免的，再说一个接口的开发和维护的工作量是微不足道的。但后面两个复杂度的问题，我们是完全可以解决的：工厂模式的终极方案——IoC模式。