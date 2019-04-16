# Week0
# Algorithm
第一次做leetcode算法题，先做个简单的[Two Sum](https://leetcode.com/problems/two-sum/)。
## 题目：
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.
## Example:
```text
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## 思路
1. 这道题的解题思路是：假定当前元素下标为i，查找数组中值为target-nums[i]元素的下标
2. 先想到的是写两个嵌套的循环来查找，一个用来遍历数组作为关键字，另一个用来查找数组中剩下的元素是否有匹配，若有则直接返回结果，没有则继续查找，两次循环结束如果没有提前返回结果，则返回null。
```java
public int[] twoSum(int[] nums, int target){
    for (int i = 0; i < nums.length; i++) {
        for (int j = i+1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target){
                return new int[]{i, j};
            }
        }
    }
    return null;
}
```
3. 想到这种方式嵌套循环的写法有点low，时间复杂度为O(n<sup>2</sup>)，所以想到了这道题的关键在于查找，利用HashMap查询效率高的优势把元素按照<value, position>的方式放在map中，只要在map中找到value为target-num[i]的元素则返回position与当前元素的下标即可。最坏时间复杂度为O(n) * O(logn) = O(nlogn)，均摊情况下时间复杂度为O(n)。
```java
public int[] twoSum(int[] nums, int target){
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        if(map.containsKey(target-nums[i])){
            return new int[]{map.get(target-nums[i]), i};
        }
        map.put(nums[i], i);
    }
    return null;
}
```
# Review
> 前段时间在看core java是读到关于Lambda的时候感觉讲的不是很清楚，所以在网上查了很多资料研究了下Lambda的用法，其中有篇文章在讲到为什么java需要Lambda时提到了一篇Steve Yegge的博客文章：[Execution in the Kingdom of Nouns](http://steve-yegge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html) 文章以风趣幽默的形式描绘了以名词为中心的java世界，最后解释了java为什么要引进Lambda。
* 文章首先从一个倒垃圾的案例讲到了生活中充满了名词、动词、形容词、介词等等。从而引出了不再用动词的王国javaland。
* java中动词等级非常低下，做了负责所以工作，但又被其它词类轻视，因为在java中动词属于名词不能单独出现，必须有一个名词陪同。
* 提到了程序式语言王国名词与动词可以混合搭配使用，这样做可以让垃圾处理看做是一系列的动作集合，不用创建很多用来包装动词的名词。
* 讲到了函数式编程中动词和名词是平等的，但名词的作用很小。之后又引出了一个叫Lambda的传说国度只有动词。
* 由一个缺少马蹄铁的故事讲述了在java世界的主要魅力在于结构，结构可以让你看的见摸的着，可以让元素得到庇护，结构可以让程序很条理。
* 最后讲到了OOP编程让动词在实际思考中变的不那么重要了，这是一种思维上奇怪的倾斜视角。类比C++在这方面有很强的灵活性，C++作为C的超集允许定义独立的函数。而且大多数语言都支持函数作为参数传递，建议java也添加这一功能像成熟。
* 总结：文章很长，很有画面感，整体来说讲了因为缺乏动词，世界观改变，做多编程想法都有点头重脚轻的balabala....
* ps: 一直没耐心读下去，这周在决定开启ARTS计划后硬着头皮读了下去😭。
# Tip
> 讲一个非常小非常小的技巧：在浏览文件夹时在Centos和ubuntu中都有一个很方便的功能，在任何一个目录下都可以在终端打开方便在命令行做一些操作，但在windows下点右键却没有这个功能，实际上windows下有两种方式可以快速的在命令行打开当前目录
1. 在当前目录的地址栏输`cmd`。
2. 在当前目录的空白处按shift同时点击右键就可以看到隐藏菜单在[此处打开powershell窗口]和[在此处打开Linux shell\](有开linux子系统的情况下)。
# Share
> 分享一下上周看Maven的笔记
## 1. maven安装和配置
### 1. 安装 
1. 检查JDK是否安装
2. 下载[maven](https://maven.apache.org/download.cgi)
3. 配置环境变量 %M2_HOME% 或 %MAVEN_HOME%
4. 检查 `mvn -version`
### 2. maven 目录结构
1. bin: 命令脚本
   + mvn
   + mvnDebug
   + m2.conf: classworlds配置文件
2. boot: plexus-classworlds*.jar类加载器框架
3. conf: 配置文件目录
   + settings.xml 全局maven行为
4. lib: 包含maven运行时需要的java类库
5. ~/.m2
   + repository 本地仓库
   + settings.xml 用户层设置
### 3. 设置http代理
+ 设置proxies
```xml
<settings>
    … 
    <proxies>
        <proxy>
            <id>my-proxy</id>
            <active>true</active>
            <protocol>http</protocol>
            <host>218.14.227.197</host>
            <port>3128</port>
            <!--
            <username>***</username>
            <password>***</password>
            <nonProxyHosts>repository.mycom.com|*.google.com</nonProxyHosts>
            -->
        </proxy>
    </proxies>
    …
</settings>
```
### 4. 简单配置
* 设置MAVEN_OPTS环境变量
    > 由于Java默认最大可用内存往往不能满足Maven运行需要，在生成大型项目站点需要占用大量内存，建议配置`MAVEN_OPTS`的值为`-Xms128m -Xmx512m`以防`java.lang.OutOfMemeoryError`
## 2. maven使用入门
> POM(Project Object Model项目对象模型)
### 1. 项目描述相关
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
        http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.juvenxu.mvnbook</groupId>
    <artifactId>hello-world</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>Maven Hello World Project</name>
</project>
```
> - modelVersion: POM模型版本号
> - groupId: 项目组
> - artifactId: 项目组中唯一ID, 一般为模式名
> - version: 项目版本
> - name: 项目名称
> - description: 项目描述
### 2. mvn项目目录结构
|目录|目的|
|---|---|
|${basedir}|存放pom.xml和所有的子目录|
|${basedir}/src/main/java|项目的java源代码|
|${basedir}/src/main/resources|项目的资源，比如说property文件，springmvc.xml|
|${basedir}/src/test/java|项目的测试类，比如说Junit代码|
|${basedir}/src/test/resources|测试用用的资源|
|${basedir}/src/main/webapp/WEB-INF|web应用文件目录，web项目的信息，比如存放web.xml、本地图片、jsp视图页面|
|${basedir}/target|打包输出目录|
|${basedir}/target/classes|编译输出目录|
|${basedir}/target/test-classes|测试编译输出目录|
|Test.java|Maven只会自动运行符合该命名规则的测试类|
|~/.m2/repository|Maven默认的本地仓库目录位置|

