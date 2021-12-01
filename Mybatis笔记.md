# 1.Mybatis：

## 初见Mybatis：

### MyBatis简介

#### **环境说明**：

- jdk 8 +
- MySQL 5.7.19
- maven-3.6.1
- IDEA

学习前需要掌握：

- JDBC
- MySQL
- Java 基础
- Maven
- Junit

#### 什么是Mybatis：

- MyBatis 是一款优秀的持久层框架

- MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集的过程

- MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 实体类 【Plain Old Java Objects,普通的 Java对象】映射成数据库中的记录。

- MyBatis 本是apache的一个开源项目ibatis, 2010年这个项目由apache 迁移到了google code，并且改名为MyBatis 。

- 2013年11月迁移到Github .

- Mybatis官方文档 : http://www.mybatis.org/mybatis-3/zh/index.html

- GitHub : https://github.com/mybatis/mybatis-3

#### 持久化：

**持久化是将程序数据在持久状态和瞬时状态间转换的机制。**

- 即把数据（如内存中的对象）保存到可永久保存的存储设备中（如磁盘）。持久化的主要应用是将内存中的对象存储在数据库中，或者存储在磁盘文件中、XML数据文件中等等。

- JDBC就是一种持久化机制。文件IO也是一种持久化机制。

- 在生活中 : 将鲜肉冷藏，吃的时候再解冻的方法也是。将水果做成罐头的方法也是。

**为什么需要持久化服务呢？那是由于内存本身的缺陷引起的**

- 内存断电后数据会丢失，但有一些对象是无论如何都不能丢失的，比如银行账号等，遗憾的是，人们还无法保证内存永不掉电。

- 内存过于昂贵，与硬盘、光盘等外存相比，内存的价格要高2~3个数量级，而且维持成本也高，至少需要一直供电吧。所以即使对象不需要永久保存，也会因为内存的容量限制不能一直呆在内存中，需要持久化来缓存到外存。

#### 持久层：

**什么是持久层？**

- 完成持久化工作的代码块 .  ---->  dao层 【DAO (Data Access Object)  数据访问对象】

- 大多数情况下特别是企业级应用，数据持久化往往也就意味着将内存中的数据保存到磁盘上加以固化，而持久化的实现过程则大多通过各种关系数据库来完成。

- 不过这里有一个字需要特别强调，也就是所谓的“层”。对于应用系统而言，数据持久功能大多是必不可少的组成部分。也就是说，我们的系统中，已经天然的具备了“持久层”概念？也许是，但也许实际情况并非如此。之所以要独立出一个“持久层”的概念,而不是“持久模块”，“持久单元”，也就意味着，我们的系统架构中，应该有一个相对独立的逻辑层面，专注于数据持久化逻辑的实现.

--- 与系统其他部分相对而言，这个层面应该具有一个较为清晰和严格的逻辑边界。【说白了就是用来操作数据库存在的！】

**为什么需要Mybatis**

- Mybatis就是帮助程序猿将数据存入数据库中 , 和从数据库中取数据 .

- 传统的jdbc操作 , 有很多重复代码块 .比如 : 数据取出时的封装 , 数据库的建立连接等等... , 通过框架可以减少重复代码,提高开发效率 .

- MyBatis 是一个半自动化的ORM框架 (Object Relationship Mapping) -->对象关系映射

- 所有的事情，不用Mybatis依旧可以做到，只是用了它，所有实现会更加简单！技术没有高低之分，只有使用这个技术的人有高低之别

- MyBatis的优点

  - 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件就可以了，易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。

  - 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。

  - 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。

  - 提供xml标签，支持编写动态sql。

  - .......

- 最重要的一点，使用的人多！公司需要！

  ### MyBatis第一个程序

  **思路流程：搭建环境-->导入Mybatis--->编写代码--->测试**

1. 代码演示：

   - 搭建实验数据

     ```mysql
     CREATE DATABASE `mybatis`;
      
     USE `mybatis`;
      
     DROP TABLE IF EXISTS `user`;
      
     CREATE TABLE `user` (
       `id` int(20) NOT NULL,
       `name` varchar(30) DEFAULT NULL,
       `pwd` varchar(30) DEFAULT NULL,
       PRIMARY KEY (`id`)
     ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
      
     insert  into `user`(`id`,`name`,`pwd`) values (1,'狂神','123456'),(2,'张三','abcdef'),(3,'李四','987654');
     ```

   - 导入MyBatis相关 jar 包

     - GitHub上找

     ```xml
     <dependency>
         <groupId>org.mybatis</groupId>
         <artifactId>mybatis</artifactId>
         <version>3.5.2</version>
     </dependency>
     <dependency>
         <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
         <version>5.1.47</version>
     </dependency>
     ```

     3、编写MyBatis核心配置文件

     - 查看帮助文档

     ```xml
     <?xml version="1.0" encoding="UTF-8" ?>
     <!DOCTYPE configuration
             PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
             "http://mybatis.org/dtd/mybatis-3-config.dtd">
     <configuration>
         <environments default="development">
             <environment id="development">
                 <transactionManager type="JDBC"/>
                 <dataSource type="POOLED">
                     <property name="driver" value="com.mysql.jdbc.Driver"/>
                     <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8"/>
                     <property name="username" value="root"/>
                     <property name="password" value="123456"/>
                 </dataSource>
             </environment>
         </environments>
         <mappers>
             <mapper resource="com/kuang/dao/userMapper.xml"/>
         </mappers>
     </configuration>
     ```

     4、编写MyBatis工具类

     - 查看帮助文档

     ```java
     import org.apache.ibatis.io.Resources;
     import org.apache.ibatis.session.SqlSession;
     import org.apache.ibatis.session.SqlSessionFactory;
     import org.apache.ibatis.session.SqlSessionFactoryBuilder;
     import java.io.IOException;
     import java.io.InputStream;
     private static SqlSessionFactory sqlSessionFactory;
     
     public class MybatisUtils {
     static {
         try {
             String resource = "mybatis-config.xml";
             InputStream inputStream = Resources.getResourceAsStream(resource);
             sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
         } catch (IOException e) {
             e.printStackTrace();
         }
     }
      
     //获取SqlSession连接
     public static SqlSession getSession(){
         return sqlSessionFactory.openSession();
     	}
     }
     ```

     5、创建实体类

     ```java
     public class User {
         
         private int id;  //id
         private String name;   //姓名
         private String pwd;   //密码
         
         //构造,有参,无参
         //set/get
         //toString()
         
     }
     ```

     6、编写Mapper接口类

     ```java
     import com.kuang.pojo.User;
     import java.util.List;
      
     public interface UserMapper {
         List<User> selectUser();
     }
     ```

     7、编写Mapper.xml配置文件

     - namespace 十分重要，不能写错！

     ```java
     <?xml version="1.0" encoding="UTF-8" ?>
     <!DOCTYPE mapper
             PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
             "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
     <mapper namespace="com.kuang.dao.UserMapper">
       <select id="selectUser" resultType="com.kuang.pojo.User">
         select * from user
       </select>
     </mapper>
     ```

     8、编写测试类

     - Junit 包测试

     ```java
     public class MyTest {
         @Test
         public void selectUser() {
             SqlSession session = MybatisUtils.getSession();
             //方法一:
             //List<User> users = session.selectList("com.kuang.mapper.UserMapper.selectUser");
             //方法二:
             UserMapper mapper = session.getMapper(UserMapper.class);
             List<User> users = mapper.selectUser();
      
             for (User user: users){
                 System.out.println(user);
             }
             session.close();
         }
     }
     ```

     9、运行测试，成功的查询出来的我们的数据，ok！

