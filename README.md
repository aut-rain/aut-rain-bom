# aut-rain-bom

## 项目介绍

aut-rain 的项目统一依赖版本 BOM，为 Java 项目提供统一的第三方依赖版本管理，覆盖 Spring Boot、Spring Cloud、Dubbo、消息队列、数据库、缓存、对象存储、XXL-JOB 和常用工具库。

项目通过 Maven `dependencyManagement` 管理版本，不包含运行时代码。导入 BOM 不会自动引入依赖，使用方按需选择所需组件。

## 使用方式

在项目的 `pom.xml` 中导入 BOM：

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>io.github.aut-rain</groupId>
            <artifactId>aut-rain-bom</artifactId>
            <version>1.1.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

选择已发布到 Maven Central 或已安装到本地仓库的版本。导入后，在 `dependencies` 中声明所需依赖，无需重复填写受管理的版本号：

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
    </dependency>
    <dependency>
        <groupId>org.redisson</groupId>
        <artifactId>redisson-spring-boot-starter</artifactId>
    </dependency>
    <dependency>
        <groupId>com.xuxueli</groupId>
        <artifactId>xxl-job-core</artifactId>
    </dependency>
</dependencies>
```

BOM 管理依赖版本，Java 编译版本、构建插件以及组件运行配置由使用方项目设置。XXL-JOB 仍需自行配置执行器并连接独立部署的调度中心。

## 作者信息

- 作者：zzy
- 昵称：aut-rain
- 邮箱：2545946621@qq.com
- GitHub：[aut-rain](https://github.com/aut-rain)

## 开源协议

本项目采用 [MIT License](LICENSE) 开源协议。所管理的第三方依赖遵循各自的许可证。