* 可以使用archetype生成项目骨架
  * `mvn archetype:generate`
* 测试代码依赖JUnit需注意添加依赖
```xml
<project>
    ...
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.7</version>
            <scope>test</scope>
            <!-- 表示该依赖只对测试有效 -->
        </dependency>
    </dependencies>
    ...
</project>
```
* 配置maven-compiler-plugin
> 直接配置插件
```xml
<project>
  ...
  <build>
    ...
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.0</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
    ...
  </build>
  ...
</project>
```
> 设置property方式
```xml
<project>
  ...
  <properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
  ...
</project>
```
* 生成可执行jar文件可以使用maven-shade-plugin修改*META-INF/MANIFEST.MF*文件
```xml
<project>
  ...
  <build>
    ...
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>1.2.1</version>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
                <goal>shade</goal>
            </goals>
            <configuration>
              <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                  <mainClass>com.juvenxu.mvnbook.helloworld.HelloWorld
                  </mainClass>
                </transformer>
              </transformers>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
    ...
  </build>
  ...
</project>
```
```xml
<project>
  ...
  <build>
    ...
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>3.2.1</version>
        <configuration>
          <transformers>
            <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
              <manifestEntries>
                <Main-Class>com.formssi.learningmvn.App</Main-Class>
                <X-Compile-Source-JDK>${maven.compile.source}</X-Compile-Source-JDK>
                <X-Compile-Target-JDK>${maven.compile.target}</X-Compile-Target-JDK>
                </manifestEntries>
            </transformer>
          </transformers>
        </configuration>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
    ...
  </build>
  ...
</project>
```
### 3. 常用maven命令
* `mvn clean compile`
  * `clean:clean`: 清理输出目录target
  * `resource:resources`: 加载项目资源
  * `compiler:compile`: 编译项目主代码
* `mvn clean test`
  * `clean:clean`
  * `resources:resources`
  * `compiler:compile`
  * `resources:testResources`
  * `compiler:testCompile`
* `mvn clean package`
  * `jar:jar`
* `mvn clean install`
  * `install:install`: target to ~/.m2/repository
## 3. 坐标和依赖
> 为了能够自动化地解析任何一个Java构件, Maven必须将它们唯一标识, 这就是**依赖管理**的底层基础-**坐标**.
### 1. 坐标
> Maven坐标为各种构件引入了秩序，任何一个构件都必须明确定义自己的坐标，而一组
Maven 坐标是通过一些元素定义的，它们是：groupId、artifactId、version、packaging、classifier。
> 项目构件的文件名是与坐标相对应的，一般的规则为 `artifactId-version[-classifier].packaging`
```xml
<project>
  ...
  <groupId>com.formssi.learningmvn</groupId>
  <artifactId>account-email</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>
  ...
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.0.2</version>
        <configuration>
          <classifier>jdk1.8</classifier>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <!-- account-email-1.0-SNAPSHOT-jdk1.8.jar -->
</project>
```
|元素|描述|ext|
|---|---|---|
|groupId|定义当前模块隶属的实际Maven项目, 表示方式与Java包类似|groupId不应直接对应项目隶属的公司/组织(一个公司/组织下可能会有很多的项目).|
|artifactId|定义实际项目中的一个Maven模块|推荐使用项目名作为artifactId前缀, 如:commons-lang3以commons作为前缀(因为Maven打包默认以artifactId作为前缀)|
|version|定义当前项目所处版本(如1.0-SNAPSHOT、4.2.7.RELEASE、1.2.15、14.0.1-h-3 等)|Maven版本号定义约定: <主版本>.<次版本>.<增量版本>-<里程碑版本>|
|packaging|定义Maven项目打包方式, 通常打包方式与所生成构件扩展名对应|有jar(默认)、war、pom、maven-plugin等.|
|classifier|用来帮助定义构建输出的一些附属构件(如javadoc、sources)|名称可以自定义，包名自由发挥空间。例如可以用于区分不同jdk版本打的包。不能直接定义项目的classifier(因为附属构件不是由项目默认生成, 须有附加插件的帮助)|
### 2. 依赖
> 根元素 project 下的 dependencies 可以包含一个或者多个 dependency 元素，以声明一个或者多个项目依赖。每个依赖可以包含的元素有：
```xml
<project>
  ...
  <dependencies>
    <dependency>
      <groupId>...</groupId>
      <artifactId>...</artifactId>
      <version>...</version>
      <type>...</type>
      <scope>...</scope>
      <optional>...</optional>
      <exclusions>
        <exclusion>
        ...
        </exclusion>
        ...
      </exclusions>
    </dependency>
    ...
  </dependencies>
  ...
</project>
```
|元素|描述|ext|
|---|---|---|
|groupId|依赖基本坐标||
|artifactId|依赖基本坐标||
|version|依赖基本坐标||
|classifier|定位附属包|可选|
|type|依赖的类型|默认jar|
|scope|依赖范围|默认compile 详见[dependency_sope](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Dependency_Scope)
|optional|标记依赖是否可选
|exclusions|用来排除传递性依赖
> Maven 有三种classpath（编译、测试、运行）以实现简单的环境环境隔离，依赖范围就是用来控制依赖这3种classpath的关系，Maven有以下几种依赖范围：

