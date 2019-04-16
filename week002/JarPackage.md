# Jar探索

Jar(java Archive)文件允许有多个文件组成一个归档文件。  [^1]
Jar文件有以下用处：  
    - 安全性：可以jar包内文件进行数字签名
    - 减少下载时间
    - 压缩
    - 扩展包装
    - 包密封
    - 包版本说明
    - 可移植性

## 基础

Jar文件文件是用ZIP格式打包的, 可以用JDK提供的工具找包，使用方式类似linux tar 命令  

用法: jar {ctxui}[vfmn0PMe] [jar-file] [manifest-file] [entry-point] [-C dir] files ...  
选项:

    - c  创建新档案
    - t  列出档案目录
    - x  从档案中提取指定的 (或所有) 文件
    - u  更新现有档案
    - v  在标准输出中生成详细输出
    - f  指定档案文件名
    - m  包含指定清单文件中的清单信息
    - n  创建新档案后执行 Pack200 规范化
    - e  为捆绑到可执行 jar 文件的独立应用程序指定应用程序入口点
    - 0  仅存储; 不使用任何 ZIP 压缩
    - P  保留文件名中的前导 '/' (绝对路径) 和 ".." (父目录) 组件
    - M  不创建条目的清单文件
    - i  为指定的 jar 文件生成索引信息
    - C  更改为指定的目录并包含以下文件  
如果任何文件为目录, 则对其进行递归处理。  
清单文件名, 档案文件名和入口点名称的指定顺序与 'm', 'f' 和 'e' 标记的指定顺序相同。  

常用操作

|功能|命令|
|---|---|
| 创建jar包                           | jar cf jar-file input-file(s) |
| 查看jar包                           | jar tf jar-file  |
| 解包jar包                           | jar xf jar-file |
| 导出指定文件                        | jar xf jar-file archived-file(s) |
| 打包并使用自定义Manifest            | jar cfm jar-file manifest-addition input-file(s)  |
| 更新jar包                           | jar uf jar-file input-file(s) |
| 运行jar包程序（需有指定Main-class） | java -jar app.jar |
| applet调用jar文件                   | `<applet code=AppletClassName.class archive="JarFileName.jar" width=width height=height></applet>` |

## Manifest

jar包可以通过*manifest*支持电子签名，版本管控，包封装，动态扩展等等  
*manifest*是一个特殊的文件，它可以包含关于打包在JAR文件中的文件的信息。通过裁剪*manifest*包含的这个“元”信息，您可以将JAR文件用于各种目的，清单每行以"header: value"格式编写。  

### 默认*manifest*

文件路径：META-INF/MANIFEST.MF
文件内容：Manifest-Version: 1.0

### 设置应用入口点

- 方法一：
  - 手动编写Manifest方式添加：</br>`Main-Class: MyPackage.MyClass`</br>`jar cfm MyJar.jar Manifest MyPackage/*.class`
- 方法二：
  - `jar cfe app.jar MyApp MyApp.class`

### 在jar包中添加JAR文件的类路径添加类

通过在清单中使用类路径头，可以避免在调用Java运行应用程序时必须指定长类路径标志。

`Class-Path: jar1-name jar2-name directory-name/jar3-name`

### 设置版本信息

| Header                 | Definition                              |
| ---------------------- | --------------------------------------- |
| Name                   | The name of the specification.          |
| Specification-Title    | The title of the specification.         |
| Specification-Version  | The version of the specification.       |
| Specification-Vendor   | The vendor of the specification.        |
| Implementation-Title   | The title of the implementation.        |
| Implementation-Version | The build number of the implementation. |
| Implementation-Vendor  | The vendor of the implementation.       |

### 将包密封在jar中

JAR文件中的包可以选择性地密封，这意味着该包中定义的所有类必须存档在同一个JAR文件中。 例如，您可能希望密封包，以确保软件中类之间的版本一致性。  

有两种密封方式：

- 对整个jar包密封
  - `Manifest-Version: 1.0` </br> `Sealed: true`
- 对jar中package密封
  - `Name: myCompany/firstPackage/`</br>`Sealed: true`</br></br>`Name: myCompany/secondPackage/`</br>`Sealed: true`

Package一旦密封，那么Java 虚拟机一旦成功装载密封Package中的某个类后，其后所有装载的带有相同Package名的类必须来自同一个Jar文件，否则将触发Sealing Violation安全异常。[^2]  
有两种情况会触发Sealing安全异常：

1. 检查当前试图加载的类对应的Package是否已经被JVM装载且密封。如果已经被装载且密封了，但被密封的Package与当前加载的类对应的Package不是来自同一个Jar文件，将触发安全异常。
2. 检查当前试图加载的类对应的 Package是否已经被JVM装载且密封。如果已经被装载但没有被密封，但当前试图加载的类对应的Package确要试图进行密封操作，将触发安全异常。JVM不允许对已经装载但未密封的Package再进行密封操作。

### 增强安全性的清单属性

部分有助与applet 和 java web applicate 安全性的属性，可以查看oracle[官方文档](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html)

## 签名和验证JAR文件（TBC）

签名和验证文件的能力是 Java 平台安全架构的重要组成部分。安全性由运行时有效的安全策略控制。 您可以配置该策略以将安全权限授予小程序和应用程序。  
JAR 文件可以用 jarsigner 工具或者直接通过 java.security API 签名。一个签名的 JAR 文件与原来的 JAR 文件完全相同，只是更新了它的manifest，并在 META-INF 目录中增加了两个文件，一个签名文件和一个签名块文件。  
JAR 文件是用一个存储在 Keystore 数据库中的证书签名的。存储在 keystore 中的证书有密码保护，必须向 jarsigner 工具提供这个密码才能对JAR 文件签名。[^3]

## Jar 相关API

- java.util.jar
- java.net.JarURLConnection
- java.net.URLClassLoader
- 示例：
  - `java JarRunner http://www.example.com/TargetApp.jar`


[^1]: https://docs.oracle.com/javase/tutorial/deployment/jar/index.html
[^2]: https://blog.csdn.net/technerd/article/details/8945587
[^3]: https://blog.csdn.net/tanga842428/article/details/52425335