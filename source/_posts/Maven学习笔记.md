---
title: Maven学习笔记
date: 2017-12-28 18:00:28
tags:
---

- 构建工具
- 依赖管理工具
- 项目信息管理工具

```
mvn clean compile
```

```
mvn clean test
```

```
mvn clean package
```

```
mvn clean install
```

```
mvn dependency:list
```

```
mvn dependency:tree
```

```
java -jar hello-world-1.0-SNAPSHOT.jar
```

##### Maven坐标的元素
- groupId
- artifactId
- version
- packaging
- classfier

##### 每个依赖可以包含的元素有：
- groupId
- artifactId
- version
- type
- scope
- optional
- exclusion

##### classpath
- 编译classpath
- 测试classpath
- 运行classpath

##### 依赖范围
- compile
- test
- provided
- runtime
- system
- import


依赖范围(Scope) | 对于编译classpath有效 | 对于测试classpath有效 | 对于运行时classpath有效 | 例子
-|-|-|-|-| 
compile | Y | Y | Y | spring-core
test | - | Y | - | JUnit
provided | Y | Y | - | servlet-api
runtime | - | Y | Y | JDBC驱动实现
system | Y | Y | - |本地的，Maven仓库之外的类库文件

##### 传递性依赖

假设A依赖于B，B依赖于C，我们说A对于B是第一直接依赖，B对于C是第二直接依赖，A对于C是传递性依赖。

第一直接依赖的范围和第二直接依赖的范围决定了传递性依赖的范围。

下表中最左边一行标识第一直接依赖范围，最上面一行表示第二直接依赖范围，中间的交叉单元格则表示传递性依赖范围。

-| compile | test | provided | runtime
-|-|-|-|-|
compile|compile|-|-|runtime
test|test|-|-|test
provided|provided|-|provided|provided
runtime|runtime|-|-|runtime


##### 依赖调节(Dependency Mediation)
- 第一原则：路径最近者优先
- 第二原则：第一声明者优先
