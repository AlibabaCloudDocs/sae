# 将Spring Cloud框架应用平滑迁移至SAE

如果您的Spring Cloud集群（包含多个应用）已经部署在阿里云上，您可以将应用迁移至SAE。本文说明了如何将应用平滑迁移到SAE中，以及实现基本的服务注册与发现。如果您的Spring Cloud集群尚未部署至阿里云，请提交工单或联系SAE技术支持人员获取完整的上云及迁移方案。

## 迁移流程

![迁移流程](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9346632261/p278735.png)

1.  迁移应用

    迁移的应用通常是无状态的，需要先进行应用迁移。

2.  迁移SLB或修改域名配置

    在应用迁移完成后，您还需要迁移SLB或修改域名配置。

    -   SLB
        -   如果您的应用在迁移之前已经使用SLB，应用迁移后可以复用该SLB。您可以根据您的实际需求选择绑定SLB的策略，具体操作，请参见[为应用绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)。
        -   如果您的应用在迁移之前没有使用SLB，建议在迁移完入口应用（如流程图中所示的API Gateway）后，为该应用创建并绑定一个新SLB。
        -   迁移方案中，推荐使用双注册和双订阅方案，以节约ECS成本。如果由于某种原因（例如原ECS端口被占用）不能复用原ECS，那么需要采用切流迁移方案，添加新的ECS用于应用迁移。在应用迁移完成后，依据迁移前应用是否使用SLB，选择复用SLB或创建SLB并绑定到迁移后应用。
    -   域名
        -   如果迁移后的应用可以复用SLB，则域名配置无需修改。
        -   如果迁移后的应用需要创建新的SLB并绑定，则需要在域名中添加新的SLB配置，并删除原来不再使用的SLB。具体操作，请参见[域名DNS修改](/cn.zh-CN/域名管理/域名修改/域名DNS修改.md)。
3.  迁移存储和消息队列
    -   如果应用迁移前已经部署在阿里云上，同时存储和消息队列同样使用了阿里云相关产品（如RDS、MQ等），那么应用迁移完成后，迁移前的存储和消息队列无需迁移。
    -   如果应用迁移前没有部署在阿里云上，请提交工单或联系SAE技术支持人员为您提供完整的上云及迁移到方案。

本文以Demo应用演示平滑迁移。Demo下载：[Demo](http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/sc-migration-examples.zip?spm=a2c4g.11186623.2.12.5d076696OB2xto&file=sc-migration-examples.zip)。

## 迁移方案

迁移应用有两种方案，切流迁移、双注册和双订阅迁移方案。两种方案均可保证应用正常运行不中断情况下完成平滑迁移。

**说明：** 本文将主要介绍双注册和双订阅方案。

-   切流迁移方案

    使用Spring Cloud Alibaba将原有的服务注册中心切换到Nacos。开发一套新的应用部署到SAE，最后通过SLB和域名配置来进行切流。

    如果选择此方案，请参见[将Spring Cloud应用托管到SAE](/cn.zh-CN/快速入门/微服务应用入门/将Spring Cloud应用托管到SAE.md)。

-   双注册和双订阅迁移方案

    双注册和双订阅迁移方案指在应用迁移时同时接入两个注册中心（原有注册中心和SAE注册中心），以保证已迁移的应用和未迁移的应用之间可相互调用。

    双注册和双订阅平滑迁移方案架构图如下：

    ![迁移方案GIF](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2877242261/p278748.gif)

    -   已迁移的应用和未迁移的应用之间可以互相发现，从而实现互相调用，保证了业务的连续性。
    -   使用方式简单，仅需要添加依赖，并修改极少代码，实现双注册和双订阅。
    -   支持查看消费者服务调用列表的详情，实时地查看到迁移的进度。
    -   支持在不重启应用的情况下，动态地变更服务注册的策略和服务订阅的策略，只需要重启一次应用就可以完成迁移。

## 迁移第一个应用

1.  制定应用迁移优先级。

    选择迁移需求优先级高的应用，建议从最下层Provider开始迁移。如果调用链路太复杂难分析，可以任意选一应用进行迁移。

2.  在应用程序中添加依赖并修改配置。

    1.  在`pom.xml`文件中添加`spring-cloud-starter-alibaba-nacos-discovery`依赖。

        ```
        <dependency>
             <groupId>org.springframework.cloud</groupId>
             <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
             <version>{相应的版本}</version>
         </dependency>
                                        
        ```

    2.  在`application.properties`中添加nacos-server的IP地址。

        ```
        spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848                            
        ```

    3.  添加多注册中心依赖`edas-sc-migration-starter`。

        Spring Cloud默认依赖中只能引入一个注册中心，存在多个注册中心时，启动会异常。如果需要至支持多注册，需要添加依赖`edas-sc-migration-starter`。

        ```
        <dependency>
             <groupId>com.alibaba.edas</groupId>
             <artifactId>edas-sc-migration-starter</artifactId>
             <version>1.0.2</version>
         </dependency>                            
        ```

