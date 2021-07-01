# 使用Webshell诊断应用

本文介绍SAE的Webshell功能，以及SAE应用的网络环境（包括容器内的环境）等运维背景知识，并在此基础上介绍如何利用Webshell完成基本的运维需求。

## Webshell简介

您可以通过阿里云控制台直接获取ECS的Shell来完成运维需求。如果ECS内开启了SSH服务，且ECS存在弹性公网IP，那么在本地可以通过SSH服务获取ECS的Shell完成运维需求。

在SAE的场景中，容器是一个暂态的、供应用运行的环境，通常不需要进行运维。为了方便进行线上问题定位和排查，SAE在控制台提供了简易版Webshell，供您查看并调试自己的容器。

SAE应用容器的基础镜像是面向应用运行时的且暂态的，因此您的镜像不需要在镜像中启动SSH服务，仅需要带有可执行的`/bin/bash`即可，同时建议您带上所需的运维工具，方便排查。

**说明：** Webshell不支持Windows镜像。

## 操作步骤

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击具体应用名称。

3.  在应用**基本信息**页面，单击**实例部署信息**页签。

4.  在**实例部署信息**页签的**默认分组**区域，单击目标实例**操作**列的**Webshell**。

    ![webshell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2215893261/p232270.png)

5.  打开Webshell后，您可以单击窗口右上角的全屏图标，将窗口全屏显示。

    ![全屏webshell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3215893261/p232273.png)

6.  按需在Webshell窗口执行命令，查看并调试您的容器。


## 应用的网络环境

SAE应用置于自建的VPC网络，并提供了命名空间功能，可以将中间件层面的服务调用进行逻辑隔离。命名空间与VPC内的vSwitch为绑定关系，一个命名空间仅能对应一个vSwitch，一个vSwitch可以对应多个命名空间，即VPC内的IP地址为局域网地址，不同VPC内应用间无法访问。命名空间主要用于中间件逻辑隔离，不同命名空间内的应用在中间件层面是隔离的，如服务发现和配置下发等。

**说明：** 关于VPC的原理和产品介绍，请参见[VPC基础架构](https://help.aliyun.com/document_detail/34221.html)。

鉴于VPC的产品特性和当前的SAE的产品特性，容器无法直接触达VPC外的服务（OSS、镜像服务等阿里云产品除外）。在没有额外配置的情况下，您的容器单独运行在网络环境，因此您无法直接接触SAE应用容器。

容器无法触达公网的代码示例如下。

![容器无法触达公网的代码示例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9573405261/p96770.png)

容器内如果需要访问公网服务，须购买NAT，并在VPC内配置vSwitch的SNAT规则。具体操作，请参见[应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)。

SNAT规则可以让VPC内地址访问公网地址，从而能够调用公网显露的服务，获取公网资源。

## 构建镜像的方法

基于阿里云容器镜像服务，SAE集成了构建镜像和管理镜像的功能。用于构建的基础镜像为`centos:7`，并为您配置了语言与编码方式、时区和Open JDK运行环境等运行环境。

容器存在的目的是为了让应用运行起来，SAE不可能以占用所有用户运行资源为代价，集成过多的工具。因此，若您对容器内工具有更多需求，请自行构建镜像或者按需从OSS获取。更多信息，请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。

## 诊断应用

通常线上容器运维不必要。如果您需要进入容器并进行运维，存在一定的业务风险：

-   单点应用业务：可能导致容器内存耗尽，从而导致分钟级别的业务中断。
-   多点部署业务：可能导致业务秒级中断。

SAE应用的诊断有常规检查和上传搜集的日志两种方式。

-   常规检查

    常规检查方法众多。以Java应用为例，有进程检查、线程以及JVM的健康状态检查。

    -   执行命令`ps -ef | grep java`检查应用的Java进程是否存在。

        **说明：** 容器内通常使用主进程启动应用，如果应用被停止，则容器也会退出，SAE自动将退出的容器重新启动，防止业务中断。

        如果进程不存在，请执行`dmesg | grep -i kill`命令检查OOM日志。如果日志存在，表示应用的进程被停止，需要检查工作目录下`hs_err_pid{PID}.log`日志文件，并定位具体原因。

    -   Java类型应用在线分析还可以使用阿里巴巴开源软件[Arthas](https://github.com/alibaba/arthas)，建议在测试镜像中集成Arthas工具进行常规诊断。Arthas能够实时查看Java类加载情况，方便观察方法出参、入参和环境变量等。

        您可以执行以下命令下载并运行Arthas：

        ```
        wget https://alibaba.github.io/arthas/arthas-boot.jar
        java -jar arthas-boot.jar                                        
        ```

        **说明：** 接入Arhas前，请先连接公网。

-   日志上传

    由于容器内工具匮乏，推荐将容器内搜集到的日志上传到云端，并下载到本地进行分析。

    目前SAE没有容器内日志下载功能，由于OSS服务连通阿里云下所有网络环境，推荐使用阿里云OSS服务进行日志上传下载。

    通过OSS服务上传并下载日志的操作方法如下：

    1.  在容器内部安装OSS命令行工具。具体操作，请参见[安装OSS命令行工具](/cn.zh-CN/常用工具/命令行工具ossutil/概述.md)。

        本文中以64位Centos系统的root用户为例，在没有打通公网的情况下可以选择在本地下载，然后将这个文件上传到OSS，然后获取OSS的VPC内地址下载文件。

        ```
        wget http://gosspublic.alicdn.com/ossutil/1.5.0/ossutil64
        chmod 755 ossutil64                               
        ```

    2.  配置所需的OSS命令行工具，并附上当前地域VPC内的[Endpoint](/cn.zh-CN/开发指南/访问域名（Endpoint）/访问域名和数据中心.md)，填写用于接收上传文件的账号的[AccessKey]()，查看已经创建的Bucket，检查您的OSS服务是否可用。

        **说明：** 请确保账号（不必是当前账号，任意开通阿里云OSS服务的账号均可）已开通OSS服务。

        1.  按照提示配置您的AccessKey、Endpoint信息，无需填写STS Token。

            ```
            ./ossutil64 config  
            ```

        2.  检查账号是否可用，如果报错则配置错误，如果没有Bucket，则建议前往OSS控制台创建，命令行工具也支持创建。

            ```
            ./ossutil64 ls   
            ```

        3.  创建一个模拟的日志文件，用于上传。

            ```
            echo "Hello" > edas-app.log
            ./ossutil64 cp edas-app.log {bucket-address，例如：oss://test-bucket，可以从上述命令"./ossutil64 ls"中查看}    
            ```

    3.  从[OSS控制台](https://oss.console.aliyun.com/overview)或其他工具中找到您的日志文件，下载到本地，并使用您熟悉的工具进行分析。

