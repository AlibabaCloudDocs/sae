# 使用Spring Cloud开发微服务应用并部署至SAE

本文以包含服务提供者和服务消费者的Spring Cloud应用为例，让您快速体验如何在本地开发、调试Spring Cloud应用并部署到SAE中，实现应用的服务注册与发现，以及消费者对提供者的调用。

-   如果您对Spring Cloud很陌生，仅了解Spring和Maven基础知识，那么阅读本文后，您将掌握如何通过Spring Cloud Alibaba Nacos Discovery实现Spring Cloud应用的服务注册与发现，以及实现消费者对提供者的调用。
-   如果您熟悉Spring Cloud中的Eureka、Consul和ZooKeeper等服务注册组件，但未使用过Spring Cloud Alibaba的服务注册组件Nacos Discovery，那么您仅需将服务注册组件的服务依赖关系和服务配置替换成Spring Cloud Alibaba Nacos Discovery，无需修改任何代码。

    Spring Cloud Alibaba Nacos Discovery同样实现了Spring Cloud Registry的标准接口与规范，与您之前使用Spring Cloud接入服务注册与发现的方式基本一致。

-   如果您熟悉如何使用开源版本的Spring Cloud Alibaba Nacos Discovery实现Spring Cloud应用的服务注册与发现，那么您可以将应用直接部署到SAE，即可使用到SAE提供的商业版服务注册与发现的能力。更多信息，请参见[应用部署概述](/cn.zh-CN/应用部署/应用部署概述.md)。

## 为什么使用SAE服务注册中心

SAE服务注册中心提供了开源Nacos Server的商用版本，使用开源版本`Spring Cloud Alibaba Nacos Discovery`开发的应用可以直接使用SAE提供的商业版服务注册中心。

SAE服务注册中心与Nacos、Eureka和Consul相比，具有以下优势：

-   共享组件，节省了部署、运维Nacos、Eureka或Consul的成本。
-   在服务注册和发现的调用中都进行了链路加密，保护您的服务，无需再担心服务被未授权的应用发现。
-   SAE服务注册中心与SAE其他组件紧密结合，为您提供一整套的微服务解决方案，包括环境隔离、灰度发布等。

您在SAE部署应用时，SAE服务注册中心以高优先级自动设置Nacos Server服务端地址和服务端口，以及命名空间、AccessKey、Context-path等信息，无需进行任何额外的配置。

## 视频教程

本视频仅介绍如何使用Spring Cloud开发微服务应用。应用的部署步骤，请参见[在SAE控制台部署应用](/cn.zh-CN/视频教程/应用部署/在SAE控制台部署应用.md)。



## 准备工作

在开始开发前，请确保您已经完成以下工作。

