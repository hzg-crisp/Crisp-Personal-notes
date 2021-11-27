# Maven上安装与配置：

### 一.在此之前我们先初步聊聊maven到底是什么？

> 官方解释：

​		Maven是基于项目对象模型(POM project object model)，可以通过一小段描述信息（配置）来管理项目的构建，报告和文档的软件项目管理工具。



> 我结合网上文档的理解：

​		就是通过pom.xml文件的配置获取jar包，而不用手动去添加jar包，而这里pom.xml文件对于学了一点maven的人来说，就有些熟悉了，怎么通过pom.xml的配置就可以获取到jar包呢？pom.xml配置文件从何而来？等等类似问题我们需要搞清楚，如果需要使用pom.xml来获取jar包，那么首先该项目就必须为maven项目，maven项目可以这样去想，就是在java项目和web项目的上面包裹了一层maven，本质上java项目还是java项目，web项目还是web项目，但是包裹了maven之后，就可以使用maven提供的一些功能了(通过pom.xml添加jar包)。

　　　所以，根据上一段的描述，我们最终的目的就是学会如何在pom.xml中配置获取到我们想要的jar包，在此之前我们就必须了解如何创建maven项目，maven项目的结构是怎样，与普通java,web项目的区别在哪里，还有如何配置pom.xml获取到对应的jar包等等，这里提前了解一下我们如何通过pom.xml文件获取到想要的jar的，具体后面会详细讲解该配置文件。

　　　Maven 把一个项目的结构和内容抽象成一个模型，在 xml 文件中 进行声明，以方便进行构建和描述pom.xml 是 Maven 的灵魂。所以，maven 环境搭建好之后，所有的学习和 操作都是关于 pom.xml 的。



经过上面的介绍，相信大家对maven有了一定的了解。本文章的重点在于Maven的安装与配置

### 二.maven的安装

1. 确保自己安装了Java环境：maven本身就是Java写的的，所以前提条件就是安装JDK。

2. 下载并解压maven的安装程序：http://maven.apache.org/download.cgi  我安装在了  **D:\BackSoft\maven\apache-maven-3.6.3**（后面用的到）

3. 配置maven的环境变量 ：

   - 在用户变量下面或则系统变量新建变量：变量名：M2_HOME   变量值：D:\BackSoft\maven\apache-maven-3.6.3（对应我上面安装的位置）或则：变量名：MAVEN_HOME   变量值：D:\BackSoft\maven\apache-maven-3.6.3（对应我上面安装的位置）。如果不放心，两个都写上。我写在了用户变量上：如下图。

   ![image-20211127100906461](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127100906461.png)

   - 将上面写的变量写入用户名变量下或则系统变量下的Path中（都有一个叫Path的变量名，特别注意，变量名和将变量名导入Path中，要么全部写在用户变量下，要么全部写在系统变量下）：%M2_HOME%\bin 或则 %MAVEN_HOME%\bin  如果你上面不放心写了两个，那这里两个你也要写上。

   ![image-20211127101714052](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127101714052.png)

   - 验证：验证是否安装成功：打开黑窗口 输入：mvn -v  出现如下内容及安装成功。

     ```java 
     C:\Users\Administrator>mvn -v
      出现如下内容，maven安装，配置正确。
     Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-11T00:41:4
     Maven home: D:\work\maven_work\apache-maven-3.3.9
     Java version: 1.8.0_40, vendor: Oracle Corporation
     Java home: C:\java\JDK8-64\jre
     Default locale: zh_CN, platform encoding: GBK
     OS name: "windows 7", version: "6.1", arch: "amd64", family: "dos"
     ```

### 三.仓库

1. 仓库：
   - 仓库是什么： 
     - 仓库是存放东西的， 存放maven使用的jar 和 我们项目使用的jar
            > maven使用的插件（各种jar）
       	  > 我项目使用的jar(第三方的工具)
   - 仓库的分类
     - 本地仓库， 就是你的个人计算机上的文件夹，存放各种jar
     - 远程仓库， 在互联网上的，使用网络才能使用的仓库
       - 中央仓库，最权威的， 所有的开发人员都共享使用的一个集中的仓库， https://repo.maven.apache.org ：中央仓库的地址
       - 中央仓库的镜像：就是中央仓库的备份， 在各大洲，重要的城市都是镜像。
       - 私服，在公司内部，在局域网中使用的， 不是对外使用的。
     - 仓库的使用:
       - maven仓库的使用不需要人为参与。,开发人员需要使用mysql驱动--->maven首先查本地仓库--->私服--->镜像--->中央仓库

2. 下载的东西存放在哪里？

- ```java 
  3）下载的东西存放到哪里了。
      默认仓库（本机仓库）：
     C:\Users\（登录操作系统的用户名）Administrator\.m2\repository
  ```

- 中央仓库的地址: https://repo.maven.apache.org 

- 更改本机存放资源的目录位置（设置本地仓库）默认在C盘，阔以更改在其他盘。

  - 将C盘中的C:\Users\16337\.m2\repository  的 repository  文件拷贝到安装Maven的目录下，我拷贝到：D:\BackSoft\maven\repository。

  - 修改maven的配置文件， maven安装目录/conf/settings.xml

    - 我的在 **D:\BackSoft\maven\apache-maven-3.6.3**，即打开：D:\BackSoft\maven\apache-maven-3.6.3\conf\settings.xml，这一步主要是在后续的学习中会下载很多的jar包，如果本地  **repository** 文件中有就可以直接引用， 而本机默认是C盘中的**repository**  ，所以需要修改。打开：D:\BackSoft\maven\apache-maven-3.6.3\conf\settings.xml后如下图修改：

    ![image-20211127104354027](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127104354027.png)

### 四：Maven在IDEA中的应用：

1. idea中集成Maven

   - File---->Settings：设置 maven 安装主目录、maven 的 settings.xml 文件和本地仓库所在位置。

   ![image-20211127105541696](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127105541696.png)

   - 设置所使用的maven：

   ![image-20211127110201171](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127110201171.png)

​					这个窗口基本上不用修改什么，但是这样会比较慢，有时候如果网速不好，就会卡的比较久，这是因为 			maven 这个骨架会从远程仓库加载 archetype 元数据，但是 archetype 又比较多，所以比较卡，这时候可以			加 个属性archetypeCatelog = internal，表示仅使用内部元数据；、

- 设置新建项目后maven：

![image-20211127110853407](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127110853407.png)

![image-20211127105541696](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127105541696.png)

![image-20211127110201171](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20211127110201171.png)



五，结束语：

​		以上就是Maven的安装与配置，可能本文中有许多的搞怪语言，或则啰嗦之处。但只要按照步骤一步一步来，还是可以很好地安装并配置好maven的，maven还有许多地方需要大家去学习，这里只是简单地将maven的安装与配置进行分享，不妥之后可以私信我进行修改，



​	