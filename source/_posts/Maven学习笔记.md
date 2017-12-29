---
title: Maven学习笔记
date: 2017-12-28 18:00:28
tags:
---


##### Maven是什么？
- 构建工具
- 依赖管理工具
- 项目信息管理工具

##### Maven的核心概念
- 坐标
- 依赖
- 仓库
- 生命周期
- 插件

```
mvn clean compile
```

```
mvn clean test
```

```
mvn clean package
```

<!--more-->

```
mvn clean install
//加参数-U可以强制让Maven检查更新
```

```
mvn clean deploy
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

##### 远程仓库的配置
**updatePolicy**
- daily:表示Maven每天检查一次，默认值
- never:从不检查更新
- always:每次构建都检查更新
- interval:每隔x分钟检查一次更新(x为任意整数)

**checksumPolicy**
- warn:Maven会在执行构建时输出警告信息
- fail:Maven遇到校验和错误就让构建失败
- ignore:使Maven完全忽略校验和错误

#### 聚合与继承

##### 可继承的POM元素
- **groupId**：项目组ID，项目坐标的核心元素
- **version**：项目版本，项目坐标的核心元素
- **description**：项目的描述信息
- **organization**：项目的组织信息
- **inceptionYear**：项目的创始年份
- **url**：项目的URL地址
- **developers**：项目的开发者信息
- **contributors**：项目的贡献者信息
- **distributionManagement**：项目的部署配置
- **issueManagement**：项目的缺陷跟踪系统信息
- **ciManagement**：项目的持续集成系统信息
- **scm**：项目的版本控制系统信息
- **mailingLists**：项目的邮件列表信息
- **properties**：自定义的Maven属性
- **dependencies**：项目的依赖配置
- **dependencyManagement**：项目的依赖管理配置
- **repositories**：项目的仓库配置
- **build**：包括项目的源码目录配置、输出目录配置、插件配置、插件管理配置等
- **reporting**：包括项目的报告输出目录配置、报告插件配置等