#### 问题说明：(静态过滤问题)

**可能出现问题说明：Maven静态资源过滤问题**

资源过滤问题:

报错：java.lang.ExceptionInInitializerError                                                                                                             										 The error may exist in com/atguigu/dao/UserMapper.xml

maven由于他的约定大于配置，我们之后可能遇到我们写的配置文件，无法被导出或则生效的问题，解决方案：

在build中配置resourses，来防止我们的资源到导出失败问题：

```java
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

2.注意点：报错。

org.apache.ibatis.binding.BindingException: Type interface com.atguigu.dao.UserDao is not known to the MapperRegistry.

```java
<!--每一个Mapper.xml都需要在Mybatis核心配置文件注册-->
<mappers>
    <mapper resource="com/atguigu/dao/UserMapper.xml"></mapper>
</mappers>
```

## 2.CRUB

#### 1.namespace：

namespace中的包名要和Dao/mapper接口的包名一致；

#### 2.select：

选择，查询语句；

​	1)id:就是对应的namespace中的方法名

​	2）resultType：Sql语句执行的返回值。

​	3）parameterType：参数类型。

​			编写接口：

```java
//根据ID查询用户
User getUserById(int n);
```

​			编写对应的mapper中的sql语句：

```java
<select id="getUserById" resultType="com.atguigu.pojo.User" parameterType="int">
    select * from mybatis.user where id=#{id}
