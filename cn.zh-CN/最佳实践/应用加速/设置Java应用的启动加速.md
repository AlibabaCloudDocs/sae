---
keyword: [启动加速, 应用加速, Java, Dragonwell, QuickStart, AppCDS, Wisp]
---

# 设置Java应用的启动加速

SAE对Java应用在部署过程中的不同阶段的启动效率做了一系列优化与提升。本文介绍如何通过设置，提升Java应用的启动效率。

设置启动加速的Java应用必须为JAR包或者WAR包部署。

## 提升应用启动时的效率

如果您希望提升应用的启动速度，您可以参考以下步骤，在创建应用时选择Dragonwell 11环境，并在启动命令设置中开启应用加速。本章节以在应用部署时设置相关参数为例，如果您希望为已经部署的应用提高启动效率，您可以参考以下文档：

-   [应用部署完成后挂载NAS](/cn.zh-CN/应用部署/设置NAS存储.mdsection_o8h_829_0jy)
-   [应用部署完成后配置启动命令](/cn.zh-CN/应用部署/设置启动命令.md)

应用运行效果如下所示。更多信息，请参见[Dragonwell Benchmark](http://ci.dragonwell-jdk.io/job/benchmarks.middleware.sae.startup/SAE_20Startup_20Report/)。

![启动加速](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6141339061/p208209.png)

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击**创建应用**。

3.  在**应用基本信息**页签，设置应用相关信息，配置完成后单击**下一步：应用部署配置**。

4.  在**应用部署配置**页签，配置相关参数。

    ![应用加速](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8150088061/p187704.png)

    参数说明如下表所示。

    |参数名|说明|
    |---|--|
    |技术栈语言|选择**Java**。|
    |应用部署方式|选择**WAR包部署**或者**JAR包部署**。本文中以**WAR包部署**为例。|
    |应用运行环境|选择您需要的应用环境，例如**apache-tomcat-8.5.42**。|
    |Java环境|选择**Dragonwell 11**。|
    |文件上传方式|可选择**上传WAR包**或**WAR包地址**。    -   **上传WAR包**：单击**选择文件**，选择待部署WAR包。
    -   **WAR包地址**：输入WAR包的存放地址。

**说明：** 应用部署程序包名仅允许字母、数字，及短划线（-）、下划线（\_）两个特殊符号。 |
    |版本|设置应用版本号，您可以选择输入版本号或者单击**使用时间戳为版本号**将时间戳作为应用版本号。|
    |时区设置|选择当前应用所在时区，例如**UTC+8**。|

5.  设置持久化存储，达到跨实例加速的效果。

    1.  展开**持久化存储**区域，打开**应用NAS存储**开关。

        ![挂载NAS配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8075623061/p67278.png)

    2.  在**使用已有的NAS文件系统**所在行的下拉列表中选择待挂载的NAS，并设置**挂载源**和**容器路径**。

6.  展开**启动命令设置**区域，选中**开启应用启动加速（Qucikstart）**，设置**持久化目录**。

    ![启动命令应用加速](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9446793161/p187709.png)

    参数说明如下表所示。

    |参数|说明|
    |--|--|
    |系统默认启动命令|SAE默认的启动命令。|
    |options设置|配置JVM参数。关于参数详情，请参见[JVM参数配置说明](/cn.zh-CN/最佳实践/JVM参数配置说明.md)、[Tuning Java Virtual Machines](https://docs.oracle.com/cd/E21764_01/web.1111/e13814/jvm_tuning.htm#PERFM150)和[JVM Tuning: How to Prepare Your Environment for Performance Tuning](https://sematext.com/blog/jvm-performance-tuning/)。如果您需要使用应用的远程调试功能，请配置以下命令：

    ```
-agentlib:jdwp=transport=dt_socket,address=9000,server=y,suspend=n
    ```

    -   transport：远程调试间的数据传输方式。
    -   address：远程调试的地址。与开启远程调试时设置的调试端口保持一致，远程调试的详细说明，请参见[Java远程调试](/cn.zh-CN/应用管理/远程调试/Java远程调试.md)。 |
    |args设置|配置标准输出和错误输出的重定向命令，例如`1>>/tmp/std.log>&1`。|
    |**options快捷设置**：只有**Java环境**为**Dragonwell**时可以设置。|
    |开启微服务性能提升（Wisp 2协程）|默认开启，开启后可以提升运行时多线程性能。|
    |开启应用内存优化（G1）|默认开启，开启后可以针对多CPU与大容量内存场景，降低GC时间，适用于GC需要优化、大数据等场景。|
    |开启应用启动加速（Quickstart）|只有**Java环境**为**Dragonwell 11**时可以设置。选中**开启应用启动加速（Quickstart）**并设置**持久化目录**后，可以提升应用启动效率。**说明：** 开启应用启动加速前，需要先设置NAS存储。具体操作，请参见[设置NAS存储](/cn.zh-CN/应用部署/设置NAS存储.md)。 |
    |持久化目录|开启应用加速后需要设置，设置的**持久化目录**推荐为NAS存储的目录或者子目录，达到跨实例间的加速效果。关于如何设置NAS存储，请参见[设置NAS存储](/cn.zh-CN/应用部署/设置NAS存储.md)。|

7.  单击**下一步：确认规格**。

8.  在**确认规格**页签，查看您所创建应用的详细信息以及配置费用情况，并单击**确认创建**。

9.  您可以通过以下方式验证配置是否生效。

    -   方法一：

        在应用的**变更记录**页面中查看应用变更详情，如果显示**执行成功**，则表示部署成功，即配置已生效。

    -   方法二：

        在应用**基本信息**页面的**实例部署信息**页签查看实例的**运行状态**。如果**运行状态**显示为绿色的**Running**，表示应用部署成功，即配置已生效。


## 提升应用运行时的效率

如果您希望提升应用运行时的效率，您可以在在创建应用时选择Dragonwell环境，并在启动命令设置中开启微服务性能提升（Wisp2协程）。具体步骤，请参见[提升应用启动时的效率](#section_rvx_qek_rqp)。

![开启微服务性能提升](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9446793161/p205869.png)

应用运行效果如下所示。更多信息，请参见[Dragonwell官方实时Benchmark](http://ci.dragonwell-jdk.io/job/benchmarks.middleware.sae.wisp/SAE_20Report/)。

![设置Wisp2后效果图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4385896061/p187807.png)

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索钉钉群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1176199061/p72048.png)

