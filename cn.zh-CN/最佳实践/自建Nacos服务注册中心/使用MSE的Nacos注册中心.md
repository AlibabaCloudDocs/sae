---
keyword: [微服务, MSE, Nacos]
---

# 使用MSE的Nacos注册中心

本地开发的Spring Cloud应用或者Dubbo应用托管到SAE时，您可以使用SAE的注册中心，也可以使用MSE托管的注册中心。本文介绍如何搭建MSE的Nacos服务注册中心，并将应用部署在SAE进行托管。

-   已创建专有网络，并确保网络可用。具体操作，请参见[使用专有网络](/cn.zh-CN/专有网络和交换机/使用专有网络.md)。
-   执行应用程序前，请确保您Nacos注册中心的访问端口（如8848）已添加至您的安全组。

某创业公司现在需要将微服务应用托管至SAE，但期望使用MSE，不使用SAE注册中心。

本文以[将Spring Cloud应用托管到SAE](https://help.aliyun.com/document_detail/123013.html)中的Demo应用[Provider](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/eureka-service-provider.zip?spm=a2c4g.11186623.2.17.73289506P2lAoA&file=eureka-service-provider.zip)和[Conumser](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/eureka-service-consumer.zip)为例，指导您如何在MSE上创建Nacos服务注册中心，将服务应用托管至SAE。

如果是集群部署，请参见[集群部署说明](https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html)。

**说明：** 服务注册中心使用优先级：SAE服务注册中心\>MSE的Nacos服务注册中心\>自建Nacos。使用自建Nacos作为应用服务发现、配置管理等功能，您需要购买相应的资源进行搭建和维护，耗时耗力。使用MSE构建的Nacos集群，您仅需关注Nacos的构建位置、版本、网络和规格，不必关注Nacos的构建和维护，更加聚焦业务本身的实现。

## 步骤一：购买并构建Nacos引擎

1.  进入MSE实例创建页面。

    -   未开通MSE集群托管
        1.  登录[MSE产品页](https://www.aliyun.com/product/mse)。
        2.  在MSE产品页单击**超值资源包**。
        3.  选择您需要创建的MSE实例，例如**ZooKeeper**、**Eureka**和**Nacos**。

            进入MSE实例创建及购买页面。

    -   已开通MSE集群托管
        1.  登录[MSE管理控制台](https://mse.console.aliyun.com)。
        2.  在左侧导航栏选择**注册配置中心** \> **实例列表**。
        3.  在**实例列表**页面，单击**创建实例**。
2.  设置参数信息。

    ![Nacos基本信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8636574161/p245269.png)

    参数说明如下。

    |参数|描述|
    |--|--|
    |付费模式|MSE有预付费（包年包月）和按量付费（按小时）两种模式，如果您的服务注册中心使用时间在一个月以上，建议采用更加优惠的预付费（包年包月）模式。|
    |地域和可用区|选择您MSE实例所在地域。|
    |引擎类型|选择**Nacos**。 |
    |引擎版本|MSE Nacos支持两种引擎版本，**1.1.3**和**1.2.1**。推荐使用**1.2.1**。

**说明：** 目前仅1.2.1版本支持配置中心，1.1.3不包含配置中心功能。 |
    |引擎规格|MSE实例规格有四种规格，**1核2G**、**2核4G**、**4核8G**和**8核16G**。

请您根据实际情况选择合适的组件规格，关于组件的评估方法，请参见[微服务注册配置中心实例能力评估](/cn.zh-CN/产品定价/微服务注册配置中心/微服务注册配置中心实例能力评估.md)。 |
    |集群节点数|选择集群内的节点数，即一个集群需要多少台上述规格的节点组成。

**说明：** 强烈建议Nacos集群规模最小3个节点，否则无法保障高可用。 |
    |网络类型|网络类型包括专有网络和公网网络两种类型。|
    |专有网络|指逻辑隔离的私有网络，您可以自定义网络拓扑和IP地址，支持通过专线连接。适合于熟悉网络管理的用户。

**说明：** 如果选择**专有网络**，则需要选择具体VPC和交换机。 |
    |公网网络|IP地址由阿里云统一分配，配置简便，使用方便，适合对操作易用性要求比较高的场景。

**说明：** 如果选择**公网网络**，则需要购买公网流量。具体操作，请参见[配置公网带宽](#step_6)。 |
    |公网带宽|可选。如果您购买的实例需要通过公网访问，请添加公网流量。具体费用，请参见[公网费用](/cn.zh-CN/产品定价/微服务注册配置中心/价格说明.md)。|

3.  单击**立即购买**，在**确认订单**页面选中MSE服务协议，并依据提示支付。


## 步骤二：服务注册与发现

Nacos启动后，提供了服务注册发现功能，需要在应用侧指定服务注册中心。在应用程序执行后，系统会依据所设服务注册中心，自动进行服务注册与发现。

**说明：** 执行应用程序前，请确保您Nacos注册中心的访问端口（如8848）已添加至您的安全组。

1.  在服务应用侧指定注册中心，并运行Provider和Consumer应用。

    打开src\\main\\resources路径下的application.properties文件，指定Nacos Server的IP地址。

    -   Provider

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
        spring.cloud.nacos.discovery.server-addr=192.168.XX.XX:8848 #替换为您购买的Nacos注册中心的地址。                            
        ```

    -   Consumer

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
        spring.cloud.nacos.discovery.server-addr=192.168.XX.XX:8848 #替换为您购买的Nacos注册中心的地址。                            
        ```

2.  服务验证。

    -   Linux/Unix/Mac系统

        ```
        curl -X GET 'http://192.168.XX.XX:8848/nacos/v1/ns/instance/list?serviceName=service-provider'
        ```

        -   `service-provider`：服务名。
        -   `192.168.XX.XX:8848`：安装Nacos的主机IP地址和端口号。
        返回结果如下，表示服务发现成功。

        ![SAE产品自建Nacos提供注册中心之Provider服务发现成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9616401161/p65846.png)

    -   Windows系统

        在浏览器中输入`http://c:18082/echo-rest/{自定义变量}`或`http://127.0.0.1:18082/echo-feign/{自定义变量}`。

        返回结果如下，表示服务注册、发现成功。

        ![SAE产品自建Nacos提供注册中心](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9616401161/p65298.png)

        `127.0.0.1:18082`为运行Provider和Consumer的主机IP地址和访问端口。


## 步骤三：应用托管至SAE

将本地服务Provider和Consumer应用程序编译为WAR或者JAR包或者镜像，并部署到SAE。具体操作，请参见[应用部署概述](https://help.aliyun.com/document_detail/113181.html)。

**说明：**

-   使用MSE的Nacos注册中心时，请确保SAE的网络与Nacos的网络互通。
-   使用MSE的Nacos注册中心时，在部署应用时建议使用镜像方式或者JAR包方式，并配置启动参数`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。
    -   如采用镜像方式，请将`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`配置在镜像文件中。关于Docker镜像制作方法，请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。
    -   如采用JAR包方式，请在控制台**启动命令设置**区域的**options设置**文本框输入`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`。

如果应用托管失败，请参见以下文档定位问题：

-   [查看实时日志](/cn.zh-CN/应用管理/日志管理/查看实时日志.md)
-   [查看变更记录](/cn.zh-CN/应用管理/应用变更记录/查看变更记录.md)
-   [应用监控](/cn.zh-CN/应用监控/控制台功能/应用总览.md)

