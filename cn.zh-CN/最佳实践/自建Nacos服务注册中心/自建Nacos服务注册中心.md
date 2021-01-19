# 自建Nacos服务注册中心

本地开发的Spring Cloud应用或者Dubbo应用托管到SAE时，您可以使用SAE的注册中心，也可以自建Nacos提供服务注册与发现功能。本文介绍如何搭建Nacos注册中心，并将应用部署在SAE进行托管。

-   已安装yum。
-   执行应用程序前，请确保您Nacos注册中心的访问端口（如8848）已添加至您的安全组。

某创业公司现在需要将微服务应用托管至SAE，但期望使用自建Nacos注册中心，不使用SAE注册中心。

本文以[将Spring Cloud应用托管到SAE](https://help.aliyun.com/document_detail/123013.html)中的Demo应用[Provider](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/eureka-service-provider.zip?spm=a2c4g.11186623.2.17.73289506P2lAoA&file=eureka-service-provider.zip)和[Conumser](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/eureka-service-consumer.zip)为例，指导您如何在单机上自建Nacos服务注册中心，将服务应用托管至SAE。

如果是集群部署，请参见[集群部署说明](https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html)。

**说明：** 服务注册中心使用优先级：SAE服务注册中心\>MSE的Nacos服务注册中心\>自建Nacos。与SAE服务注册中心和MSE的Nacos服务注册中心相比，自建Nacos不仅需要购买各种搭建所需的资源，还需要投入尽力进行维护，耗费资源，增加运维成本。

## 步骤一：环境准备

Nacos依赖Java环境来运行。如果您是从代码开始构建并运行Nacos，请确保是在以下版本环境中安装使用。

-   64 bit OS，支持Linux/Unix/Mac/Windows，推荐选用Linux/Unix/Mac。
-   64 bit JDK 1.8及以上版本。

1.  查询可安装的JDK。

    ```
    yum -y list java*
    ```

2.  安装JDK。

    ```
    yum install -y java-latest-openjdk-devel.x86_64
    ```

3.  配置JAVA\_HOME。

    ```
    export JAVA_HOME=jdk-install-dir
    
    export PATH=$JAVA_HOME/bin:$PATH
    ```


## 步骤二：Nacos安装

1.  下载Nacos。

    ```
    wget https://github.com/alibaba/nacos/releases/download/1.1.3/nacos-server-1.1.3.zip
    ```

    **说明：** 如果您需要使用`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`配置，请确保您的Nacos版本为1.3.3及以上。

2.  解压Nacos并进入nacos/bin文件。

    ```
    unzip nacos-server-1.1.3.zip
    cd nacos/bin
    ```

    **说明：** 如果服务器上没有Unzip工具，请执行`yum install unzip`命令，并在安装后键入Y。

    ![解压Nacos](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9616401161/p64903.png)

3.  启动Nacos。

    ```
    sh startup.sh -m standalone
    ```

    ![启动Nacos](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9616401161/p64904.png)


## 步骤三：服务注册与发现

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
        spring.cloud.nacos.discovery.server-addr=192.168.XX.XX:8848                            
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
        spring.cloud.nacos.discovery.server-addr=192.168.XX.XX:8848                            
        ```

2.  服务验证。

    -   Linux/Unix/Mac系统

        ```
        curl -X GET 'http://192.168.XX.XX:8848/nacos/v1/ns/instance/list?serviceName=service-provider'
        ```

        -   `service-provider`：服务名
        -   `192.168.XX.XX:8848`：安装Nacos的主机IP地址和端口号。
        返回结果如下，表示服务发现成功。

        ![SAE产品自建Nacos提供注册中心之Provider服务发现成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9616401161/p65846.png)

    -   Windows系统

        在浏览器中输入`http://c:18082/echo-rest/{自定义变量}`或`http://127.0.0.1:18082/echo-feign/{自定义变量}`。

        返回结果如下，表示服务注册、发现成功。

        ![SAE产品自建Nacos提供注册中心](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9616401161/p65298.png)

        `127.0.0.1：18082`为运行Provider和Consumer的主机IP地址和访问端口。


## 步骤四：应用托管至SAE

将本地服务Provider和Consumer应用程序编译为WAR或者JAR包或者镜像，并部署到SAE。具体操作，请参见[应用部署概述](https://help.aliyun.com/document_detail/113181.html)。

**说明：**

-   使用自建Nacos时请确保SAE的网络与自建Nacos的网络互通。
-   使用自建Nacos为服务注册中心，在部署应用时建议使用镜像方式或者JAR包方式，并配置启动参数`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。
    -   如采用镜像方式，请将`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`配置在镜像文件中。关于Docker镜像制作方法，请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。
    -   如采用JAR包方式，请在控制台**启动命令设置**区域的**options设置**文本框输入`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`。

如果应用托管失败，请参见以下文档定位问题：

-   [查看实时日志](/cn.zh-CN/应用管理/日志管理/查看实时日志.md)
-   [查看变更记录](/cn.zh-CN/应用管理/应用变更记录/查看变更记录.md)
-   [应用监控](/cn.zh-CN/应用监控/控制台功能/应用总览.md)