-   下载[Maven](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/App-develop/apache-maven-3.6.0-bin.tar.gz)并设置环境变量。
-   下载最新版本的[Nacos Server](https://github.com/alibaba/nacos/releases)。
-   按以下步骤启动Nacos Server。
    1.  解压下载的Nacos Server压缩包。
    2.  进入`nacos/bin`目录，启动Nacos Server。
        -   Linux/Unix/Mac系统：执行命令`sh startup.sh -m standalone`。
        -   Windows系统：双击执行`startup.cmd`文件。

## 创建服务提供者

在本地创建服务提供者应用工程，添加依赖，开启服务注册与发现功能，并将注册中心指定为Nacos Server。

1.  创建命名为`nacos-service-provider`的Maven工程。

2.  在`pom.xml`文件中添加依赖。

    以Spring Boot 2.1.4.RELEASE和Spring Cloud Greenwich.SR1为例，依赖如下：

    ```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.4.RELEASE</version>
        <relativePath/>
    </parent>
    
    <dependencies>
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
            <version>2.1.1.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Greenwich.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>                  
    ```

    示例中使用的版本为Spring Cloud Greenwich，对应Spring Cloud Alibaba版本为2.1.1.RELEASE。

    -   如果使用Spring Cloud Finchley版本，对应Spring Cloud Alibaba版本为2.0.1.RELEASE。
    -   如果使用Spring Cloud Edgware版本，对应Spring Cloud Alibaba版本为1.5.1.RELEASE。

        **说明：** Spring Cloud Edgware版本的生命周期已结束，不推荐使用该版本开发应用。

3.  在`src\main\java`下创建Package`com.aliware.edas`。

4.  在Package`com.aliware.edas`中创建服务提供者的启动类`ProviderApplication`，并添加以下代码。

    其中`@EnableDiscoveryClient`注解表明此应用需开启服务注册与发现功能。

    ```
        package com.aliware.edas;
    
        import org.springframework.boot.SpringApplication;
        import org.springframework.boot.autoconfigure.SpringBootApplication;
        import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
    
        @SpringBootApplication
        @EnableDiscoveryClient
        public class ProviderApplication {
    
            public static void main(String[] args) {
                SpringApplication.run(ProviderApplication.class, args);
            }
        }             
    ```

5.  在Package`com.aliware.edas`中创建`EchoController`。

    `EchoController`中，指定URL mapping为`/echo/{string}` ，指定HTTP方法为GET，从URL路径中获取方法参数，并回显收到的参数。

    ```
        package com.aliware.edas;
    
        import org.springframework.web.bind.annotation.PathVariable;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RequestMethod;
        import org.springframework.web.bind.annotation.RestController;
    
        @RestController
        public class EchoController {
            @RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
            public String echo(@PathVariable String string) {
                return string;
            }
        }              
    ```

6.  在`src\main\resources`路径下创建文件`application.properties`，在`application.properties`中添加如下配置，指定Nacos Server的地址。

    ```
        spring.application.name=service-provider
        server.port=18081
        spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848               
    ```

    其中`127.0.0.1`为Nacos Server的地址。如果您的Nacos Server部署在另外一台机器，则需要修改成对应的IP地址。如果有其它需求，可以在`application.properties`文件中增加配置。更多信息，请参见[\#d8e380](#d8e380)。

7.  验证结果。

    1.  执行`nacos-service-provider`中`ProviderApplication`的`main`函数，启动应用。

    2.  登录本地启动的Nacos Server控制台`http://127.0.0.1:8848/nacos`。

        本地Nacos控制台的默认用户名和密码同为nacos。

    3.  在左侧导航栏选择**服务管理** \> **服务列表**。

        可以看到服务列表中已经包含了`service-provider`，且在**详情**中可以查询该服务的详情。


## 创建服务消费者

本节除介绍服务注册的功能，还将介绍Nacos服务与RestTemplate和FeignClient两个客户端如何配合使用。

1.  创建命名为`nacos-service-consumer`的Maven工程。

2.  在`pom.xml`中添加依赖。

    ```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.4.RELEASE</version>
        <relativePath/>
    </parent>
    
    <dependencies>
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
            <version>2.1.1.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
    </dependencies>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Greenwich.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>        
    ```

3.  在`src\main\java`下创建Package`com.aliware.edas`。

4.  在Package`com.aliware.edas`中配置RestTemplate和FeignClient。

    1.  在Package`com.aliware.edas`中创建一个接口类`EchoService`，添加`@FeignClient`注解，并配置对应的HTTP URL地址及HTTP方法。

        ```
        package com.aliware.edas;
        
        import org.springframework.cloud.openfeign.FeignClient;
        import org.springframework.web.bind.annotation.PathVariable;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RequestMethod;
        
        @FeignClient(name = "service-provider")
        public interface EchoService {
            @RequestMapping(value = "/echo/{str}", method = RequestMethod.GET)
            String echo(@PathVariable("str") String str);
        }                   
        ```

    2.  在Package`com.aliware.edas`中创建启动类`ConsumerApplication`并添加相关配置。

        -   使用`@EnableDiscoveryClient`注解启用服务注册与发现。
        -   使用`@EnableFeignClients`注解激活FeignClient。
        -   添加`@LoadBalanced`注解将RestTemplate与服务发现集成。
        ```
        package com.aliware.edas;
        
        import org.springframework.boot.SpringApplication;
        import org.springframework.boot.autoconfigure.SpringBootApplication;
        import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
        import org.springframework.cloud.client.loadbalancer.LoadBalanced;
        import org.springframework.cloud.openfeign.EnableFeignClients;
        import org.springframework.context.annotation.Bean;
        import org.springframework.web.client.RestTemplate;
        
        @SpringBootApplication
        @EnableDiscoveryClient
        @EnableFeignClients
        public class ConsumerApplication {
        
            @LoadBalanced
            @Bean
            public RestTemplate restTemplate() {
                return new RestTemplate();
            }
        
            public static void main(String[] args) {
                SpringApplication.run(ConsumerApplication.class, args);
            }
        }
        ```

5.  在Package`com.aliware.edas`中创建类`TestController`以演示和验证服务发现功能。

    ```
        package com.aliware.edas;
    
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.web.bind.annotation.PathVariable;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RequestMethod;
        import org.springframework.web.bind.annotation.RestController;
        import org.springframework.web.client.RestTemplate;
    
        @RestController
        public class TestController {
    
            @Autowired
            private RestTemplate restTemplate;
            @Autowired
            private EchoService echoService;
    
            @RequestMapping(value = "/echo-rest/{str}", method = RequestMethod.GET)
            public String rest(@PathVariable String str) {
                return restTemplate.getForObject("http://service-provider/echo/" + str,
                        String.class);
            }
    
            @RequestMapping(value = "/echo-feign/{str}", method = RequestMethod.GET)
            public String feign(@PathVariable String str) {
                return echoService.echo(str);
            }
    
        }           
    ```

6.  在`src\main\resources`路径下创建文件`application.properties`，在`application.properties`中添加以下配置，指定Nacos Server的地址。

    ```
        spring.application.name=service-consumer
        server.port=18082
        spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    ```

    其中`127.0.0.1`为Nacos Server的地址。如果您的Nacos Server部署在另外一台机器，则需要修改成对应的IP地址。如果有其它需求，可以在`application.properties`文件中增加配置。更多信息，请参见[\#d8e380](#d8e380)。

7.  验证结果。

    1.  执行`nacos-service-consumer`中`ConsumerApplication`的`main`函数，启动应用。

    2.  登录本地启动的Nacos Server控制台`http://127.0.0.1:8848/nacos`。

        本地Nacos控制台的默认用户名和密码同为nacos。

    3.  在左侧导航栏中选择**服务管理** \> **服务列表**，可以看到服务列表中已经包含了`service-consumer`，且在详情中可以查询该服务的详情。


## 本地测试

在本地测试消费者对提供者的服务调用结果。

-   Linux/Unix/Mac系统：运行以下命令。

    ```
    curl http://127.0.0.1:18082/echo-rest/rest-rest
    curl http://127.0.0.1:18082/echo-feign/feign-rest
    ```

-   Windows系统：在浏览器中输入http://127.0.0.1:18082/echo-rest/rest-rest和http://127.0.0.1:18082/echo-feign/feign-rest。

## 将应用部署到SAE

在本地完成应用的开发和测试后，便可将应用打包并部署到SAE。具体步骤，请参见[部署应用概述](https://help.aliyun.com/document_detail/113181.htm)。

**说明：**

-   SAE暂不支持创建空应用，因此第一次部署需在控制台完成。
-   如果使用JAR包部署，在应用部署配置时选择**应用运行环境**为**标准Java应用运行环境**。
-   如果使用WAR包部署，在应用部署配置时**应用运行环境**为**pache-tomcat-XXX**。

当您将应用部署到SAE时，SAE服务注册中心会以更高优先级去设置Nacos Server服务端地址和服务端口，以及命名空间、AccessKey、Context-path信息。您无需进行任何额外的配置，原有的配置内容可以选择保留或删除。

**说明：**

-   使用自建Nacos时请确保SAE的网络与自建Nacos的网络互通。
-   使用自建Nacos为服务注册中心，在部署应用时建议使用镜像方式或者JAR包方式，并配置启动参数`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。
    -   如采用镜像方式，请将`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`配置在镜像文件中。关于Docker镜像制作方法，请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。
    -   如采用JAR包方式，请在控制台**启动命令设置**区域的**options设置**文本框输入`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`。

## 结果验证

1.  为部署到SAE的应用绑定SLB。具体步骤，请参见[绑定公网SLB](https://help.aliyun.com/document_detail/113305.html)。

2.  在浏览器输入配置好的公网访问地址，并在应用首页发起调用请求。

3.  登录SAE控制台，进入消费者应用详情页面，在左侧导航栏选择**应用监控** \> **应用总览**，查看服务调用数据总览。

    如果能够监测到调用数据，则说明服务调用成功。


## 配置项参考

|配置项|Key|默认值|说明|
|---|---|---|--|
|服务端地址|spring.cloud.nacos.discovery.server-addr|无|Nacos Server启动监听的IP地址和端口。|
|服务名|spring.cloud.nacos.discovery.service|$\{spring.application.name\}|给当前的服务命名。|
|网卡名|spring.cloud.nacos.discovery.network-interface|无|当IP未配置时，注册的IP为此网卡所对应的IP地址。如果网卡名也未配置，则默认取第一块网卡的地址。|
|注册的IP地址|spring.cloud.nacos.discovery.ip|无|优先级最高。|
|注册的端口|spring.cloud.nacos.discovery.port|-1|默认情况下不用配置，系统会自动探测。|
|命名空间|spring.cloud.nacos.discovery.namespace|无|常用场景之一是隔离不同环境的资源，例如开发测试环境和生产环境的资源（如配置、服务）隔离等。|
|Metadata|spring.cloud.nacos.discovery.metadata|无|使用Map格式配置，您可以根据自己的需求自定义一些和服务相关的元数据信息。|
|集群|spring.cloud.nacos.discovery.cluster-name|DEFAULT|配置成Nacos集群名称。|
|接入点|spring.cloud.nacos.discovery.endpoint|UTF-8|地域的某个服务的入口域名。通过此域名可以动态地获取服务端地址，此配置在部署到EDAS时无需填写。|
|是否集成Ribbon|ribbon.nacos.enabled|true|如果没有明确需求，不需要修改。|

更多关于Spring Cloud Alibaba Nacos Discovery的信息请参见开源版本的[Nacos Discovery](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Nacos-discovery)。

## 更多信息

-   更多关于Spring Cloud Alibaba Nacos Discovery的信息，请参见[Spring Cloud Alibaba Nacos Discovery](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Nacos-discovery)。
-   如果您在本地开发了依赖Eureka、Consul、ZooKeeper等组件实现的服务注册与发现的Spring Cloud应用，那么修改该应用的依赖配置并部署至SAE的相关操作请参见[将Spring Cloud应用托管到SAE](https://help.aliyun.com/document_detail/123013.html)。

## 问题反馈

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![问题反馈](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

