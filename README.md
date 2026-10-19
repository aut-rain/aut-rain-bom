# aut-rain-bom

aut-rain 的项目统一依赖版本 BOM。

## 用途

集中管理常用 Java、Spring、RPC、消息、数据库、缓存、对象存储和工具库的兼容版本。该项目只提供 Maven `dependencyManagement`，不包含运行时代码，也不会自动引入任何依赖。

## 使用方式

当前开发版本为 `1.1.0`（尚未发布），新增 XXL-JOB 执行器版本管理。发布前可通过 `mvn install` 在本地试用；已发布的 `1.0.0` 不包含此依赖管理。

在使用方项目的 `pom.xml` 中导入：

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

导入后按需声明依赖即可省略版本号，例如：

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
</dependency>
```

## XXL-JOB

导入本 BOM 后添加执行器 SDK，无需声明版本：

```xml
<dependency>
    <groupId>com.xuxueli</groupId>
    <artifactId>xxl-job-core</artifactId>
</dependency>
```

管理版本为 `3.3.0`，其上游使用 Spring Boot 3.5 / Spring 6.2，适合当前 BOM 的技术基线。`3.5.0` 是更新的正式版，但上游已使用 Spring Boot 4 / Spring 7，且涉及通信协议调整，因此暂不作为此版本的默认选择。

`xxl-job-core` 不是自动配置 starter。使用方需按官方示例配置 `XxlJobSpringExecutor`、调度中心地址、执行器名称、访问令牌和日志路径，并注册任务。调度中心 `xxl-job-admin` 单独部署，建议与执行器采用相同版本；本 BOM 不管理调度中心应用或第三方 starter。

选型依据及验证范围见 [1.1.0 变更说明](docs/releases/1.1.0.md)。

## 坐标

```text
io.github.aut-rain:aut-rain-bom:1.1.0
```

作者：zzy（aut-rain）  
邮箱：2545946621@qq.com

## 发布到 Maven Central

日常升级、验证、发布重试与故障排查请参阅 [迭代维护说明书](docs/迭代维护说明书.md)。

项目通过 GitHub Actions 发布到 Sonatype Maven Central Portal。首次发布前需要完成以下准备：

1. 在 Central Portal 验证 `io.github.aut-rain` 命名空间，并创建发布令牌。
2. 创建用于签名的 GPG 密钥，将 ASCII armored 私钥上传到 GitHub Actions secret `MAVEN_GPG_PRIVATE_KEY`。
3. 在 GitHub 仓库中配置以下 Actions secrets：
   - `CENTRAL_USERNAME`：Central Portal 发布令牌的用户名。
   - `CENTRAL_PASSWORD`：Central Portal 发布令牌的密码。
   - `MAVEN_GPG_PRIVATE_KEY`：GPG ASCII armored 私钥。
   - `MAVEN_GPG_PASSPHRASE`：GPG 私钥口令。
4. 修改 `pom.xml` 中的 `<version>`，提交并推送后创建版本标签：

```bash
git tag -a v1.1.0 -m "release: v1.1.0"
git push origin v1.1.0
```

标签推送后，GitHub Actions 会执行签名并发布。版本发布后不可覆盖，应使用新的版本号发布修订版本。
