# 使用Spring Boot开发Dubbo应用

除了可以使用传统的XML配置方式开发Dubbo应用，还可以使用Spring Boot开发Dubbo应用，特别对于Java技术薄弱和Maven经验少，且又不熟悉Dubbo框架的开发者更为适合。本文以全新开发过程，向您展示如何使用Spring Boot开发Dubbo应用，并使用SAE服务注册中心实现服务注册与发现。

-   下载[Maven](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/App-develop/apache-maven-3.6.0-bin.tar.gz)并设置环境变量。
-   下载最新版本的[Nacos Server](https://github.com/alibaba/nacos/releases)。
-   启动Nacos Server。

    1.  解压下载的Nacos Server压缩包
    2.  进入`nacos/bin`目录，启动Nacos Server。
        -   Linux/Unix/Mac系统：执行命令`sh startup.sh -m standalone`。
        -   Windows系统：双击执行`startup.cmd`文件。

## 为什么使用Spring Boot开发Dubbo应用

Spring Boot简化了微服务应用的配置和部署，同时Nacos又同时提供了服务注册发现和配置管理功能，两者结合的方式能够帮助您快速搭建基于Spring的Dubbo服务，相比xml的开发方式，大幅提升开发效率。

全新场景使用Spring Boot开发Dubbo应用有两种主要的方式：

-   使用xml开发。
-   使用Spring Boot的注解方式开发。

使用xml方式请参考[将Dubbo应用托管到SAE](/cn.zh-CN/应用开发/使用Dubbo开发应用/将Dubbo应用托管到SAE.md)。文本档介绍如何使用Spring Boot的注解方式开发Dubbo服务。

## 视频教程

本视频仅介绍使用Spring Boot开发Dubbo应用，部署部分请参见[在SAE控制台部署应用](/cn.zh-CN/视频教程/应用部署/在SAE控制台部署应用.md)。



## 示例工程

您可以按照本文的逐步搭建工程，也可以选择直接下载本文对应的[示例工程](https://github.com/aliyun/alibabacloud-microservice-demo/archive/master.zip)，或者使用Git来clone：`git clone https://github.com/aliyun/alibabacloud-microservice-demo.git`

该项目包含了众多了示例工程，本文对应的示例工程位于`alibabacloud-microservice-demo/microservice-doc-demo/dubbo-samples-spring-boot`。

## 创建服务提供者

1.  创建命名为`spring-boot-dubbo-provider`的Maven工程。

2.  在`pom.xml`文件中添加所需的依赖。

    这里以Spring Boot 2.0.6.RELEASE为例。

    ```
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.0.6.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.apache.dubbo</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>2.7.3</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba.nacos</groupId>
            <artifactId>nacos-client</artifactId>
            <version>1.1.1</version>
        </dependency>
    </dependencies>                   
    ```

3.  开发Dubbo服务提供者。

    Dubbo中服务都是以接口的形式提供的。

    1.  在`src/main/java`路径下创建一个package`com.alibaba.edas.boot`。

    2.  在`com.alibaba.edas.boot`下创建一个接口（interface）`IHelloService`，里面包含一个`SayHello`方法。

        ```
        package com.alibaba.edas.boot;
        public interface IHelloService {
        String sayHello(String str);
        }                                
        ```

    3.  在`com.alibaba.edas.boot`下创建一个类`IHelloServiceImpl`，实现此接口。

        ```
        package com.alibaba.edas.boot;
        import com.alibaba.dubbo.config.annotation.Service;
        @Service
        public class IHelloServiceImpl implements IHelloService {
        public String sayHello(String name) {
          return "Hello, " + name + " (from Dubbo with Spring Boot)";
         }
        }                                
        ```

        **说明：** 这里的Service注解是Dubbo提供的一个注解类，类的全名称为：**com.alibaba.dubbo.config.annotation.Service**。

4.  配置Dubbo服务。

    1.  在`src/main/resources`路径下创建`application.properties`或`application.yaml`文件并打开。

    2.  在`application.properties`或`application.yaml`中添加如下配置。

        ```
        # Base packages to scan Dubbo Components (e.g @Service , @Reference)
        dubbo.scan.basePackages=com.alibaba.edas.boot
        dubbo.application.name=dubbo-provider-demo
        dubbo.registry.address=nacos://127.0.0.1:8848                                
        ```

        **说明：**

        -   以上三个配置没有默认值，必须要给出具体的配置。
        -   `dubbo.scan.basePackages`的值是开发的代码中含有`com.alibaba.dubbo.config.annotation.Service`和`com.alibaba.dubbo.config.annotation.Reference`注解所在的包。多个包之间用逗号隔开。
        -   `dubbo.registry.address`的值前缀必须以**nacos://**开头，后面的IP地址和端口指的是Nacos Server的地址。代码示例中为本地地址，如果您将Nacos Server部署在其它机器上，请修改为实际的IP地址。
5.  开发并启动Spring Boot入口类`DubboProvider`。

    ```
        package com.alibaba.edas.boot;
    
        import org.springframework.boot.SpringApplication;
        import org.springframework.boot.autoconfigure.SpringBootApplication;
    
        @SpringBootApplication
        public class DubboProvider {
    
            public static void main(String[] args) {
                SpringApplication.run(DubboProvider.class, args);
            }
    
        }                        
    ```

6.  登录Nacos控制台`http://127.0.0.1:8848`，在左侧导航栏中单击**服务列表**，查看提供者列表。

    可以看到服务提供者里已经包含了`com.alibaba.edas.boot.IHelloService`，且可以查询该服务的服务分组和提供者IP。


## 创建服务消费者

1.  创建一个Maven工程，命名为`spring-boot-dubbo-consumer`。

2.  在`pom.xml`文件中添加相关依赖。

    这里以Spring Boot 2.0.6.RELEASE为例。

    ```
        <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.0.6.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.apache.dubbo</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>2.7.3</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba.nacos</groupId>
            <artifactId>nacos-client</artifactId>
            <version>1.1.1</version>
        </dependency>
    
    </dependencies>                        
    ```

    如果您需要选择使用Spring Boot 1.x的版本，请使用Spring Boot 1.5.x版本，对应的com.alibaba.boot:dubbo-spring-boot-starter版本为0.1.0。

    **说明：** Spring Boot 1.x版本的生命周期即将在2019年08月结束，推荐使用新版本开发您的应用。

3.  开发Dubbo消费者。

    1.  在`src/main/java`路径下创建package`com.alibaba.edas.boot`。

    2.  在`com.alibaba.edas.boot`下创建一个接口（interface）`IHelloService`，里面包含一个`SayHello`方法。

        ```
        package com.alibaba.edas.boot;
        
        public interface IHelloService {
         String sayHello(String str);
        }                                
        ```

4.  开发Dubbo服务调用。

    例如需要在Controller中调用一次远程Dubbo服务，开发的代码如下所示。

    ```
    package com.alibaba.edas.boot;
    
    import com.alibaba.dubbo.config.annotation.Reference;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    
    @RestController
        public class DemoConsumerController {
    
            @Reference
            private IHelloService demoService;
    
            @RequestMapping("/sayHello/{name}")
            public String sayHello(@PathVariable String name) {
                return demoService.sayHello(name);
            }
        }                        
    ```

    **说明：** 这里的Reference注解是com.alibaba.dubbo.config.annotation.Reference。

5.  在`application.properties/application.yaml`配置文件中新增以下配置。

    ```
    dubbo.application.name=dubbo-consumer-demo
    dubbo.registry.address=nacos://127.0.0.1:8848                        
    ```

    **说明：**

    -   以上两个配置没有默认值，必须要给出具体的配置。
    -   `dubbo.registry.address`的值前缀必须以`nacos://`开头，后面的IP地址和端口为Nacos Server的地址。代码示例中为本地地址，如果您将Nacos Server部署在其它机器上，请修改为实际的IP地址。
6.  开发并启动Spring Boot入口类`DubboConsumer`。

    ```
    package com.alibaba.edas.boot;
    
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    
    @SpringBootApplication
    public class DubboConsumer {
    
        public static void main(String[] args) {
            SpringApplication.run(DubboConsumer.class, args);
        }
    
    }                        
    ```

7.  登录Nacos控制台`http://127.0.0.1:8848`，在左侧导航栏中单击**服务列表**，再在服务列表页面查看调用者服务。

    可以看到包含了`com.alibaba.edas.boot.IHelloService`，且可以查看该服务的服务分组和调用者IP。


## 结果验证

```
`curl http://localhost:8080/sayHello/SAE`

`Hello, SAE (from Dubbo with Spring Boot)`            
```

## 部署到SAE

本地使用Nacos作为注册中心的应用，可以直接部署到SAE中，无需做任何修改，注册中心会被自动替换为SAE上的注册中心。

您可以根据实际需求选择部署途径（控制台或工具），详情请参见[应用部署概述](/cn.zh-CN/应用部署/应用部署概述.md)。

使用控制台部署前，请参见如下操作将应用程序编译为可运行的JAR包、WAR包。

1.  在`pom.xml`文件中添加以下打包插件的配置。

    -   Provider

        ```
        <build>
         <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
                   <executions>
                       <execution>
                           <goals>
                               <goal>repackage</goal>
                           </goals>
                           <configuration>
                               <classifier>spring-boot</classifier>
                               <mainClass>com.alibaba.edas.boot.DubboProvider</mainClass>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
         </plugins>
        </build>                                
        ```

    -   Consumer

        ```
        <build>
         <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
                   <executions>
                       <execution>
                           <goals>
                               <goal>repackage</goal>
                           </goals>
                           <configuration>
                               <classifier>spring-boot</classifier>
                               <mainClass>com.alibaba.edas.boot.DubboConsumer</mainClass>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
         </plugins>
        </build>                                
        ```

2.  执行mvn clean package将本地的程序打成JAR包。


## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索钉钉群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1176199061/p72048.png)