|依赖范围（Scope）|对于编译classpath有效|对于测试classpath有效|对于运行时classpath有效|例子|ext
|---|---|---|---|---|---|
|compile|Y|Y|Y|spring-core|
|test|-|Y|-|JUnit
|provided|Y|Y|-|servlet-api|表示希望JDK或容器在运行时提供依赖
|runtime|-|Y|Y|JDBC驱动实现
|system|Y|Y|-|本地的，Maven仓库之外的类库文件|必须通过systemPath元素显式指定依赖**慎用**

### 3. 传递依赖
> Maven依赖传递机制会自动加载我们引入的**依赖包的依赖**, 而不必去手动指定。假设A 依赖于B，B 依赖于C，我们说A 对于B 是第一直接依赖，B 对于C 是第二直接依赖，A 对于C 是传递性依赖。第一直接依赖的范围和第二直接依赖的范围决定了传递性依赖的范围，如下表所示，最左边一行表示第一直接依赖范围，最上面一行表示第二直接依赖范围，中间的交叉单元格则表示传递性依赖范围: 

||compile|test|provided|runtime|
|---|---|---|---|---|
compile|compile|-|-|runtime|
|test|test|-|-|test|
|provided|provided|-|provided|provided|
|runtime|runtime|-|-|runtime|
- test第为第二依赖时，依赖不会传递
- provided作为第二依赖时，只有同为provided才会传递为provided
- compile作为第二依赖时，传递第一依赖范围
- runtime作为第二依赖时，除第一依赖为compile时传递范围会提升到runtime，其它都传递第一依赖
### 4. 依赖调解
1. 第一原则：路径最近者优先
2. 第二原则：第一声明者优先
3. 合理使用可选依赖不被传递性
4. 擅用排除依赖改显示声明方式排除项目隐患(SNAPSHOT不稳定因素)
5. 使用properties添加变量让配置更简洁
6. 解析依赖命令：
   1. `mvn dependency:list`
   2. `mvn dependency:tree`
   3. `mvn dependency:analyze`
## 4. 使用Maven构建Web应用
> Web项目标准打包方式为WAR（Web Application Archives），下面为典型war文件目录结构：
```text
- war/
  + META-INF/
  + WEB-INF/
  | + classes/
  | | + ServletA.class
  | | + config.properties
  | | + ...
  | |
  | + lib/
  | | + dom4j-1.4.1.jar
  | | + mail-1.4.1.jar
  | | + ...
  | |
  | + web.xml
  |
  + img/
  |
  + css/
  |
  + js/
  |
  + index.html
  + sample.jsp
```
> Web项目Maven目录结构
```text
+ project
  |
  + pom.xml
  |
  + src/
    + main/
    | + java/
    | | + ServletA.java
    | | + ...
    | |
    | + resources/
    | | + config.properties
    | | + ...
    | |
    | + webapp/
    | + WEB-INF/
    | | + web.xml
    | |
    | + img/
    | |
    | + css/
    | |
    | + js/
    | +
    | + index.html
    | + sample.jsp
    |
    + test/
      + java/
      + resources/
```
> 下述几个模式待后续仔细研究
---
## 4. Maven仓库
> Maven 中, 任何一个依赖、插件或项目构建的输出, 都可称为构件, 而Maven仓库就是集中存储这些构件的地方.
## 5. 生命周期与插件
> Maven 将所有项目的构建过程统一抽象成一套生命周期: 项目的清理、初始化、编译、测试、打包、集成测试、验证、部署和站点生成 … 几乎所有项目的构建,都能映射到这一组生命周期上. 但生命周期是抽象的(Maven的生命周期本身是不做任何实际工作), 任务执行(如编译源代码)均交由插件完成. 其中每个构建步骤都可以绑定一个或多个插件的目标,而且Maven为大多数构建步骤都编写并绑定了默认插件.当用户有特殊需要的时候, 也可以配置插件定制构建行为, 甚至自己编写插件. 
## 6. 聚合与继承
> Maven的聚合特性(aggregation)能够使项目的多个模块聚合在一起构建, 而继承特性(inheritance)能够帮助抽取各模块相同的依赖、插件等配置,在简化模块配置的同时, 保持各模块一致.