</select>
```

​			测试：

```java
@Test
public void getUserById(){
    //第一步：获得sqlSession的对象
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    UserDao mapper = sqlSession.getMapper(UserDao.class);
    User user = mapper.getUserById(1);
    System.out.println(user);

    sqlSession.close();

}
```

#### 3.insert

```java
<insert id="addUser" parameterType="com.atguigu.pojo.User">
    insert into mybatis.user(id,name,pwd)values(#{id},#{name},#{pwd})
</insert>
```

#### 4.update

```java
<update id="upDate" parameterType="com.atguigu.pojo.User">
    update mybatis.user set name = #{name},pwd = #{pwd} where id= #{id}
</update>
```

#### 5.delete

``` java
<delete id="deleteUser" parameterType="int">
    delete from mybatis.user where id = #{id}
</delete>
```

**注意事项：**

```java
//增删改时需要提交事务
sqlSession.commit();

//所有关于数据的操作，完成之后需要关闭数据库
sqlSession.close();
```



### 1.万能的map

假设，我们的实体类，或则数据库中的表，字段或则参数过多，我们应当考虑使用Map；

```java
//万能的map
int addUser2(Map<String , Object> map);
```

```java
<insert id="addUser2" parameterType="map">
    insert into mybatis.user(id,name,pwd)values(#{userId},#{userName},#{passWord})
</insert>
```

```java
@Test
public void addUser2(){
    //第一步：获得sqlSession的对象
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    UserDao mapper = sqlSession.getMapper(UserDao.class);

    Map<String,Object> map = new HashMap<>();
    map.put("userId",5);
    map.put("userName","Hello");
    map.put("passWord","123456");

    mapper.addUser2(map);

    //提交事务
    sqlSession.commit();
    //关闭数据库
    sqlSession.close();
}
```

Map传递参数，直接在sql中取出key即可！【parameterType=“map”】

对象传递参数，直接在sql中取对象属性即可！【parameterType=“Object”】

只有一个基本类型参数的情况下，可以直接在sql中取到。

多个参数要用Map。或则**注解**！

### 2.思考题：

模糊查询怎么写？

1.java代码执行的时候，传递通配符%%；

```java
List<User> userList = userMapper.getUserLike("%陈%");
```

2.在sql拼接中使用通配符！

  

 ## 3.配置解析

### 1.核心配置文件

- mybatis-config.xml
- Mybatis的配置文件包含了会深深影响Mybatis行为的设置和属性信息；

- configuration（配置）（类型处理器，对象工厂，插件不用理解）
  - [properties（属性）](https://mybatis.org/mybatis-3/zh/configuration.html#properties)
  - [settings（设置）](https://mybatis.org/mybatis-3/zh/configuration.html#settings)
  - [typeAliases（类型别名）](https://mybatis.org/mybatis-3/zh/configuration.html#typeAliases)
  - [typeHandlers（类型处理器）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)
  - [objectFactory（对象工厂）](https://mybatis.org/mybatis-3/zh/configuration.html#objectFactory)
  - [plugins（插件）](https://mybatis.org/mybatis-3/zh/configuration.html#plugins)
  - environments（环境配置）
    - environment（环境变量）
      - transactionManager（事务管理器）
      - dataSource（数据源）
  - [databaseIdProvider（数据库厂商标识）](https://mybatis.org/mybatis-3/zh/configuration.html#databaseIdProvider)
  - [mappers（映射器）](https://mybatis.org/mybatis-3/zh/configuration.html#mappers)

### 2.环境配置（environment）

Mybatis可以配置成适应多种环境

不过要记住：尽管可以配置多个环境，但每个SqlSessionFactory实例只可能选择一种环境

学会使用配置多套运行环境

Mybatis默认的事物管理器就是JDBC，连接池，POOLED

### 3.属性（properties）

我们可以通过properties属性来实现应用配置文件

这些属性都是课外部配置且可以动态替换的，既可以在典型的java属性文件中配置，亦可以通过properties元素的子元素进行配置。【db.properties】

编写一个配置文件：

**在xml中。所有的标签都可以规定其顺序。不能随意的乱写**

db.properties

```java 
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=true&useUnicode=true&characterEncoding=UTF-8
username=root
password=123456
```

在核心配置文件中引入

```java
<properties resource="db.properties">
    <property name="password" value="123456"/>
</properties>
```

- 可以直接引入外部文件；
- 可以在其中增加一些属性配置
- 如果两个文件有同一字段，优先使用外部配置文件！

### 4.类型别名（typeAliases）

- 类型别名是为java类型设置一个短的名字
- 存在的意义仅仅在于减少类完全限定名的繁琐

```properties
<!--可以给实体类其别名-->
<typeAliases>
    <typeAlias type="com.atguigu.pojo.User" alias="User"></typeAlias>
</typeAliases>
```

也可以指定一个包名，MyBatis会在包名下搜索需要的java Bean，比如：

**扫描实体类的包，它的默认别名就是为这个类的类名，首字母最好小写！**

```properties
//或则可以这样写
<typeAliases>
    <package name="com.atguigu.pojo"/>
</typeAliases>
```

- 在实体类较少的时候，使用第一种方式
- 如果实体类非常的多，建议使用第二种
- 第一种可以DIY（自定义）别名，第二种则不行 ，如果非要改，需要在实体类上增加注解。 

```
@Alias("user")
public class User {
```

### 5.设置

这是Mybatis中及其重要的调整设置，它们会改变Mybatis的运行时行为。

### 6.引射器（mapper）

MapperRedistry：注册绑定我们的Mapper文件

#### 方式一：使用resourse（推荐使用）

```java
<!--每一个Mapper.xml都需要在Mybatis核心配置文件注册-->
<mappers>
    <mapper resource="com/atguigu/dao/UserMapper.xml"></mapper>
</mappers>
```

#### 方式二：使用class文件绑定注册

```java
    <!--每一个Mapper.xml都需要在Mybatis核心配置文件注册-->
    <mappers>
        <mapper class="com.atguigu.dao.UserMapper"></mapper>
    </mappers>
```

**注意点：**

- 接口和它的Mapper配置文件必须同名；
- 接口和它的Mapper配置文件必须在同一包下；

#### 方式三：使用扫描包进行注册绑定：

```java
    <!--每一个Mapper.xml都需要在Mybatis核心配置文件注册-->
    <mappers>
        <package name="com.atguigu.dao"/>
    </mappers>
```

**注意点：**

- 接口和它的Mapper配置文件必须同名；
- 接口和它的Mapper配置文件必须在同一包下；

### 7.生命周期与作用域：

**不同作用域和生命周期类别是至关重要的，因为错误的使用会导致非常严重的。** 

![image-20210813165233899](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813165233899.png)

**SqlSessionFactoryBuilder:**

- 一旦创建了SqlSessionFactory，就不需要他了；

- 局部变量

  

**SqlSessionFactory：**

- 说白了就是可以想象为：数据库连接池

- SqlSessionFactory一旦被创建就应该在应用期间一直存在，**没有任何理由丢弃或则重新创建另外一个实例**

- 因为SqlSessionFactory的最佳作用域是应用作用域。

- 最简单的就是使用**单例模式**或则是静态单例模式。

  

**SqlSession:**

- 链接到连接池的一个请求！
- SqlSession的实例不是线程安全的，因此是不能被共享的，所以他的最佳的作用域是请求或方法作用域
- 用完之后需要赶紧关闭，否则资源浪费。

![image-20210813170503671](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813170503671.png)



这里面的每一个Mapper，就代表一个具体的业务!

## 4.解决属性名和字段名不一致的问题：

#### 1.数据库中的字段：

![image-20210813200558598](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813200558598.png)

新建一个文件夹，拷贝之前的，测试实体类字段不一致的情况。

![image-20210813200727057](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813200727057.png)

测试出现的问题：

最后的password中的值为null；

```
//select * from mybatis.user where id=#{id}
//类型处理器
//select  id,name,pwd mybatis.user where id=#{id}
```

解决方法;

- 其别名：

```
<select id="getUserById" resultMap="UserMap">
    //select  id,name,pwd as password mybatis.user where id=#{id}
</select>
```

#### 2.resultMap

结果集映射

```java
id name pwd 
id name password
```

```java
<!--结果集映射  id：resultMap后面的，type：返回值类型-->
<resultMap id="UserMap" type="User">
    <!--column:数据库中的字段，property实体类中的属性-->
    <result column="id" property="id"></result>
    <result column="name" property="name"></result>
    <result column="pwd" property="password"></result>
</resultMap>

<select id="getUserById" resultMap="UserMap">
    select * from mybatis.user where id=#{id}
</select>
```

- resultMap元素Mybatis中最重要最强大的元素
- ResultMap的设计思想是，对于简单的语句根本不需要配置显示的结果映射，而对于复杂一点的语句只需要描述它们的关系就行了。
- ResultMap最优秀的地方在于，虽然你已经对它相当的了解，但是根本就不需要显式的用到它们。
- 如果世界总是这么简单就好了。

## 5.日志

#### 1.日志工厂（基于配置文件settings中的iogImpl）

如果一个数据库操作出现了异常，我们需要拍错，日志就是最好的助手！

曾经：sout，debug

现在：日志工厂！

![image-20210813215837775](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813215837775.png)

- SLF4J 
- LOG4J 【掌握】
- LOG4J2 
- JDK_LOGGING
- COMMONS_LOGGING
- STDOUT_LOGGING 【掌握】
- NO_LOGGING



在mybatis中具体使用哪个日志实现，在设置中设定！

STDOUT_LOGGING标准日志输出、

在mybatis核心配置文件中，配置我们的日志；



```
<settings>
    <!--标准的日志工厂实现-->
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```



![image-20210813221700813](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813221700813.png)

#### 2.LOG4J：

什么是LOG4J：

- Log4j是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件
- 我们也可以控制每一条日志的输出格式
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。
- 通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置，而不需要修改应用的代码。

1.先导入LOG4J的包；

```java
<!-- https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

2.logj的配置文件：

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/atguigu.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

3.配置log4j为日志的实现：

```
 <settings>
        <!--标准的日志工厂实现-->
		<!--<setting name="logImpl" value="STDOUT_LOGGING"/>-->
        <setting name="logImpl" value="LOG4J"/>
    </settings>
```

4.log4的使用：直接测试运行刚才的查询。

![image-20210814142901324](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210814142901324.png)

**简单的使用:**

1.在要使用的Log4j的类中，导入包import org。apache.log4 j.Logger;

2.日志对象，参数为当前类的class

```java
static Logger logger = Logger.getLogger(UserDaoTest.class);
```

3.日志级别：

```java
logger.info("info:进入了testLog4j");
logger.debug("debug:进入了testLog4j");
logger.error("error:进入了testLog4j");
```

## 6.分页

### 1.使用Limit分页;

```java
语法：SELECT * FROM USER LIMIT STARTINDEX,PAGESIZE;
select * from user limit 3；   相当于[0,3]
```



使用Mybatis实现分页，核心SQL

1.接口：

```java
//分页
List<User> getUserByLimit(Map<String,Integer> map);
```

2.Mapper.xml

```java
<!--分页-->
<select id="getUserByLimit" parameter="map" resultMap="userMap">
    select * from mybatis.user Limit #{startIndex},#{pageSize}
</select>
```

3.测试：

```java
@Test
public void getUserByLimit(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    HashMap<String, Integer> map = new HashMap<>();
    map.put("startIndex",1);
    map.put("pageSize",2);

    List<User> userByLimit = mapper.getUserByLimit(map);
    for (User user : userByLimit) {
        System.out.println(user);
    }
}
```

  ## 7.使用注解开发：

1.注解在接口上实现：

```java
//使用注解来查询用户
@Select("select * from user")
List <User> getUsers();
```

2.需要在核心配置文件中绑定接口：

```java
<!--绑定接口-->
<mappers>
    <mapper class="com.atguigu.dao.UserMapper"></mapper>
</mappers>
```

3.测试；



本质：反射机制实现

底层：动态代理；



![流程图](流程图.png)

 ### 使用注解来实现增删改查

我们可以在工具类创建的时候实现自动提交事务！

```java
//既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession的实例。
    // SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession(true);//加上参数true为自动提交；
    }
```

编写接口，增加注解

```java
public interface UserMapper {
    //使用注解来查询用户
    @Select("select * from user")
    List <User> getUsers();

    //方法存在多个参数的时候，所有的参数前面必须加上@param（“参数名”）注解；前提是基本类型或String类型。
    @Select("select * from user where id = #{id}")
    User getUserByID(@Param("id") int id);

    @Insert("insert into user(id,name,pwd) values (#{id},#{name},#{password})")
    int addUser(User user);

    @Update("update user set name=#{name},pwd=#{password} where id = #{id}")
    int updateUser(User user);

    @Delete("delete from user where id = #{id}")
    int deleteUser(@Param("id") int id);
}

```

测试：

【注意：我们必须要将接口注册绑定到我们的核心配置文件中！注意resourse和class的区别】



**关于@Param（）注解**

- 基本类型的参数或则String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，但是建议大家都加上
- 我们在SQL中引用的就是我们这里的@Param()中设定的属性名；

## 8.Locbok()

备：主要简化实体类（pojo）的代码量

1.使用步骤：

- 在IDEA中安装Locbok插件

- 在项目中导入lombok的jar包

```java
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
</dependency>
```

- 在实体类上加注解：

```java
@Data  //构建 getter setting toString方法
@AllArgsConstructor//构建有参构造
@NoArgsConstructor//构建无参构造
```



```java
@Getter and @Setter
@FieldNameConstants
@ToString
@EqualsAndHashCode
@AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
@Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
@Data
@Builder
@SuperBuilder
@Singular
@Delegate
@Value
@Accessors
@Wither
@With
@SneakyThrows
```

@Date：无参构造，get，set，toString,hashcode,equals

## 9.多对一处理

多对一：

![image-20210816145605246](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210816145605246.png)

- 多个学生，对应一个老师
- 对于学生这边而言，关联，，多个学生，关联一个老师（多对一）
- 对于老师而言，集合，一个老师，有很多个学生（一对多)

SQL:

```sql
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO teacher(`id`, `name`) VALUES (1, 秦老师); 

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8INSERT INTO `student` (`id`, `name`, `tid`) VALUES (1, 小明, 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (2, 小红, 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (3, 小张, 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (4, 小李, 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (5, 小王, 1);
```



### 测试环境搭建

1.导入lombok

2.新建实体类Teacher，Student

3.建立Mapper接口

4.建立Mapper.XML文件

5.在核心配置文件中绑定注册我们的Mapper接口或则文件！[方式较多，自己选]

6.测试查询是否能够成功！

### 

### 按照查询嵌套处理

```xml
    <!--
    思路：
        1.查询所有学生信息
        2.根据查询出来的学生的tid，寻找对应的老师！  类似于子查询；
    -->
    <select id="getStudent" resultMap="StudentTeacher">
        select * from student
    </select>
    <resultMap id="StudentTeacher" type="Student">
        <result property="id" column="id"></result>
        <result property="name" column="name"></result>
        <!--复杂的属性，我们需要单独处理  对象：association   集合：collection-->
        <association property="teacher" column="tid" javaType="Teacher" 		       select="getTeacher"></association>
    </resultMap>

    <select id="getTeacher" resultType="Teacher">
        select * from teacher where id = #{id}
    </select>
```

回顾Mysql多对一查询方式：

- 子查询
- 连表查询 

## 10一对多处理

比如：一个老师拥有多个学生

对于老师而言，就是一对多的关系

### 环境搭建



**1.环境搭建，和以前的一样，快速搭建：**

实体类：

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Student {
    private int id;
    private String name;

    //学生需要关联一个老师
    private int tid;
}
```

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Teacher {
    private int id;
    private String name;

    //一个老师有很多的学生
    private List<Student> students;
}
```

#### 按照结果嵌套查询

```jAVA
<!--按结果嵌套查询-->
    <select id="getTeacher" resultMap="TeacherStudent">
        select s.id sid,s.name sname,t.name tname,t.id tid
        from student s,teacher t
        where s.tid = t.id and t.id = #{tid}
    </select>

    <resultMap id="TeacherStudent" type="Teacher">
        <result property="id" column="tid"></result>
        <result property="name" column="tname"></result>
        <!--复杂的属性，我们需要单独处理  对象：association   集合：collection
        javaType="" 指定属性的类型
        集合中的泛型信息，我们使用ofType获取；
        -->
        <collection property="students" ofType="Student">
            <result property="id" column="sid"></result>
            <result property="name" column="sname"></result>
            <result property="tid" column="tid"></result>
        </collection>
    </resultMap>
```

#### 按照查询嵌套处理

```java
    <!--按照查询嵌套处理-->
    <select id="getTeaacher2" resultMap="TeacherStudent2">
        select * from mybatis.teacher where id = #{tid}
    </select>

    <resultMap id="TeacherStudent2" type="Teacher">
        <collection property="students" javaType="ArrayList" ofType="Student" select="getStudentByTeacherId" column="id">

        </collection>
    </resultMap>

    <select id="getStudentByTeacherId" resultType="Student">
        select * from mybatis.student where tid = #{tid}
    </select>
```

### 小结：

1. 关联 - association 【多对一】
2. 集合 - collection 【一对多】
3. javaType   &  ofType
   - javaType 用来指定实体类中的属性的类型
   - ofType 用来指定映射到List或则集合中的pojo类型，泛型中的约束类型！

**注意点：**

- 保证SQL的可读性，尽量保证通俗易懂

- 注意一对多和多对一中，属性名和字段名的问题

- 如果问题不好排查错误。可以使用日志，建议使用Log4j

  

## 11.动态SQL

**什么是动态SQL：动态SQL就是指根据不同的条件生成不同的SQL语句**

动态 SQL 是 MyBatis 的强大特性之一。如果你使用过 JDBC 或其它类似的框架，你应该能理解根据不同条件拼接 SQL 语句有多痛苦，例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL，可以彻底摆脱这种痛苦。

```java
动态 SQL 元素可能会感觉似曾相识。在 MyBatis 之前的版本中，需要花时间了解大量的元素。借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。
   	if
	choose (when, otherwise)
	trim (where, set)
	foreach 
```

### 搭建环境

```java
CREATE TABLE `blog`(
`id` VARCHAR(50) NOT NULL COMMENT 博客id,
`title` VARCHAR(100) NOT NULL COMMENT 博客标题,
`author` VARCHAR(30) NOT NULL COMMENT 博客作者,
`create_time` DATETIME NOT NULL COMMENT 创建时间,
`views` INT(30) NOT NULL COMMENT 浏览量
)ENGINE=INNODB DEFAULT CHARSET=utf8 
```



创建一个基础工程

1. 导包
2. 编写配置文件
3. 编写实体类
4. 编写实体类对应的Mapper接口和Mapper.XML文件



### IF

```xml
    <select id="queryBlogIf" parameterType="map" resultType="Blog">
        select * from mybatis.blog where 1=1
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </select>
```

### choose(where.set)

类似于switch case：只会拼接一项。

```xml
    <select id="queryBlogChoose" resultType="Blog" parameterType="map">
-- //when :相当于switch  case中的case,otherwise相当于default。都满足只拼接第一项；
        select * from mybatis.blog
        <where>
            <choose>
                <when test="title!=null">
                    title = #{title}
                </when>
                <when test="author!=null">
                    author = #{author}
                </when>
                <otherwise>
                    and views = #{views}
                </otherwise>
            </choose>
        </where>
    </select>
```

### trim(where,set)

where:防止拼接字符串出现问题；（第一个的拼接关键字可以省略）

```xml
<select id="queryBlogIf" parameterType="map" resultType="Blog">
    select * from mybatis.blog 
    <where>
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
    </where>
</select>
```

**set：**

```xml
<update id="updateBlog" parameterType="map">
    update mybatis.blog
    <set>
        <if test="title !=null">
            title = #{title}
        </if>
        <if test="author !=null">
            author = #{author}
        </if>
    </set>
    where id = #{id}
</update>
```

所谓的动态SQL，本质还是SQL语句，只是我们可以在SQL层面上，去执行一个逻辑代码

if  where  set  choose  when



### SQL片段：

有的时候，我们可能会将一些功能的部分抽取出来，方便使用

1.使用SQL标签抽取公共的部分

```XML
<sql id="if_title_author">
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </sql>
```

2.在需要使用的地方使用include标签引用即可

```xml
 	<select id="queryBlogIf" parameterType="map" resultType="Blog">
        select * from mybatis.blog
        <where>
            <include refid="if_title_author"></include>
        </where>
    </select>
```

**注意事项：**

​	1.最好是基于表单来定义SQL片段的！

​	2.不要存在where标签



### Foreach：

动态 SQL 的另一个常见使用场景是对集合进行遍历（尤其是在构建 IN 条件语句的时候）。比如：

```java
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
```

*foreach* 元素的功能非常强大，它允许你指定一个集合，声明可以在元素体内使用的集合项（item）和索引（index）变量。它也允许你指定开头与结尾的字符串以及集合项迭代之间的分隔符。这个元素也不会错误地添加多余的分隔符，看它多智能！

**提示** 你可以将任何可迭代对象（如 List、Set 等）、Map 对象或者数组对象作为集合参数传递给 *foreach*。当使用可迭代对象或者数组时，index 是当前迭代的序号，item 的值是本次迭代获取到的元素。当使用 Map 对象（或者 Map.Entry 对象的集合）时，index 是键，item 是值。

至此，我们已经完成了与 XML 配置及映射文件相关的讨论。下一章将详细探讨 Java API，以便你能充分利用已经创建的映射配置。

![image-20210817214121363](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210817214121363.png)

```xml
    <!--    
    select * from mybatis.blog where 1=1 and (id=1 or id = 2 or id = 3)
    我们现在传递一个万能的map，这个map中可以存在一个集合！
    -->
    <select id="queryBlogForeach" parameterType="map" resultType="Blog">
        select * from mybatis.blog
        <where>
            <foreach collection="ids" item="id" open="and (" close=")" separator="or">
                id = #{id}
            </foreach>
        </where>
    </select>
```

**动态SQL就是拼接SQL语句。我们只要保证SQL的正确性，按照SQL的格式，去排列组合就可以了**

建议：

- 现在Mysql中写出完整的SQL。在对应的去修改成为我们的动态SQL实现通用即可

## 12.缓存（了解）

### 1.简介

```java
查询：连接数据库 ， 耗资源！
    一次查询的结果，给他暂存在一个可以直接取到的地方！--》内存：缓存
    
    我们再次查询相同的数据的时候，直接走缓存，就不用了走数据库了
```

![image-20210817215818989](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210817215818989.png)

### 2.Mybatis缓存

- Mybatis包含一个非常强大的查询缓存特性，它可以非常方便的定制和配置缓存，缓存可以极大的提升查询效率。
- Mybatis系统中默认定义了两级缓存：一集缓存和二级缓存
  - 默认情况下。只有一级缓存开启。（SqlSession级别的缓存，也称为本地缓存）
  - 二级缓存需要手动开启和配置，它基于namespace级别的缓存
  - 为了提高扩展性，Mybatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存

### 3.一级缓存

- 一级缓存也叫本地缓存
  - 与数据库同一次会话期间查询到的数据会放在本地缓存中。
  - 以后如果需要获取相同的数据，直接从缓存中拿，没必要再去查询数据库；

**测试：**

- 开启日志
- 测试在一个SqlSession中查询两次相同的记录
- 查看日志输出：
- ![image-20210818090835086](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210818090835086.png)

- 缓存失效： 

  - 查询不同的东西

  - 增删改操作，可能会改变原来的数据，所以必定会刷新缓存。

  - 查询不同的Mapper.xml

  - 手动清理缓存

    ![image-20210818092104783](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210818092104783.png)

**小结：**

一级缓存默认是开启的，只在一次SqlSession中有效，也就是拿到连接到关闭连接这个区间段！

### 4.二级缓存

- 耳机缓存也叫做全局缓存，一级缓存作用域太低了，所以诞生了二级缓存。

- 基于namespace级别的缓存，一个名称空间，对应一个二级缓存；

- 工作机制

  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中
- 如果当前的会话关闭，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据被保存到二级缓存中；
  - 新的会话查询信息，就可以从二级缓存中获取内容；
- 不同的mapper查处的数据会放在自己对应的缓存（map）中；

**步骤：**

1. 开启全局缓存:在核心配置文件中配置；

   ```java 
     <setting name="cacheEnables" value="true"/>
   ```

2. 在要使用二级缓存的Mapper中开启

   ```xml
    <!--在当前Mapper.xml中使用二级缓存-->
    <cache/>
   ```

   也可以自定义参数：

   ```XML
       <cache
            eviction="FIFO"
            flushInterval="60000"
            readOnly="true"
            size="512"/>
   ```

3. 测试：问题：我们需要将实体类序列化！否则的话会报错！

   ![image-20210818104709874](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210818104709874.png)

小结：

- 只要开启了二级缓存，在同一个Mapper在才有用
- 所有的数据会先放在一级缓存中；
- 只有当会话提交，或则关闭的时候，才会提交到二级缓存中。

## 5.缓存原理

![image-20210818105542912](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210818105542912.png)

# 代理模式

为什么要学习代理模式？因为这就是SpringAOP的底层（SpringAOP和SpringMVC）

代理模式的分类：

- 静态代理
- 动态代理

![image-20210818153604064](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210818153604064.png)

## 1.静态代理：

**角色分析：**

- 抽象角色：一般会使用接口或则抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
- 客户：访问代理对象的人！



代码步骤：

1. 接口

   ```java
   //租房
   public interface Rent {
       public void rent();
   }
   ```

2. 真实角色

   ```java
   //房东
   public class Host implements Rent{
       public void rent(){
           System.out.println("房东要出租房子！");
       }
   }
   ```

3. 代理角色

   ```java
   public class Proxy {
   
       private Host host;
   
       public Proxy() {
       }
   
       public Proxy(Host host) {
           this.host = host;
       }
   
       public void rent(){
           host.rent();
           seeHouse();
           hetong();
           fare();
       }
   
       //看房
       public void seeHouse(){
           System.out.println("中介带你看房！");
       }
   
       //签合同
       public void hetong(){
           System.out.println("中介带你签合同！");
       }
   
       //看房
       public void fare(){
           System.out.println("收中介费！");
       }
   }
   ```

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
           //房东要租房子
           Host host = new Host();
           //代理，中介帮房东租房子，但是呢？代理角色一般会有一些附属操作
           Proxy proxy = new Proxy();
   
           //你不用面对房东，直接找中介租房即可！
           proxy.rent();
       }
   }
   ```

**代理模式的好处：**

- 可以使真实角色的操作更加的纯粹！不用去关注一些公共的业务
- 公共也就是交给代理角色，实现业务分工！
- 公共业务发生扩展的时候，方便集中管理

缺点：

- 一个真实角色就会产生一个代理介绍；代码量会翻倍，开发效率会变低。

**了解Aop**

![image-20210818163802395](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210818163802395.png)

## 2.动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的！
- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口---JDK动态代理
  - 基于类：cglib
  - java字节码实现：javasist



需要了解两个类：Proxy：代理，InvocationHandler：调用处理程序



动态代理的好处：

- 可以使真实角色的操作更加的纯粹！不用去关注一些公共的业务
- 公共也就是交给代理角色，实现业务分工！
- 公共业务发生扩展的时候，方便集中管理
- 一个动态代理的是一个接口，一般就是对应一类业务

# 整合Mybatis

步骤：

1.导入相关的jar包

- junit
- mybatis
- mysql数据库
- spring相关的
- aop织入
- mybatis-spring【new】


```xml
<!--整合mybatis和Spring想要的包-->
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.1</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.25</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.7</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.8</version>
        </dependency>
        <!-- Spring操作数据库的话，还需要一个spring-jdbc-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.3.8</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.6</version>
        </dependency>
		<!--整合mybatis和spring的包-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.6</version>
        </dependency>
        <!--用注解来代替get，set等方法-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.20</version>
        </dependency>
        <!--Maven 静态资源过滤问题-->
    </dependencies>
	<build>
         <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```



2.编写配置文件

3.测试



### Mybatis-spring

1.编写数据源头配置

2.sqlSessionFactory

3.sqlSessionTemplate

4.需要给接口加实现类【】

5.将自己写的实现类，注入到Spring中。

6.测试使用即可！

**具体代码看：D:/back/com.atguigu_mybatis中的mybatis-spring**

**UserMpperImpl**和下面的applicationContext.xml配套；

```java
package com.atguigu.mapper;

