# Java EE 5 Java Persistence API 
JPA(Java Peristence API)是一个java应用程序接口规范，为Java开发人员提供了一个对象/关系映射工具，用于管理Java应用程序中的关系数据。
- Java持久化由以下三个方面组成
  - Java持久化API
  - 查询语言
  - 对象或关系映射元数据
- Entity  
轻量级持久性域对象，通常表示关系数据库中的表，并且每个实体实例对应于表中的行。实体的持久性状态由持久字段或持久属性表示。这些字段或属性使用对象/关系映射注解将实体和实体关系映射到基础数据存储中的关系数据。
  - Entity类的需求
    - 引入`javax.persistence.Entiy`注解
    - 必需有一个公共的或受保护的无参构造器
    - 类不能声明为final, 没有方法或持久实例变量必须声明为final
    - 如果实体实例通过值作为分离对象传递，例如通过会话bean的远程业务接口，则该类必须实现Serializable接口。
    - 实体可以扩展实体类和非实体类，非实体类可以扩展实体类
    - 持久实例变量必须声明为私有、受保护或包私有，并且只能由实体类的方法直接访问。客户端必须通过访问器或业务方法访问实体的状态。
  - 持久化类中的字段和属性  
    实体可以使用持久字段或持久属性。如果映射注解应用于实体的实例变量，则实体使用持久字段。如果映射注解应用于实体的JavaBeans样式属性的getter方法，则实体使用持久属性。在单个实体中无法同时将注解映射到的字段和属性中。  
    字段或属性必需是以下几种：
      - java原始类型
      - java包装器类型
      - java.math.BigInteger, java.math.BigDecimal, java.util.Date, java.util.Calendar, java.sql.Date, java.sql.Time, java.sql.TimeStamp
      - 自定义可序列化类型
      - byte[], Byte[], char[], Character[]
      - 枚举类型
      - 其它实体或其它实体集合
      - 可嵌入的类
  - 实体中的主键  
    每个实体都有唯一的对象标识符，使客户端可以定位实例。实体可以使用简单的主键和复合主键。  
    - 简单主键：`javax.persistence.Id`
    - 复合主键：`javax.persistence.EmbeddedId`和`javax.persistence.IdClass`
    - 不要用浮点类型做主键
  - 实体关系的多重性
    - 一对一
    - 一对多
    - 多对一
    - 多对多
  - 实体关系的方向
    - 双向
    - 单向
    - 根据查询导航方向
    - 级联删除关系：使用关系的实体通常依赖于关系中其他实体的存在。例如，订单项是订单的一部分，如果订单已删除，则还应删除订单项。这称为级联删除关系。
  - 实体的继承  
    实体支持类继承、多态关联和多态查询。它们可以扩展非实体类，而非实体类可以扩展实体类。实体类可以是抽象的，也可以是具体的。  
  - 实体管理(TBC)