---
> 超详细pom配置
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0http://maven.apache.org/maven-v4_0_0.xsd">   
    <!--父项目的坐标。如果项目中没有规定某个元素的值，那么父项目中的对应值即为项目的默认值。 坐标包括group ID，artifact ID和 version。-->  
    <parent>  
     <!--被继承的父项目的构件标识符-->  
     <artifactId/>  
     <!--被继承的父项目的全球唯一标识符-->  
     <groupId/>  
     <!--被继承的父项目的版本-->  
     <version/>  
     <!-- 父项目的pom.xml文件的相对路径。相对路径允许你选择一个不同的路径。默认值是../pom.xml。Maven首先在构建当前项目的地方寻找父项 目的pom，其次在文件系统的这个位置（relativePath位置），然后在本地仓库，最后在远程仓库寻找父项目的pom。-->  
     <relativePath/>  
 </parent>  
 <!--声明项目描述符遵循哪一个POM模型版本。模型本身的版本很少改变，虽然如此，但它仍然是必不可少的，这是为了当Maven引入了新的特性或者其他模型变更的时候，确保稳定性。-->     
    <modelVersion>4.0.0</modelVersion>   
    <!--项目的全球唯一标识符，通常使用全限定的包名区分该项目和其他项目。并且构建时生成的路径也是由此生成， 如com.mycompany.app生成的相对路径为：/com/mycompany/app-->   
    <groupId>asia.banseon</groupId>   
    <!-- 构件的标识符，它和group ID一起唯一标识一个构件。换句话说，你不能有两个不同的项目拥有同样的artifact ID和groupID；在某个 特定的group ID下，artifact ID也必须是唯一的。构件是项目产生的或使用的一个东西，Maven为项目产生的构件包括：JARs，源 码，二进制发布和WARs等。-->   
    <artifactId>banseon-maven2</artifactId>   
    <!--项目产生的构件类型，例如jar、war、ear、pom。插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型-->   
    <packaging>jar</packaging>   
    <!--项目当前版本，格式为:主版本.次版本.增量版本-限定版本号-->   
    <version>1.0-SNAPSHOT</version>   
    <!--项目的名称, Maven产生的文档用-->   
    <name>banseon-maven</name>   
    <!--项目主页的URL, Maven产生的文档用-->   
    <url>http://www.baidu.com/banseon</url>   
    <!-- 项目的详细描述, Maven 产生的文档用。  当这个元素能够用HTML格式描述时（例如，CDATA中的文本会被解析器忽略，就可以包含HTML标 签）， 不鼓励使用纯文本描述。如果你需要修改产生的web站点的索引页面，你应该修改你自己的索引页文件，而不是调整这里的文档。-->   
    <description>A maven project to study maven.</description>   
    <!--描述了这个项目构建环境中的前提条件。-->  
 <prerequisites>  
  <!--构建该项目或使用该插件所需要的Maven的最低版本-->  
    <maven/>  
 </prerequisites>  
 <!--项目的问题管理系统(Bugzilla, Jira, Scarab,或任何你喜欢的问题管理系统)的名称和URL，本例为 jira-->   
    <issueManagement>  
     <!--问题管理系统（例如jira）的名字，-->   
        <system>jira</system>   
        <!--该项目使用的问题管理系统的URL-->  
        <url>http://jira.baidu.com/banseon</url>   
    </issueManagement>   
    <!--项目持续集成信息-->  
 <ciManagement>  
  <!--持续集成系统的名字，例如continuum-->  
  <system/>  
  <!--该项目使用的持续集成系统的URL（如果持续集成系统有web接口的话）。-->  
  <url/>  
  <!--构建完成时，需要通知的开发者/用户的配置项。包括被通知者信息和通知条件（错误，失败，成功，警告）-->  
  <notifiers>  
   <!--配置一种方式，当构建中断时，以该方式通知用户/开发者-->  
   <notifier>  
    <!--传送通知的途径-->  
    <type/>  
    <!--发生错误时是否通知-->  
    <sendOnError/>  
    <!--构建失败时是否通知-->  
    <sendOnFailure/>  
    <!--构建成功时是否通知-->  
    <sendOnSuccess/>  
    <!--发生警告时是否通知-->  
    <sendOnWarning/>  
    <!--不赞成使用。通知发送到哪里-->  
    <address/>  
    <!--扩展配置项-->  
    <configuration/>  
   </notifier>  
  </notifiers>  
 </ciManagement>  
 <!--项目创建年份，4位数字。当产生版权信息时需要使用这个值。-->  
    <inceptionYear/>  
    <!--项目相关邮件列表信息-->   
    <mailingLists>  
     <!--该元素描述了项目相关的所有邮件列表。自动产生的网站引用这些信息。-->   
        <mailingList>   
         <!--邮件的名称-->  
            <name>Demo</name>   
            <!--发送邮件的地址或链接，如果是邮件地址，创建文档时，mailto: 链接会被自动创建-->   
            <post>banseon@126.com</post>   
            <!--订阅邮件的地址或链接，如果是邮件地址，创建文档时，mailto: 链接会被自动创建-->   
            <subscribe>banseon@126.com</subscribe>   
            <!--取消订阅邮件的地址或链接，如果是邮件地址，创建文档时，mailto: 链接会被自动创建-->   
            <unsubscribe>banseon@126.com</unsubscribe>   
            <!--你可以浏览邮件信息的URL-->  
            <archive>http:/hi.baidu.com/banseon/demo/dev/</archive>   
        </mailingList>   
    </mailingLists>   
    <!--项目开发者列表-->   
    <developers>   
     <!--某个项目开发者的信息-->  
        <developer>   
         <!--SCM里项目开发者的唯一标识符-->  
            <id>HELLO WORLD</id>   
            <!--项目开发者的全名-->  
            <name>banseon</name>   
            <!--项目开发者的email-->  
            <email>banseon@126.com</email>   
            <!--项目开发者的主页的URL-->  
            <url/>  
            <!--项目开发者在项目中扮演的角色，角色元素描述了各种角色-->  
            <roles>   
                <role>Project Manager</role>   
                <role>Architect</role>   
            </roles>  
            <!--项目开发者所属组织-->  
            <organization>demo</organization>   
            <!--项目开发者所属组织的URL-->  
            <organizationUrl>http://hi.baidu.com/banseon</organizationUrl>   
            <!--项目开发者属性，如即时消息如何处理等-->  
            <properties>   
                <dept>No</dept>   
            </properties>  
            <!--项目开发者所在时区， -11到12范围内的整数。-->  
            <timezone>-5</timezone>   
        </developer>   
    </developers>   
    <!--项目的其他贡献者列表-->   
    <contributors>  
     <!--项目的其他贡献者。参见developers/developer元素-->  
     <contributor>  
   <name/><email/><url/><organization/><organizationUrl/><roles/><timezone/><properties/>  
     </contributor>       
    </contributors>     
    <!--该元素描述了项目所有License列表。 应该只列出该项目的license列表，不要列出依赖项目的 license列表。如果列出多个license，用户可以选择它们中的一个而不是接受所有license。-->   
    <licenses>  
     <!--描述了项目的license，用于生成项目的web站点的license页面，其他一些报表和validation也会用到该元素。-->   
        <license>  
         <!--license用于法律上的名称-->  
            <name>Apache 2</name>   
            <!--官方的license正文页面的URL-->  
            <url>http://www.baidu.com/banseon/LICENSE-2.0.txt</url>   
            <!--项目分发的主要方式：  
              repo，可以从Maven库下载  
              manual， 用户必须手动下载和安装依赖-->  
            <distribution>repo</distribution>   
            <!--关于license的补充信息-->  
            <comments>A business-friendly OSS license</comments>   
        </license>   
    </licenses>   
    <!--SCM(Source Control Management)标签允许你配置你的代码库，供Maven web站点和其它插件使用。-->   
    <scm>   
        <!--SCM的URL,该URL描述了版本库和如何连接到版本库。欲知详情，请看SCMs提供的URL格式和列表。该连接只读。-->   
        <connection>   
            scm:svn:http://svn.baidu.com/banseon/maven/banseon/banseon-maven2-trunk(dao-trunk)    
        </connection>   
        <!--给开发者使用的，类似connection元素。即该连接不仅仅只读-->  
        <developerConnection>   
            scm:svn:http://svn.baidu.com/banseon/maven/banseon/dao-trunk    
        </developerConnection>  
        <!--当前代码的标签，在开发阶段默认为HEAD-->  
        <tag/>         
        <!--指向项目的可浏览SCM库（例如ViewVC或者Fisheye）的URL。-->   
        <url>http://svn.baidu.com/banseon</url>   
    </scm>   
    <!--描述项目所属组织的各种属性。Maven产生的文档用-->   
    <organization>   
     <!--组织的全名-->  
        <name>demo</name>   
        <!--组织主页的URL-->  
        <url>http://www.baidu.com/banseon</url>   
    </organization>  
    <!--构建项目需要的信息-->  
    <build>  
     <!--该元素设置了项目源码目录，当构建项目的时候，构建系统会编译目录里的源码。该路径是相对于pom.xml的相对路径。-->  
  <sourceDirectory/>  
  <!--该元素设置了项目脚本源码目录，该目录和源码目录不同：绝大多数情况下，该目录下的内容 会被拷贝到输出目录(因为脚本是被解释的，而不是被编译的)。-->  
  <scriptSourceDirectory/>  
  <!--该元素设置了项目单元测试使用的源码目录，当测试项目的时候，构建系统会编译目录里的源码。该路径是相对于pom.xml的相对路径。-->  
  <testSourceDirectory/>  
  <!--被编译过的应用程序class文件存放的目录。-->  
  <outputDirectory/>  
  <!--被编译过的测试class文件存放的目录。-->  
  <testOutputDirectory/>  
  <!--使用来自该项目的一系列构建扩展-->  
  <extensions>  
   <!--描述使用到的构建扩展。-->  
   <extension>  
    <!--构建扩展的groupId-->  
    <groupId/>  
    <!--构建扩展的artifactId-->  
    <artifactId/>  
    <!--构建扩展的版本-->  
    <version/>  
   </extension>  
  </extensions>  
  <!--当项目没有规定目标（Maven2 叫做阶段）时的默认值-->  
  <defaultGoal/>  
  <!--这个元素描述了项目相关的所有资源路径列表，例如和项目相关的属性文件，这些资源被包含在最终的打包文件里。-->  
  <resources>  
   <!--这个元素描述了项目相关或测试相关的所有资源路径-->  
   <resource>  
    <!-- 描述了资源的目标路径。该路径相对target/classes目录（例如${project.build.outputDirectory}）。举个例 子，如果你想资源在特定的包里(org.apache.maven.messages)，你就必须该元素设置为org/apache/maven /messages。然而，如果你只是想把资源放到源码目录结构里，就不需要该配置。-->  
    <targetPath/>  
    <!--是否使用参数值代替参数名。参数值取自properties元素或者文件里配置的属性，文件在filters元素里列出。-->  
    <filtering/>  
    <!--描述存放资源的目录，该路径相对POM路径-->  
    <directory/>  
    <!--包含的模式列表，例如**/*.xml.-->  
    <includes/>  
    <!--排除的模式列表，例如**/*.xml-->  
    <excludes/>  
   </resource>  
  </resources>  
  <!--这个元素描述了单元测试相关的所有资源路径，例如和单元测试相关的属性文件。-->  
  <testResources>  
   <!--这个元素描述了测试相关的所有资源路径，参见build/resources/resource元素的说明-->  
   <testResource>  
    <targetPath/><filtering/><directory/><includes/><excludes/>  
   </testResource>  
  </testResources>  
  <!--构建产生的所有文件存放的目录-->  
  <directory/>  
  <!--产生的构件的文件名，默认值是${artifactId}-${version}。-->  
  <finalName/>  
  <!--当filtering开关打开时，使用到的过滤器属性文件列表-->  
  <filters/>  
  <!--子项目可以引用的默认插件信息。该插件配置项直到被引用时才会被解析或绑定到生命周期。给定插件的任何本地配置都会覆盖这里的配置-->  
  <pluginManagement>  
   <!--使用的插件列表 。-->  
   <plugins>  
    <!--plugin元素包含描述插件所需要的信息。-->  
    <plugin>  
     <!--插件在仓库里的group ID-->  
     <groupId/>  
     <!--插件在仓库里的artifact ID-->  
     <artifactId/>  
     <!--被使用的插件的版本（或版本范围）-->  
     <version/>  
     <!--是否从该插件下载Maven扩展（例如打包和类型处理器），由于性能原因，只有在真需要下载时，该元素才被设置成enabled。-->  
     <extensions/>  
     <!--在构建生命周期中执行一组目标的配置。每个目标可能有不同的配置。-->  
     <executions>  
      <!--execution元素包含了插件执行需要的信息-->  
      <execution>  
       <!--执行目标的标识符，用于标识构建过程中的目标，或者匹配继承过程中需要合并的执行目标-->  
       <id/>  
       <!--绑定了目标的构建生命周期阶段，如果省略，目标会被绑定到源数据里配置的默认阶段-->  
       <phase/>  
       <!--配置的执行目标-->  
       <goals/>  
       <!--配置是否被传播到子POM-->  
       <inherited/>  
       <!--作为DOM对象的配置-->  
       <configuration/>  
      </execution>  
     </executions>  
     <!--项目引入插件所需要的额外依赖-->  
     <dependencies>  
      <!--参见dependencies/dependency元素-->  
      <dependency>  
       ......  
      </dependency>  
     </dependencies>       
     <!--任何配置是否被传播到子项目-->  
     <inherited/>  
     <!--作为DOM对象的配置-->  
     <configuration/>  
    </plugin>  
   </plugins>  
  </pluginManagement>  
  <!--使用的插件列表-->  
  <plugins>  
   <!--参见build/pluginManagement/plugins/plugin元素-->  
   <plugin>  
    <groupId/><artifactId/><version/><extensions/>  
    <executions>  
     <execution>  
      <id/><phase/><goals/><inherited/><configuration/>  
     </execution>  
    </executions>  
    <dependencies>  
     <!--参见dependencies/dependency元素-->  
     <dependency>  
      ......  
     </dependency>  
    </dependencies>  
    <goals/><inherited/><configuration/>  
   </plugin>  
  </plugins>  
 </build>  
 <!--在列的项目构建profile，如果被激活，会修改构建处理-->  
 <profiles>  
  <!--根据环境参数或命令行参数激活某个构建处理-->  
  <profile>  
   <!--构建配置的唯一标识符。即用于命令行激活，也用于在继承时合并具有相同标识符的profile。-->  
   <id/>  
   <!--自动触发profile的条件逻辑。Activation是profile的开启钥匙。profile的力量来自于它  
   能够在某些特定的环境中自动使用某些特定的值；这些环境通过activation元素指定。activation元素并不是激活profile的唯一方式。-->  
   <activation>  
    <!--profile默认是否激活的标志-->  
    <activeByDefault/>  
    <!--当匹配的jdk被检测到，profile被激活。例如，1.4激活JDK1.4，1.4.0_2，而!1.4激活所有版本不是以1.4开头的JDK。-->  
    <jdk/>  
    <!--当匹配的操作系统属性被检测到，profile被激活。os元素可以定义一些操作系统相关的属性。-->  
    <os>  
     <!--激活profile的操作系统的名字-->  
     <name>Windows XP</name>  
     <!--激活profile的操作系统所属家族(如 'windows')-->  
     <family>Windows</family>  
     <!--激活profile的操作系统体系结构 -->  
     <arch>x86</arch>  
     <!--激活profile的操作系统版本-->  
     <version>5.1.2600</version>  
    </os>  
    <!--如果Maven检测到某一个属性（其值可以在POM中通过${名称}引用），其拥有对应的名称和值，Profile就会被激活。如果值  
    字段是空的，那么存在属性名称字段就会激活profile，否则按区分大小写方式匹配属性值字段-->  
    <property>  
     <!--激活profile的属性的名称-->  
     <name>mavenVersion</name>  
     <!--激活profile的属性的值-->  
     <value>2.0.3</value>  
    </property>  
    <!--提供一个文件名，通过检测该文件的存在或不存在来激活profile。missing检查文件是否存在，如果不存在则激活  
    profile。另一方面，exists则会检查文件是否存在，如果存在则激活profile。-->  
    <file>  
     <!--如果指定的文件存在，则激活profile。-->  
     <exists>/usr/local/hudson/hudson-home/jobs/maven-guide-zh-to-production/workspace/</exists>  
     <!--如果指定的文件不存在，则激活profile。-->  
     <missing>/usr/local/hudson/hudson-home/jobs/maven-guide-zh-to-production/workspace/</missing>  
    </file>  
   </activation>  
   <!--构建项目所需要的信息。参见build元素-->  
   <build>  
    <defaultGoal/>  
    <resources>  
     <resource>  
      <targetPath/><filtering/><directory/><includes/><excludes/>  
     </resource>  
    </resources>  
    <testResources>  
     <testResource>  
      <targetPath/><filtering/><directory/><includes/><excludes/>  
     </testResource>  
    </testResources>  
    <directory/><finalName/><filters/>  
    <pluginManagement>  
     <plugins>  
      <!--参见build/pluginManagement/plugins/plugin元素-->  
      <plugin>  
       <groupId/><artifactId/><version/><extensions/>  
       <executions>  
        <execution>  
         <id/><phase/><goals/><inherited/><configuration/>  
        </execution>  
       </executions>  
       <dependencies>  
        <!--参见dependencies/dependency元素-->  
        <dependency>  
         ......  
        </dependency>  
       </dependencies>  
       <goals/><inherited/><configuration/>  
      </plugin>  
     </plugins>  
    </pluginManagement>  
    <plugins>  
     <!--参见build/pluginManagement/plugins/plugin元素-->  
     <plugin>  
      <groupId/><artifactId/><version/><extensions/>  
      <executions>  
       <execution>  
        <id/><phase/><goals/><inherited/><configuration/>  
       </execution>  
      </executions>  
      <dependencies>  
       <!--参见dependencies/dependency元素-->  
       <dependency>  
        ......  
       </dependency>  
      </dependencies>  
      <goals/><inherited/><configuration/>  
     </plugin>  
    </plugins>  
   </build>  
   <!--模块（有时称作子项目） 被构建成项目的一部分。列出的每个模块元素是指向该模块的目录的相对路径-->  
   <modules/>  
   <!--发现依赖和扩展的远程仓库列表。-->  
   <repositories>  
    <!--参见repositories/repository元素-->  
    <repository>  
     <releases>  
      <enabled/><updatePolicy/><checksumPolicy/>  
     </releases>  
     <snapshots>  
      <enabled/><updatePolicy/><checksumPolicy/>  
     </snapshots>  
     <id/><name/><url/><layout/>  
    </repository>  
   </repositories>  
   <!--发现插件的远程仓库列表，这些插件用于构建和报表-->  
   <pluginRepositories>  
    <!--包含需要连接到远程插件仓库的信息.参见repositories/repository元素-->      
    <pluginRepository>  
     <releases>  
      <enabled/><updatePolicy/><checksumPolicy/>  
     </releases>  
     <snapshots>  
      <enabled/><updatePolicy/><checksumPolicy/>  
     </snapshots>  
     <id/><name/><url/><layout/>  
    </pluginRepository>  
   </pluginRepositories>  
   <!--该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。要获取更多信息，请看项目依赖机制。-->  
   <dependencies>  
    <!--参见dependencies/dependency元素-->  
    <dependency>  
     ......  
    </dependency>  
   </dependencies>  
   <!--不赞成使用. 现在Maven忽略该元素.-->  
   <reports/>     
   <!--该元素包括使用报表插件产生报表的规范。当用户执行“mvn site”，这些报表就会运行。 在页面导航栏能看到所有报表的链接。参见reporting元素-->  
   <reporting>  
    ......  
   </reporting>  
   <!--参见dependencyManagement元素-->  
   <dependencyManagement>  
    <dependencies>  
     <!--参见dependencies/dependency元素-->  
     <dependency>  
      ......  
     </dependency>  
    </dependencies>  
   </dependencyManagement>  
   <!--参见distributionManagement元素-->  
   <distributionManagement>  
    ......  
   </distributionManagement>  
   <!--参见properties元素-->  
   <properties/>  
  </profile>  
 </profiles>  
 <!--模块（有时称作子项目） 被构建成项目的一部分。列出的每个模块元素是指向该模块的目录的相对路径-->  
 <modules/>  
    <!--发现依赖和扩展的远程仓库列表。-->   
    <repositories>   
     <!--包含需要连接到远程仓库的信息-->  
        <repository>  
         <!--如何处理远程仓库里发布版本的下载-->  
         <releases>  
          <!--true或者false表示该仓库是否为下载某种类型构件（发布版，快照版）开启。 -->  
    <enabled/>  
    <!--该元素指定更新发生的频率。Maven会比较本地POM和远程POM的时间戳。这里的选项是：always（一直），daily（默认，每日），interval：X（这里X是以分钟为单位的时间间隔），或者never（从不）。-->  
    <updatePolicy/>  
    <!--当Maven验证构件校验文件失败时该怎么做：ignore（忽略），fail（失败），或者warn（警告）。-->  
    <checksumPolicy/>  
   </releases>  
   <!-- 如何处理远程仓库里快照版本的下载。有了releases和snapshots这两组配置，POM就可以在每个单独的仓库中，为每种类型的构件采取不同的 策略。例如，可能有人会决定只为开发目的开启对快照版本下载的支持。参见repositories/repository/releases元素 -->  
   <snapshots>  
    <enabled/><updatePolicy/><checksumPolicy/>  
   </snapshots>  
   <!--远程仓库唯一标识符。可以用来匹配在settings.xml文件里配置的远程仓库-->  
   <id>banseon-repository-proxy</id>   
   <!--远程仓库名称-->  
            <name>banseon-repository-proxy</name>   
            <!--远程仓库URL，按protocol://hostname/path形式-->  
            <url>http://192.168.1.169:9999/repository/</url>   
            <!-- 用于定位和排序构件的仓库布局类型-可以是default（默认）或者legacy（遗留）。Maven 2为其仓库提供了一个默认的布局；然 而，Maven 1.x有一种不同的布局。我们可以使用该元素指定布局是default（默认）还是legacy（遗留）。-->  
            <layout>default</layout>             
        </repository>   
    </repositories>  
    <!--发现插件的远程仓库列表，这些插件用于构建和报表-->  
    <pluginRepositories>  
     <!--包含需要连接到远程插件仓库的信息.参见repositories/repository元素-->  
  <pluginRepository>  
   ......  
  </pluginRepository>  
 </pluginRepositories>  
     
    <!--该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。要获取更多信息，请看项目依赖机制。-->   
    <dependencies>   
        <dependency>  
   <!--依赖的group ID-->  
            <groupId>org.apache.maven</groupId>   
            <!--依赖的artifact ID-->  
            <artifactId>maven-artifact</artifactId>   
            <!--依赖的版本号。 在Maven 2里, 也可以配置成版本号的范围。-->  
            <version>3.8.1</version>   
            <!-- 依赖类型，默认类型是jar。它通常表示依赖的文件的扩展名，但也有例外。一个类型可以被映射成另外一个扩展名或分类器。类型经常和使用的打包方式对应， 尽管这也有例外。一些类型的例子：jar，war，ejb-client和test-jar。如果设置extensions为 true，就可以在 plugin里定义新的类型。所以前面的类型的例子不完整。-->  
            <type>jar</type>  
            <!-- 依赖的分类器。分类器可以区分属于同一个POM，但不同构建方式的构件。分类器名被附加到文件名的版本号后面。例如，如果你想要构建两个单独的构件成 JAR，一个使用Java 1.4编译器，另一个使用Java 6编译器，你就可以使用分类器来生成两个单独的JAR构件。-->  
            <classifier></classifier>  
            <!--依赖范围。在项目发布过程中，帮助决定哪些构件被包括进来。欲知详情请参考依赖机制。  
                - compile ：默认范围，用于编译    
                - provided：类似于编译，但支持你期待jdk或者容器提供，类似于classpath    
                - runtime: 在执行时需要使用    
                - test:    用于test任务时使用    
                - system: 需要外在提供相应的元素。通过systemPath来取得    
                - systemPath: 仅用于范围为system。提供相应的路径    
                - optional:   当项目自身被依赖时，标注依赖是否传递。用于连续依赖时使用-->   
            <scope>test</scope>     
            <!--仅供system范围使用。注意，不鼓励使用这个元素，并且在新的版本中该元素可能被覆盖掉。该元素为依赖规定了文件系统上的路径。需要绝对路径而不是相对路径。推荐使用属性匹配绝对路径，例如${java.home}。-->  
            <systemPath></systemPath>   
            <!--当计算传递依赖时， 从依赖构件列表里，列出被排除的依赖构件集。即告诉maven你只依赖指定的项目，不依赖项目的依赖。此元素主要用于解决版本冲突问题-->  
            <exclusions>  
             <exclusion>   
                    <artifactId>spring-core</artifactId>   
                    <groupId>org.springframework</groupId>   
                </exclusion>   
            </exclusions>     
            <!--可选依赖，如果你在项目B中把C依赖声明为可选，你就需要在依赖于B的项目（例如项目A）中显式的引用对C的依赖。可选依赖阻断依赖的传递性。-->   
            <optional>true</optional>  
        </dependency>  
    </dependencies>  
    <!--不赞成使用. 现在Maven忽略该元素.-->  
    <reports></reports>  
    <!--该元素描述使用报表插件产生报表的规范。当用户执行“mvn site”，这些报表就会运行。 在页面导航栏能看到所有报表的链接。-->  
 <reporting>  
  <!--true，则，网站不包括默认的报表。这包括“项目信息”菜单中的报表。-->  
  <excludeDefaults/>  
  <!--所有产生的报表存放到哪里。默认值是${project.build.directory}/site。-->  
  <outputDirectory/>  
  <!--使用的报表插件和他们的配置。-->  
  <plugins>  
   <!--plugin元素包含描述报表插件需要的信息-->  
   <plugin>  
    <!--报表插件在仓库里的group ID-->  
    <groupId/>  
    <!--报表插件在仓库里的artifact ID-->  
    <artifactId/>  
    <!--被使用的报表插件的版本（或版本范围）-->  
    <version/>  
    <!--任何配置是否被传播到子项目-->  
    <inherited/>  
    <!--报表插件的配置-->  
    <configuration/>  
    <!--一组报表的多重规范，每个规范可能有不同的配置。一个规范（报表集）对应一个执行目标 。例如，有1，2，3，4，5，6，7，8，9个报表。1，2，5构成A报表集，对应一个执行目标。2，5，8构成B报表集，对应另一个执行目标-->  
    <reportSets>  
     <!--表示报表的一个集合，以及产生该集合的配置-->  
     <reportSet>  
      <!--报表集合的唯一标识符，POM继承时用到-->  
      <id/>  
      <!--产生报表集合时，被使用的报表的配置-->  
      <configuration/>  
      <!--配置是否被继承到子POMs-->  
      <inherited/>  
      <!--这个集合里使用到哪些报表-->  
      <reports/>  
     </reportSet>  
    </reportSets>  
   </plugin>  
  </plugins>  
 </reporting>  
 <!-- 继承自该项目的所有子项目的默认依赖信息。这部分的依赖信息不会被立即解析,而是当子项目声明一个依赖（必须描述group ID和 artifact ID信息），如果group ID和artifact ID以外的一些信息没有描述，则通过group ID和artifact ID 匹配到这里的依赖，并使用这里的依赖信息。-->  
 <dependencyManagement>  
  <dependencies>  
   <!--参见dependencies/dependency元素-->  
   <dependency>  
    ......  
   </dependency>  
  </dependencies>  
 </dependencyManagement>     
    <!--项目分发信息，在执行mvn deploy后表示要发布的位置。有了这些信息就可以把网站部署到远程服务器或者把构件部署到远程仓库。-->   
    <distributionManagement>  
        <!--部署项目产生的构件到远程仓库需要的信息-->  
        <repository>  
         <!--是分配给快照一个唯一的版本号（由时间戳和构建流水号）？还是每次都使用相同的版本号？参见repositories/repository元素-->  
   <uniqueVersion/>  
   <id>banseon-maven2</id>   
   <name>banseon maven2</name>   
            <url>file://${basedir}/target/deploy</url>   
            <layout/>  
  </repository>  
  <!--构件的快照部署到哪里？如果没有配置该元素，默认部署到repository元素配置的仓库，参见distributionManagement/repository元素-->   
  <snapshotRepository>  
   <uniqueVersion/>  
   <id>banseon-maven2</id>  
            <name>Banseon-maven2 Snapshot Repository</name>  
            <url>scp://svn.baidu.com/banseon:/usr/local/maven-snapshot</url>   
   <layout/>  
  </snapshotRepository>  
  <!--部署项目的网站需要的信息-->   
        <site>  
         <!--部署位置的唯一标识符，用来匹配站点和settings.xml文件里的配置-->   
            <id>banseon-site</id>   
            <!--部署位置的名称-->  
            <name>business api website</name>   
            <!--部署位置的URL，按protocol://hostname/path形式-->  
            <url>   
                scp://svn.baidu.com/banseon:/var/www/localhost/banseon-web    
            </url>   
        </site>  
  <!--项目下载页面的URL。如果没有该元素，用户应该参考主页。使用该元素的原因是：帮助定位那些不在仓库里的构件（由于license限制）。-->  
  <downloadUrl/>  
  <!--如果构件有了新的group ID和artifact ID（构件移到了新的位置），这里列出构件的重定位信息。-->  
  <relocation>  
   <!--构件新的group ID-->  
   <groupId/>  
   <!--构件新的artifact ID-->  
   <artifactId/>  
   <!--构件新的版本号-->  
   <version/>  
   <!--显示给用户的，关于移动的额外信息，例如原因。-->  
   <message/>  
  </relocation>  
  <!-- 给出该构件在远程仓库的状态。不得在本地项目中设置该元素，因为这是工具自动更新的。有效的值有：none（默认），converted（仓库管理员从 Maven 1 POM转换过来），partner（直接从伙伴Maven 2仓库同步过来），deployed（从Maven 2实例部 署），verified（被核实时正确的和最终的）。-->  
  <status/>         
    </distributionManagement>  
    <!--以值替代名称，Properties可以在整个POM中使用，也可以作为触发条件（见settings.xml配置文件里activation元素的说明）。格式是<name>value</name>。-->  
    <properties/>  
</project>  
```