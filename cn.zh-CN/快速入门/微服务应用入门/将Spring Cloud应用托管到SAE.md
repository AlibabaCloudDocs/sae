# 将Spring Cloud应用托管到SAE

本文以包含服务提供者（Provider）和服务消费者（Consumer）的Spring Cloud微服务应用为例，指导您将原依赖Eureka、Consul、ZooKeeper等组件实现服务注册与发现的Spring Cloud应用部署到SAE中，并实现应用的服务注册与发现，以及Consumer对Provider的调用。

下载最新版本[Nacos Server](https://github.com/alibaba/nacos/releases)，并已启动Nacos Server。

1.  解压已下载的Nacos Server压缩包。
2.  进入nacos/bin目录，启动Nacos Server。
    -   Linux/Unix/Mac系统：执行命令`sh startup.sh -m standalone`。
    -   Windows系统：双击执行startup.cmd文件。

## 为什么托管到SAE

原依赖Eureka、Consul、ZooKeeper和Redis等组件实现服务注册与发现的Spring Cloud应用，如果需要部署至SAE，仅需将原服务注册与发现中心和配置中心替换为Alibaba Nacos Discovery，无需修改任何业务代码。

SAE服务注册中心具有Spring Cloud Alibaba Nacos Discovery所有功能，SAE服务注册中心可以完全代替Eureka、Consul、ZooKeeper和Redis等，作为您微服务应用的服务注册中心。

将Spring Cloud应用托管到SAE，您仅需关注Spring Cloud应用自身的逻辑，无需再关注注册中心和配置中心的搭建和维护，托管后还可以使用SAE提供的弹性伸缩、一键批量启停、应用监控等功能，大幅度降低开发和运维成本。

如果您仍决定使用自建的Nacos作为服务注册中心，请参见[如何搭建Nacos为服务注册中心（不推荐）](/cn.zh-CN/最佳实践/自建Nacos服务注册中心/自建Nacos服务注册中心.md)。

## 步骤一：获取Demo

eureka-service-provider和eureka-service-consumer是SAE提供的微服务Demo应用程序包，二者均为已经接入Eureka的Spring Cloud应用。Consumer应用消费Provider应用提供的服务。

-   Provider应用：[eureka-service-provider](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/Demo/eureka-service-provider.zip)
-   Consumer应用：[eureka-service-consumer](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/Demo/eureka-service-consumer.zip)

## 步骤二：修改Provider应用的服务注册与发现配置

将云原生的Provider应用托管到SAE中，需要在应用程序中修改pom依赖，并指定Nacos Server的IP地址。

**说明：** 以下情况下需要指定Nacos Server的IP地址：

-   本地测试时，本地测试通过后再部署到SAE中。
-   SAE的服务注册中心为自建的Nacos。

1.  添加pom依赖。

    打开应用的pom.xml文件，将`spring-cloud-starter-netflix-eureka-client`替换成为`spring-cloud-starter-alibaba-nacos-discovery`，并设置Nacos Server的版本信息。

    替换前：

    ```
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>                            
    ```

    替换后：

    ```
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        <version>2.1.1.RELEASE</version>
    </dependency>                           
    ```

    **说明：**

    -   示例中使用的版本是Spring Cloud Greenwich，对应`spring-cloud-starter-alibaba-nacos-discovery`的版本为`2.1.1.RELEASE`。
    -   如果您使用的是Spring Cloud Finchley版本，对应`spring-cloud-starter-alibaba-nacos-discovery`的版本为`2.0.1.RELEASE`。
    -   如果您使用的是Spring Cloud Edgware版本，对应`spring-cloud-starter-alibaba-nacos-discovery`的版本为`1.5.1.RELEASE`。
2.  指定Nacos Server的IP地址。

    打开src\\main\\resources路径下的application.properties文件，指定Nacos Server的IP地址。

    修改前：

    ```
    spring.application.name=service-provider
    server.port=18081
    eureka.client.serviceUrl.defaultZone=http://127.0.0.1:8761/eureka/                            
    ```

    修改后：

    ```
    spring.application.name=service-provider
    server.port=18081
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848                            
    ```

    其中`127.0.0.1`为Nacos Server的IP地址。如果Nacos Server部署在其他机器上，则需要修改为对应的IP地址。如果有其它需求，请参见[配置项参考](#section_07h_l2l_rvu)在`application.properties`文件中增加所需配置。

3.  查询应用服务。

    1.  执行`nacos-service-provider`中`ProviderApplication`的`main`函数，启动应用。

    2.  登录本地启动的Nacos Server控制台`127.0.0.1:8848/nacos`，在左侧导航栏中选择**服务管理** \> **服务列表**。

        **说明：** 本地Nacos Server控制台的默认用户名和密码均为nacos。

        如果**服务列表**中显示**service-provider**，且在详情中可以查询该服务的详情，那么表示服务注册成功。


## 步骤三：修改Consumer应用的服务注册与发现配置

将云原生的Consumer应用托管到SAE中，需要在应用程序中修改pom依赖，并指定Nacos Server的IP地址。

**说明：** 以下情况下需要指定Nacos Server的IP地址：

-   本地测试时，本地测试通过后再部署到SAE中。
-   SAE的服务注册中心为自建的Nacos。

1.  添加pom依赖。

    打开应用的pom.xml文件，将`spring-cloud-starter-netflix-eureka-client`替换成为`spring-cloud-starter-alibaba-nacos-discovery`，并设置Nacos Server的版本信息。

    替换前：

    ```
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>                            
    ```

    替换后：

    ```
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        <version>2.1.1.RELEASE</version>
    </dependency>                           
    ```

    **说明：**

    -   示例中使用的版本是Spring Cloud Greenwich，对应`spring-cloud-starter-alibaba-nacos-discovery`的版本为`2.1.1.RELEASE`。
    -   如果您使用的是Spring Cloud Finchley版本，对应`spring-cloud-starter-alibaba-nacos-discovery`的版本为`2.0.1.RELEASE`。
    -   如果您使用的是Spring Cloud Edgware版本，对应`spring-cloud-starter-alibaba-nacos-discovery`的版本为`1.5.1.RELEASE`。
2.  指定Nacos Server的IP地址。

    打开src\\main\\resources路径下的application.properties文件，指定Nacos Server的IP地址。

    修改前：

    ```
    spring.application.name=service-consumer
    server.port=18082
    eureka.client.serviceUrl.defaultZone=http://127.0.0.1:8761/eureka/                            
    ```

    修改后：

    ```
    spring.application.name=service-consumer
    server.port=18082
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848                            
    ```

    其中`127.0.0.1`为Nacos Server的IP地址。如果Nacos Server部署在其他机器上，则需要修改为对应的IP地址。如果有其它需求，请参见[配置项参考](#section_07h_l2l_rvu)在`application.properties`文件中增加所需配置。

3.  查询应用服务。

    1.  执行`nacos-service-consumer`中`ConsumerApplication`的`main`函数，启动应用。

    2.  登录本地启动的Nacos Server控制台`127.0.0.1:8848/nacos`，在左侧导航栏中选择**服务管理** \> **服务列表**。

        **说明：** 本地Nacos Server控制台的默认用户名和密码均为nacos。

        如果**服务列表**中显示**service-consumer**，且在详情中可以查询该服务的详情，那么表示服务注册成功。


## 步骤四：查看Provider与Consumer的调用结果

在本地查看Consumer对Provider的服务调用结果。启动服务，执行`IP+port/echo-rest/{自定义变量}`或`IP+port/echo-feign/{自定义变量}`查看调用结果。

-   Linux/Unix/Mac系统：执行`curl http://127.0.0.1:18082/echo-rest/{自定义变量}`或`curl http://127.0.0.1:18082/echo-feign/{自定义变量}`。
-   Windows系统：在浏览器中输入`http://127.0.0.1:18082/echo-rest/{自定义变量}`或`http://127.0.0.1:18082/echo-feign/{自定义变量}`。

示例：以Windows系统为例，当显示以下结果时，表示Provider与Consumer业务调用成功。

![结果验证](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1463698951/p70441.png)

## 步骤五：将应用部署到SAE

1.  在应用的pom.xml文件中添加应用程序的打包配置，添加完成后执行mvn clean package命令将本地的程序编译成可执行的JAR包。

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
                     </execution>
                 </executions>
             </plugin>
         </plugins>
     </build>                        
    ```

2.  将编译好的Provider和Consumer应用包部署至SAE。具体操作，请参见[部署微服务应用到SAE](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用JAR文件部署微服务应用.md)。

    **说明：**

    -   SAE暂不支持创建空应用，因此第一次部署须在控制台完成。
    -   如果使用JAR包部署，在**应用部署配置**页签的**应用运行环境**须选择标准Java应用运行环境。
    -   如果使用WAR包部署，在**应用部署配置**页签的**应用运行环境**须选择apache-tomcat-XXX。
    当您将应用部署到SAE时，SAE服务注册中心以高优先级自动设置Nacos Server服务端地址和服务端口，以及命名空间、AccessKey ID、AccessKey Secret等信息，您无需进行任何额外的配置。对于原有的配置内容您可以保留或删除。

    **说明：**

    -   使用自建Nacos时请确保SAE的网络与自建Nacos的网络互通。
    -   使用自建Nacos为服务注册中心，在部署应用时建议使用镜像方式或者JAR包方式，并配置启动参数`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。
        -   如采用镜像方式，请将`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`配置在镜像文件中。关于Docker镜像制作方法，请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。
        -   如采用JAR包方式，请在控制台**启动命令设置**区域的**options设置**文本框输入`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`。

## 步骤六：结果验证

1.  为Consumer应用[绑定公网SLB](https://help.aliyun.com/document_detail/113305.html)，并在浏览器键入所设置的公网访问地址，进入应用首页。

2.  在应用首页发起调用请求，然后登录[SAE控制台](https://sae.console.aliyun.com/)，在左侧导航栏单击**应用列表**，在**应用列表**页面选择Consumer应用，进入**应用详情**页面。

3.  在左侧导航栏选择**应用监控** \> **应用总览**，查看服务调用数据总览。

    如果能够监测到调用数据，则说明服务调用成功。


## 配置项参考

|配置项|Key|默认值|说明|
|---|---|---|--|
|服务端地址|spring.cloud.nacos.discovery.server-addr|无|Nacos Server启动监听的IP 地址和端口。|
|服务名|spring.cloud.nacos.discovery.service|$\{spring.application.name\}|当前服务的名称。|
|网卡名|spring.cloud.nacos.discovery.network-interface|无|当IP地址未配置时，注册IP为此网卡所对应的IP地址。如果此项也未配置，则默认取第一块网卡的IP地址。|
|注册的IP地址|spring.cloud.nacos.discovery.ip|无|高优先级。|
|注册的端口|spring.cloud.nacos.discovery.port|-1|默认情况下不用配置，系统会自动探测。|
|命名空间|spring.cloud.nacos.discovery.namespace|无|不同环境的注册逻辑隔离，例如开发测试环境和生产环境的资源（如配置、服务）隔离等。|
|Metadata|spring.cloud.nacos.discovery.metadata|无|使用Map格式配置，您可以根据自己需要自定义和服务相关的元数据信息。|
|集群|spring.cloud.nacos.discovery.cluster-name|DEFAULT|配置成Nacos集群名称。|
|接入点|spring.cloud.nacos.discovery.enpoint|UTF-8|地域的某个服务的入口域名，通过此域名可以动态地获取服务端地址，此配置在部署到SAE时无需填写。|
|是否集成Ribbon|ribbon.nacos.enabled|true|一般不需要修改。|

更多关于Spring Cloud Alibaba Nacos Discovery的信息，请参见开源版本的[Spring Cloud Alibaba Nacos Discovery](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Nacos-discovery)文档。

## 更多信息

-   您在SAE部署完应用后，可以对应用进行更新、扩缩容、启停、删除应用等生命周期管理操作。具体操作，请参见[管理应用生命周期](/cn.zh-CN/应用管理/应用生命周期/管理应用生命周期.md)。
-   您在SAE部署完应用后，可以对应用进行自动弹性伸缩、SLB绑定和批量启停等提升应用性能的操作。具体操作，请参见以下文档：
    -   [绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)
    -   [配置弹性伸缩策略](/cn.zh-CN/应用管理/应用实例/配置弹性伸缩策略.md)
    -   [一键启停应用](/cn.zh-CN/应用管理/应用生命周期/一键启停应用.md)
    -   [配置管理](/cn.zh-CN/应用管理/ACM配置管理/配置管理概述.md)
    -   [变更实例规格](/cn.zh-CN/应用管理/应用实例/变更实例规格.md)
-   您在SAE部署完应用后，还可以对应用进行日志管理、监控管理、应用事件查看和变更记录查看等聚焦应用运行状态的操作。具体操作，请参见以下文档：
    -   [日志管理](/cn.zh-CN/应用管理/日志管理/查看实时日志.md)
    -   [监控管理](/cn.zh-CN/监控与报警/监控/基础监控.md)
    -   [应用事件查看](/cn.zh-CN/应用管理/应用变更记录/查看应用事件.md)
    -   [变更记录查看](/cn.zh-CN/应用管理/应用变更记录/查看变更记录.md)
    -   [使用Webshell诊断应用](/cn.zh-CN/应用管理/使用Webshell诊断应用.md)

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索钉钉群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1176199061/p72048.png)

