# 使用Alibaba Cloud Toolkit自动化部署微服务至SAE

本以介绍如何使用Alibaba Cloud Toolkit部署应用至SAE，以及对应用进行监控。

-   [开通SAE服务](/cn.zh-CN/快速入门/准备工作.md)。
-   下载[Maven](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/App-develop/apache-maven-3.6.0-bin.tar.gz)并设置环境变量。
-   下载并安装[JDK 1.8或更高版本](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
-   下载并安装 [IntelliJ IDEA （2018.3或更高版本）](https://www.jetbrains.com/idea/download/)。

**说明：** 由于JetBrains插件官方服务器设立在海外，如果因访问缓慢导致无法下载安装，请加入文末交流群，从Cloud Toolkit产品运营部获取离线安装包。

-   IntelliJ IDEA中已安装Alibaba Cloud Toolkit插件，具体请参见[t1067664.md\#section\_wei\_ien\_29a](/cn.zh-CN/应用部署/插件部署/通过IntelliJ IDEA插件部署应用.md)。

## 步骤一：在SAE创建Demo应用

SAE支持JAR包、WAR包和镜像三种方式部署应用，具体请参见[应用部署概述](/cn.zh-CN/应用部署/应用部署概述.md)。

本文以JAR包方式为例，在SAE分别创建Provider和Consumer应用，具体操作请参见[在SAE控制台使用JAR文件部署微服务应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用JAR文件部署微服务应用.md)。

## 步骤二：创建服务提供者

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

    示例中使用的版本为Spring Cloud Greenwich ，对应Spring Cloud Alibaba版本为2.1.1.RELEASE。

    -   如果使用Spring Cloud Finchley版本，对应Spring Cloud Alibaba版本为2.0.1.RELEASE。
    -   如果使用Spring Cloud Edgware版本，对应Spring Cloud Alibaba版本为1.5.1.RELEASE。
    **说明：** Spring Cloud Edgware版本的生命周期已结束，不推荐使用这个版本开发应用。

3.  在`src\main\java`下创建名为com.aliware.edas的**Package** 。

4.  在com.aliware.edas中创建服务提供者的启动类`ProviderApplication`，并添加如下代码。

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

5.  在Package`com.aliware.edas`中创建`EchoController`，指定URL mapping为 \{/echo/\{String\}\}，指定HTTP方法为GET，方法参数从URL路径中获得，回显收到的参数。

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

6.  在`src\main\resources`路径下创建文件application.properties，在application.properties中添加如下配置，并指定Nacos Server的访问地址。

    ```
    spring.application.name=service-provider
    server.port=18081
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848               
    ```

    其中`127.0.0.1`为Nacos Server的IP地址。如果您的Nacos Server部署在其他设备，则需要修改成对应的IP地址。

    **说明：** 如果您的服务注册中心为自建服务注册中心，请将`127.0.0.1`替换为您的自建服务中心地址。

7.  验证结果。

    1.  执行`nacos-service-provider`中`ProviderApplication`的`main`函数，启动应用。

    2.  登录本地启动的Nacos Server控制台`http://127.0.0.1:8848/nacos`（本地Nacos控制台的默认用户名和密码同为nacos）。

    3.  在左侧导航栏中选择**服务管理** \> **服务列表** 。

        可以看到服务列表中已经包含了**service-provider**，且在详情中可以查询该服务的详情。


## 步骤四：创建服务消费者

本内容除介绍服务注册的功能，还将介绍Nacos服务发现与RestTemplate和FeignClient两个客户端如何配合使用。

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

3.  在`src\main\java`下创建名为com.aliware.edas的**Package**。

4.  在 `com.aliware.edas`中配置RestTemplate和FeignClient。

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

    2.  在 `com.aliware.edas` 中创建启动类`ConsumerApplication`并添加相关配置。

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

5.  在 `com.aliware.edas` 中创建类`TestController`以演示和验证服务发现功能。

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

6.  在`src\main\resources`路径下创建文件`application.properties`，在`application.properties`中添加如下配置，指定Nacos Server的地址。

    ```
    spring.application.name=service-consumer
    server.port=18082
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    ```

    其中`127.0.0.1`为Nacos Server的IP地址。如果您的Nacos Server部署在其他设备，则需要修改成对应的IP地址。

    **说明：** 如果您的服务注册中心为自建服务注册中心，请将`127.0.0.1:8848`替换为您的自建服务中心地址。

7.  验证结果。

    1.  执行`nacos-service-consumer`中`ConsumerApplication`的`main`函数，启动应用。

    2.  登录本地启动的Nacos Server控制台`http://127.0.0.1:8848/nacos`（本地Nacos控制台的默认用户名和密码同为nacos）。

    3.  在左侧导航栏中选择**服务管理** \> **服务列表** 。

        可以看到服务列表中已经包含了**service-consumer**，且在详情中可以查询该服务的详情。


## 步骤五：本地测试

在本地测试消费者对提供者的服务调用结果。

-   Linux/Unix/Mac 系统：运行以下命令。

    ```
    curl http://127.0.0.1:18082/echo-rest/rest-rest
    curl http://127.0.0.1:18082/echo-feign/feign-rest
    ```

-   Windows系统：在浏览器中输入 http://127.0.0.1:18082/echo-rest/rest-rest 和 http://127.0.0.1:18082/echo-feign/feign-rest。

本示例以Windows系统为例。

![Spring Cloud微服务应用是使用MSE调用成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0007481951/p69683.png)

表示本地开发的微服务 Provider 和 Consumer 调用正常。

## 步骤六：部署应用至 SAE

应用程序完成开发后，您需要在 Cloud Toolkit 中配置部署任务信息，将您的业务代码发布至[步骤2](#section_yik_4pq_dnd)所创建的应用。

1.  配置 Cloud Toolkit 账户。

    1.  单击 Cloud Toolkit 图标![Alibaba Cloud Toolkit图标](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)，在下拉列表中单击 **Preference…**，在设置页面左侧导航栏选择 **Alibaba Cloud Toolkit** \> **Accounts** 。

    2.  在**Accounts**界面中设置**Access Key ID**和**Access Key Secret**，并单击**OK**。

        **说明：**

        **Access Key ID**和**Access Key Secret**获取方法：

        在**Accounts**界面中单击**Get existing AK/SK**，进入并登录阿里云登录页面，系统自动跳转至安全信息管理页面，获取**Access Key ID**和**Access Key Secret**。

2.  配置部署任务。

    1.  在IntelliJ IDEA上单击Cloud Toolkit 图标![Alibaba Cloud Toolkit图标](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)，并在下拉列表中选择 **Deploy to SAE**。

    2.  在**Deploy to SAE**运行配置页面，配置应用部署参数。配置完成后单击**Apply**保存设置。

        **说明：** 如果您使用自建服务注册中心，您还需要在**Advanced**页签中配置启动命令`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。

        -   Provider 应用配置

            配置应用部署的区域、命名空间和步骤2中创建的应用。

            ![在ACT上配置Provider](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3949185851/p76614.png)

        -   Consumer应用配置

            配置应用部署的区域、命名空间和步骤2中创建的应用。

            ![Consumer应用配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3949185851/p76617.png)

3.  部署应用。

    单击**Run**，运行Provider应用后，然后运行Consumer应用。

    ![运行时](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4949185851/p76628.png)

4.  结果验证。

    1.  为Consumer应用绑定SLB。

        具体操作参见[为应用绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)。

        ![为Consumer绑定SLB](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4949185851/p76635.png)

        ![为Consumer绑定SLB成功示意图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4949185851/p76636.png)

    2.  访问Consumer。

        1.  对Consumer发起HTTP请求。

            `curl http://47.111.58.18/echo-feign/feign-rest`

        2.  对Consumer发起HTTP请求，Consumer调用Provider。

            `curl http://47.111.58.18/echo-rest/rest-rest`

        ![调用请求](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4949185851/p76637.png)

    3.  在应用监控大盘查看调用数据。

        在Consumer应用的**应用监控**中查看应用调用信息。

        ![应用总览](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4949185851/p76640.png)

        ![应用详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5949185851/p76641.png)

        ![接口调用详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5949185851/p76642.png)


