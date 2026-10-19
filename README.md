# aut-rain-bom

aut-rain 的项目统一依赖版本 BOM。

## 用途

集中管理常用 Java、Spring、RPC、消息、数据库、缓存、对象存储和工具库的兼容版本。该项目只提供 Maven `dependencyManagement`，不包含运行时代码，也不会自动引入任何依赖。

## 使用方式

在使用方项目的 `pom.xml` 中导入：

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.autrain</groupId>
            <artifactId>aut-rain-bom</artifactId>
            <version>1.0.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

导入后按需声明依赖即可省略版本号，例如：

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
</dependency>
```

## 坐标

```text
com.autrain:aut-rain-bom:1.0.0
```

作者：zzy（aut-rain）  
邮箱：2545946621@qq.com