import com.atguigu.pojo.User;
import org.mybatis.spring.SqlSessionTemplate;
import org.mybatis.spring.support.SqlSessionDaoSupport;

public class UserMapperImpl extends SqlSessionDaoSupport implements UserMapper{

    @Override
    public User getUserById(int n) {
        User user = new User(5,"王杰","123456");

        UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
        mapper.addUser(user);
        mapper.deleteUser(5);
        return mapper.getUserById(1);
    }

    @Override
    public int addUser(User user) {
        return getSqlSession().getMapper(UserMapper.class).addUser(user);
    }

    @Override
    public int deleteUser(int id) {
        return getSqlSession().getMapper(UserMapper.class).deleteUser(5);
    }
}
```

**applicationContext.xml**（和上面的UserMpperImpl配套）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">


    <import resource="spring_dao.xml"></import>
    <bean id="userMapper" class="com.atguigu.mapper.UserMapperImpl">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
    </bean>

</beans>
```



**mybatis-config.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>

    <typeAliases>
        <typeAlias type="com.atguigu.pojo.User" alias="User"></typeAlias>
    </typeAliases>


</configuration>
```



**一个比较全的spring-dao.xml**（包含事务处理）

```xml


<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
                           http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!--DataSource:使用Spring的数据源来替换Mybatis的配置   c3p0   dbcp  druid
        我们这里使用Spring提供的JDBC：org.springframework.jdbc.datasource
    -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
        <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"></property>
        <property name="username" value="root"></property>
        <property name="password" value="123456"></property>
    </bean>

    <!--sqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"></property>
        <!--绑定Mybatis的配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"></property>
        <property name="mapperLocations" value="classpath:com/atguigu/mapper/*.xml"></property>
     </bean>

    <!-- SqlSessionTemplate:就是我们使用的sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <!--只能使用构造器注入sqlSessionFactory。因为它没有set方法-->
        <constructor-arg index="0" ref="sqlSessionFactory"></constructor-arg>
    </bean>

    <!--配置声明式事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!--结合Aop实现事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--给那些方法配置事务-->
        <!--配置事务的传播特性：new propagation=-->
        <tx:attributes>
            <!--对增加方法-->
            <tx:method name="add" propagation="REQUIRED"/>
            <!--对删除方法-->
            <tx:method name="delete" propagation="REQUIRED"/>
            <!--对更改方法-->
            <tx:method name="update" propagation="REQUIRED"/>
            <!--对查询方法-->
            <tx:method name="query" propagation="REQUIRED"/>
            <!--对全部方法，写这一个就行-->
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>

    <!--配置事务切入-->
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(* com.atguigu.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"></aop:advisor>
    </aop:config>
</beans>
```



### 声明式事务

1.回顾事务

- 把一组业务当成一个业务来做；要么都成功，要么都失败！
- 事务在项目开发中，十分的重要，涉及到数据的一致性问题，不能马虎
- 确保完整性和一致性



**事务SCID原则：**

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源。防止数据损坏
- 持久性
  - 事务一旦提交，无论系统发生问题，结果都不会在被影响，被持久化的写到储存器中！

### spring中的事务管理

- 声明式事务：Aop
- 编程式事务：需要在代码中，进行事务的管理



思考：

为什么需要事务？

- 如果不配置事务，可能存在数据提交不一致的情况；
- 如果我们不在Spring中去配置声明式事务，我们就需要在代码中手动的配置事务。
- 事务在项目的开发中十分的重要，设计到数据的一致性和完整性问题，不容马虎！

```xml
 <!--配置声明式事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!--结合Aop实现事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--给那些方法配置事务-->
        <!--配置事务的传播特性：new propagation=-->
        <tx:attributes>
            <!--对增加方法-->
            <tx:method name="add" propagation="REQUIRED"/>
            <!--对删除方法-->
            <tx:method name="delete" propagation="REQUIRED"/>
            <!--对更改方法-->
            <tx:method name="update" propagation="REQUIRED"/>
            <!--对查询方法-->
            <tx:method name="query" propagation="REQUIRED"/>
            <!--对全部方法，写这一个就行-->
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>

    <!--配置事务切入-->
    <aop:config>
        //这个可以当模板，只需要修改：expression="execution(* com.atguigu.mapper.*.*(..))"里面			的路径即可。
        <aop:pointcut id="txPointCut" expression="execution(* com.atguigu.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"></aop:advisor>
    </aop:config>
```



























# 注解和反射

## 注解（Annotation） 

### 什么是注解

注释是给人看的，注解是给机器看的

### 注解的作用

- 不是程序本身，但是可以对程序做出解释
- 可以被其他程序读取（比如： 编译器）

### 注解的格式

```java
@注解名
```

### Annotation的使用位置

package，class，method，field

### 内置注解

@override  重写

@deprecated   表示不推荐使用

@suppressWarning()  正压注解

### 元注解（meta-annotation）

#### 作用

负责解释其他注解的注解

#### 标准注解（四个）

@target  用于描述注解的使用范围（即：被描述的注解可以在什么地方使用）

@retention   表示需要在什么级别保存该注释信息，用于描述注解的生命周期。

@Document   说明该注解将被包含在javadoc中

@inherited 说明子类可以继承父类中的该注解。

#### 自定义注解可以有参数

参数类型 +参数名（）；

参数类型 + 参数名()  default  默认值;

```java
//定义一个注解
public class Test03{
    //注解可以显示赋值，如果没有默认值，我们就必须给注解赋值
    @MyAnnotation2(age=18,name="哈哈")
    pulic void test(){}
}

//Target 表示我们的注解可以用在哪些地方                           重点
@Target({ElementType.TYPE, ElementType.METHOD})

//Retention 表示我们的注解在什么地方还有效
//runtiome>class>sourse                                      重点
@Retention(RetentionPolicy.RUNTIME)

//Documented 表示是否将我们的注解生成在Javadac中
@Documented

//Inherited 子类可以继承父类的注解；
@Inherited
@interface MyAnnotation02 {
    //注解的参数：参数类型 + 参数名（）；
    String name() default "";
    int age();
    int id() default -1;     //如果默认值为-1，代表不存在。
}
```

name为注解的参数名 ，default 后面的是默认值，如果我们不设置默认值，则使用注解额时候必须传参



自定义注意：

- 使用@interface自定义注解时，自动继承了java.lang.annotation.Annotation接口



**分析：**

- @interfacey用来声明一个注解，格式：public@interface注解名{定义内容}
- 其中的每一方式实际上是声明了一个配置参数。
- 方法的名称就是参数的名称。
- 返回值类型就是参数的类型（返回值只能是基本类型，Class，String，enum）
- 可以通过default来声明参数的默认值。
- 如果只有一个参数成员，一般参数名为value。
- 注解元素必须要有值，我们定义注解元素时，经常使用空字符串，0作为默认值。

## 反射：

![image-20210814211722824](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210814211722824.png)

![image-20210814211759861](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210814211759861.png)

### 类加载

同一个字节码文件在运行过程中只会加载一次。通过下面三种方式获取的类对象都是一个对象。

### 获取类对象的三种方式：

```java
Class.forName("全类名");
类名.class;
对象.getClass();    
```

```java
public class Test_01 {
    public static void main(String[] args) throws ClassNotFoundException {
        Person person = new Student();
        System.out.println("这个人是："+person.name);

        //方式一：通过对象获得
        Class c1 = person.getClass();
        System.out.println(c1.hashCode());

        //方式二：forname获得；
        Class c2 = Class.forName("cmd.Student");
        System.out.println(c2.hashCode());

        //方式三：通过类名.class获得
        Class c3 = Student.class;
        System.out.println(c3.hashCode());
    }
}
class Person{
    public String name;
    public Person() {
    }

    public Person(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                '}';
    }
}
class Student extends Person{
    public Student(){
        this.name="学生";
    }
}
```

第一种多用于 配置文件，将类名定义在配置文件中。读取文件，加载类；

第二种多用于参数的传递；

第三种多用于对象的传递；



### 那些类可以有Class对象

-    class：外部类，成员（成员内部类，静态内部类），局部内部类，匿名内部类。

- interface：接口

- []:数组

- enum：枚举

- annotation：注解@interface

- primitive type：基本数据类型

- void

- ```java
  Class c1 = Object.class;//类
  Class c2 = Comparable.class;//接口
  Class c3 = String[].class;//一位数组
  Class c4 = int[][].class;//二维数组
  Class c5 = Override.class;//注解
  Class c6 = ElementType.class;//枚举
  Class c7 = Integer.class;//基本数据类型
  Class c8 = void.class;//void
  Class c9 = Class.class;//Class
  
  //只要元素类型与维度一样，就是同一个class
  int[]a = new int[10];
  int[] b = new int[100];
  ```

### 什么时候进行类的初始化

 > 类的主动引用

  - 虚拟机启动，先初始化main方法所在的类
  - new 一个对象
  - 调用静态成员，（除final之外的常量）和静态方法
  - 通过java.ang.reflect 包进行反射调用
  - 当初始化一个类的时候如果父类没有被初始化，则先初始化其父类

> 类的被动引用(不会引发类的初始化)

- 当访问一个静态时，只有真正声明这个域的类才会被初始化。
  - 如：当通过子类引用父类的静态变量，不会导致子类初始化
- 当通过数组定义类的引用，不会触发类的初始化
- 引用常量不会触发此类的初始化（常量在链接阶段就存入调用类的常量池中了）

### 类加载器

- 引导类加载器（java的核心加载器） 

  - 名称： rt.jar 根加载器
  - 位置：直接存在于jre文件夹下面
  - 特点： 无法获取  通过C++编写的
  - 作用： 用于装载核心类库
  - 我们用的所有的基础类都在下面， 
    - lang包
    - util包
    - swing包
    - ...

- 扩展加载器

  - 名称： ext

  - 位置:    jre 下面的ext文件夹下面

  - 特点： 目前未知（是我不知道，不是没有作用）

  - 作用：  负责jre/lib/ext目录下的jar包或者-D  java.ext.dirs 指定目录显得jar包装入工作库

  - 获取：

    - ```java
      ClassLoader.getSystemClassLoader().getParent();
      ```

- 系统加载器(用户类加载器)

  - 名称： systemClassLoader (用户的类加载器)

  - 位置： 当前工程下面

  - 特点： 加载该工程的class文件

  - 作用： 负责java -classpath 或 -D java.class.path所指的目录下的类与jar包装入工作，是最常用的加载器；

  - 获取：

    - ```java
      ClassLoader.getSystemClassLoader();
      ```

      

### 获取类名

```java
Class a = Class.forName("com.ziop.relfect.User");
User user=new User;
a = user.getclass();
//获得类的名字
System.out.printin(a.getname());//获得包名+类名
System.out.println(a.getsimplename());//获得类名
```

### 获取属性名

```java
a.getFields();  // 只能获取public 的属性
a.getDeclaredField("name");    // 获取指定的属性
a.getDeclaredFields();   //获取全部的属性  包括private
```

### 获取方法

```java
a.getMethods();  //获得本类及其父类的所有方法   不包括私有
a.getDeclaredMethods();  //获得本类的所有方法  包括私有的
a.getMethods("getTest",); //第二个参数及其以后的参数，用以判断重载的方法
a.setDeclaredMethods("setTest",String.class); 
```

### 获取构造器

```java
a.getConstructors();
a.getDeclaredConstructors(); // 同上
a.getDeclaredConstructors(String.class,int.class); // 获取指定有参构造
```

### 动态创建对象

```java
//创建无参构造器的对象
Class a = Class.forName("com.ziop.relfect.User");
User user  = (User)a.newInstance();  
// 创建有参的对象
Constructor constructor  =  a.getDeclaredConstructors(String.class,int.class); // 获取指定有参构造
User user2 = (User)constructor.newInstance("ziop",2021,20);
//通过反射调用普通方法
User user3  = (User)a.newInstance();  
	//获取一个普通方法
Method setName = a.setDeclaredMethods("setTest",String.class);
setName.invoke(user3,"ziop");   //invoke  : 激活函数
//通过反射操作属性
User user4  = (User)a.newInstance();  
Field name = a.getFeclaredField("name");
	//如果属性是私有的，则直接设置会出错，提示访问不了，同过关闭程序的安全检测则可以更改
name.setAccessible(true);  // 设置安全检测关闭
name.set(user4,"ziop")
```

![image-20210813205644158](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813205644158.png)

### 关闭安全检测可以提高执行效率（但是不推荐使用）

```java
name.setAccessible(true);  // 设置安全检测关闭
```

![image-20210813215437312](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813215437312.png)

### 获取泛型类型

```java
method.getGenericParamaterTypes();    获取参数类型
```

![image-20210813214352107](https://gitee.com/Ziop/typora-img/raw/master/img/image-20210813214352107.png)

如果想要获取泛型里面的类型，则需要判断他是否属于一个参数化类型，如果是的话则提取出来 

![image-20210813214544697](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813214544697.png)

![image-20210813215009848](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210813215009848.png)

```java
method.getgenericReturnType(); //获取返回值的泛型
```

![image-20210813215236259](https://gitee.com/Ziop/typora-img/raw/master/img/image-20210813215236259.png)

### 反射操作注解

​    

```java
Class a = Class.forName("com.ziop.relfect.User");
a.getAnnotations();   //获取所有的注解
Ziop ziop =  (Ziop)a.getAnnotations(ziop.class)  // 获取指定的注解
String value = ziop.value();   // 获取指定的注解的值  value是 ziop注解中的一个字段

```

