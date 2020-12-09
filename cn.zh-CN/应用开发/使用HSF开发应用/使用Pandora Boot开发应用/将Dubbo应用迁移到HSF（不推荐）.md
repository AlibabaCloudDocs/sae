# 将Dubbo应用迁移到HSF（不推荐）

您可以通过添加Maven依赖、添加或修改Maven打包插件和修改配置，将使用Dubbo开发的应用迁移到HSF。不过，由于SAE已经支持原生Dubbo框架的应用，所以，新用户不建议使用此方式。

原生Dubbo框架下的应用开发请参见[使用 Spring Boot 开发 Dubbo 应用](/cn.zh-CN/应用开发/使用Dubbo开发应用/使用 Spring Boot 开发 Dubbo 应用.md)，您也可以直接下载[Dubbo转换为HSF的示例代码](http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/edas-dubbo-spring-boot-demo.zip)。

## 添加Maven依赖

在应用工程的pom.xml中，增加`spring-cloud-starter-pandora`的依赖。

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-pandora</artifactId>
    <version>1.3</version>
</dependency>
```

## 添加或修改Maven打包插件

在应用工程的pom.xml中，添加或修改Maven的打包插件。

**说明：** 为避免与其他打包插件发生冲突，请勿在build的plugin中添加其他FatJar插件。

```
<build>
    <plugins>
        <plugin>
            <groupId>com.taobao.pandora</groupId>
            <artifactId>pandora-boot-maven-plugin</artifactId>
            <version>2.1.9.1</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>repackage</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

## 修改配置

在Spring Boot的启动类中，添加两行加载Pandora的代码：

```
import com.taobao.pandora.boot.PandoraBootstrap;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication
    public class ServerApplication {

        public static void main(String[] args) {
            PandoraBootstrap.run(args);
            SpringApplication.run(ServerApplication.class, args);
            PandoraBootstrap.markStartupAndWait();
        }
    }
```