3.  修改RibbonClients默认配置。

    Ribbon是实现负载均衡组件，应用从多个注册中心订阅服务，需要修改Ribbon配置。在应用启动的主类中，将RibbonClients默认配置修改为`MigrationRibbonConfiguration`。

    假设原有的应用主类启动代码如下：

    ```
    @SpringBootApplication
     public class ConsumerApplication {
         public static void main(String[] args) {
             SpringApplication.run(ConsumerApplication.class, args);
         }
     }                                
    ```

    修改后应用主类启动代码如下：

    ```
    @SpringBootApplication
     @RibbonClients(defaultConfiguration = MigrationRibbonConfiguration.class)
     public class ConsumerApplication {
         public static void main(String[] args) {
             SpringApplication.run(ConsumerApplication.class, args);
         }
     }                                
    ```

    **说明：**

    在本地修改应用或者应用部署到SAE后，如果对应用有其他控制需求，例如将应用注册到某些注册中心或从某些注册中心订阅，则可以通过Spring Cloud Config或Nacos Config动态地调整配置，而无需重启应用。调整配置的方法，请参见[动态调整服务注册和订阅方式](#li_zny_ay3_290)。

    要通过Spring Cloud Config或Nacos Config动态地调整配置，需要在应用中添加配置管理依赖和修改配置。如果使用Spring Cloud Config，请参见相应的开源文档。如果使用Nacos Config，请参见[实现配置管理](/cn.zh-CN/应用开发/使用Spring Cloud开发应用/实现配置管理.md)。

4.  将应用部署到SAE。

    根据实际需求将应用部署到SAE。具体操作，请参见[部署应用概述](https://help.aliyun.com/document_detail/113181.html)。

5.  结果验证。

    1.  观察业务运行是否正常。

    2.  查看服务订阅监控。

        -   Spring Boot 1.x版本：http://ip:port/dubboRegistry
        -   Spring Boot 2.x版本：http://ip:port/actuator/dubboRegistry
        如果应用开启了Spring Boot Actuator监控功能，请访问Actuator查看此应用订阅的各服务的RibbonServerList信息。Actuator地址如下： metaInfo中serverGroup字段表示此节点的服务注册中心。

        ![开启Spring Boot Actuator监控](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120424/cn_zh/1559123295576/edas-appDev-springCloud-app-migration-actuator.png)


## 迁移其他所有应用

按照[迁移第一个应用](#section_16u_xia_bhd)的步骤依次将所有应用迁移到SAE。

## 清理迁移配置

迁移完成后，删除原有的注册中心配置和迁移过程专用的依赖`edas-sc-migration-starter`。

`edas-sc-migration-starter`迁移专用的starter，长期使用对业务的稳定性没有影响，对于Ribbon负载均衡实现有一定的局限性，建议在迁移完毕后删除，并在业务量较小的时间段内进行分批重启应用。

-   动态调整服务注册和订阅方式

    应用迁移过程中，可以通过SAE配置管理功能动态变更服务注册和订阅方式。

-   动态调整服务订阅

    系统默认订阅策略是从所有注册中心订阅，并对数据进行聚合。

    您可以通过SAE的配置管理修改`spring.cloud.edas.migration.subscribes`属性，选择具体的注册中心订阅数据。

    ```
    spring.cloud.edas.migration.subscribes=nacos,eureka # 同时从Eureka和Nacos订阅服务。
    spring.cloud.edas.migration.subscribes=nacos        # 只从Nacos订阅服务。                        
    ```

-   动态变更服务注册

    系统默认订阅策略是从所有注册中心订阅。

    您可以通过SAE的配置管理来调整服务注册中心。

    通过修改`spring.cloud.edas.migration.registry.excludes`属性关闭指定的注册中心。

    ```
    spring.cloud.edas.migration.registry.excludes=   #默认值为空，注册到所有的服务注册中心。
    spring.cloud.edas.migration.registry.excludes=eureka   #关闭Eureka的注册。
    spring.cloud.edas.migration.registry.excludes=nacos,eureka   #关闭Nacos和Eureka的注册。                       
    ```

    应用运行时如需要动态修改服务注册策略，可使用Spring Cloud配置管理功能在运行时修改此属性。


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

