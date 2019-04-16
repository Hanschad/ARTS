# Java持久化开发概念简述
## Peristence持久化
持久化是一种描述数据可以比创建它的过程更长久的概念，简单的说就是数据可以存放在比内存更持久的一个地方(这个地方peristence翻译为存留更容易理解)[^2]，Java中有多种实现方式，如：JDBC, 序列化，文件IO，JCA, 对象数据库和XML数据库。大多数数据都保存在数据库中。
## JDBC
JDBC(Java DataBase Connectivity)，提供了一组Java API来访问关系数据库的Java程序。这些Java APIs 可以使 Java 应用程序执行 SQL 语句，能够与任何符合 SQL 规范的数据库进行交互。  
JDBC 提供了一个灵活的框架来编写操作数据库的独立的应用程序，该程序能够运行在不同的平台上且不需修改，能够与不同的 DBMS 进行交互。  
**优点**：
- 干净整洁的 SQL 处理
- 大数据下有良好的性能
- 对于小应用非常好
- 易学的简易语法  

**缺点**：
- 大项目中使用很复杂
- 很大的编程成本
- 没有封装
- 难以实现 MVC 的概念
- 查询需要指定 DBMS
## ORM
ORM(Object-relational mapping)对象关系映射，是一种使用面向对象编程语言在不兼容类型系统之间转换数据的编程技术，实际上创建了可以在编程语言中使用的虚拟对象数据库。  
**相比于JDBC有以下优点**：
- 使用业务代码访问对象而不是数据库中的表
- 从面向对象逻辑中隐藏 SQL 查询的细节
- 基于 JDBC 的 'under the hood'
- 没有必要去处理数据库实现
- 实体是基于业务的概念而不是数据库的结构
- 事务管理和键的自动生成
- 应用程序的快速开发
## JPA
JPA(Java Peristence API)是一个java应用程序接口规范，为Java开发人员提供了一个对象/关系映射工具，用于管理Java应用程序中的关系数据。
## Hibernate
Hibernate是一个开源的对象关系映射框架，对JDBC进行了轻量级的对象封闭，它将POJO与数据库表建立映射关系，是一个全自动的ORM框架，hibernate可以自动生成SQL语句，自动执行。  
Hibernate 是传统 Java 对象和数据库服务器之间的桥梁，用来处理基于 O/R 映射机制和模式的那些对象。[^4]  
![hibernate_position](https://i.imgur.com/ky2O0EX.jpg)  
**Hibernate 优势**：
- Hibernate 使用 XML 文件来处理映射 Java 类别到数据库表格中，并且不用编写任何代码。
- 为在数据库中直接储存和检索 Java 对象提供简单的 APIs。
- 如果在数据库中或任何其它表格中出现变化，那么仅需要改变 XML 文件属性。
- 抽象不熟悉的 SQL 类型，并为我们提供工作中所熟悉的 Java 对象。
- Hibernate 不需要应用程序服务器来操作。
- 操控你数据库中对象复杂的关联。
- 最小化与访问数据库的智能提取策略。
- 提供简单的数据询问。
## Spring-Data-JPA
Spring data JPA是在JPA规范下提供了Repository层的实现，简化了数据访问层的编码，接口中包含了一些个性化的查询方法，Spring-Data-JPA将自动实现查询方法。JPA默认使用Hibernate作为ORM实现。
## MyBatis
MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。  
与hibernate相比：MyBatis是一个能够灵活编写SQL语句，并将SQL的参和查询结果映射成POJOs的一个持久层框架。**对于数据的操作，hibernate是面向对象的，而MyBatis是面向关系的。**[^3]
## POJO
- 普通的java对象，除符合java语法外，不受任何限制，不受任何类路径的约束。用于提高程序可读性和可重用性[^1]。
- 基本上定义了一个实体
- 字段访问修饰符随意
- 可以不定义构造器
- POJO封装了业务逻辑，如下图所示，Controllers与业务逻辑交互，业务逻辑又与POJO交互来访问数据库。在本例中，数据库实体由POJO表示。这个POJO具有与数据库实体相同的成员。  
![pojo](https://i.imgur.com/sQKmilO.jpg)  
## JavaBeans
- POJO的特殊类型
- JavaBeans是POJOs，但POJOs不一定是JavaBeans
- 序列化
- 字段访问修饰符需为private
- 字段必需有getter或setter或两个都有
- 需要一个无参构造器
- 字段只能由constructor、getter或setter访问














































[^1]:https://www.geeksforgeeks.org/pojo-vs-java-beans/
[^2]:https://en.wikibooks.org/wiki/Java_Persistence/What_is_Java_persistence%3F
[^3]:https://www.jianshu.com/p/3927c2b6acc0
[^4]:http://wiki.jikexueyuan.com/project/hibernate/overview.html
