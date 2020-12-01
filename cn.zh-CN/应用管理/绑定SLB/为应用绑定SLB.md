---
keyword: [SAE SLB, 绑定SLB, SLB]
---

# 为应用绑定SLB

在SAE中部署应用后，您可以通过添加负载均衡SLB（Server Load Balancer）实现公网访问，也可以添加私网SLB实现同VPC内所有应用间的互相访问。本文介绍如何为应用绑定SLB。

为应用绑定SLB前，请先了解以下文档：

-   [SLB使用限制](/cn.zh-CN/用户指南/产品限制/使用限制.md)
-   [t1855858.md\#](/cn.zh-CN/应用管理/绑定SLB/SLB使用说明.md)
-   [t1879367.md\#](/cn.zh-CN/应用管理/绑定SLB/SAE SLB配置实践.md)

不同场景下绑定SLB的前提条件如下所示：

-   场景一：绑定已有SLB
    1.  [上传已有SSL证书](/cn.zh-CN/用户指南/证书管理/创建证书/概述.md)
    2.  [在SAE控制台部署应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用WAR包部署Java Web应用.md)

        **说明：** 在SAE中复用的SLB实例需要满足以下条件：

        -   必须为非性能共享型SLB实例。
        -   必须为非容器服务独占的SLB实例。
        -   必须为通过[SLB控制台](https://slb.console.aliyun.com/)购买的SLB实例。SAE不复用其他产品代购或者独占的SLB实例，以防出现监听配置冲突。
        -   必须与部署在SAE上的应用所在的实例处于同一个VPC内。
-   场景二：绑定新建SLB
    1.  [上传已有SSL证书](/cn.zh-CN/用户指南/证书管理/创建证书/概述.md)
    2.  [创建SLB实例](/cn.zh-CN/快速入门/创建负载均衡实例.md)
    3.  [在SAE控制台部署应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用WAR包部署Java Web应用.md)

## 场景一：绑定已有SLB

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击具体应用名称。

3.  在应用**基本信息**页面的**应用访问设置**区域绑定SLB。

    -   添加私网SLB请单击**添加私网SLB访问**。
    -   添加公网SLB请单击**添加公网SLB访问**。
    本文以**添加公网SLB访问**为例。

    ![应用访问设置1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5565913061/p56572.png)

    1.  单击**公网访问地址**所在区域的**添加公网SLB访问**。

        ![添加公网SLB访问](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5565913061/p56535.png)

    2.  在**添加公网SLB访问**对话框的**请选择SLB**的下拉列表中选择已有的SLB。

    3.  配置SLB监听端口。

        -   TCP协议：
            -   **SLB端口**：提供公网访问应用的SLB端口，可设置范围为1~65535。
            -   **容器端口**：进程监听端口，由程序定义，例如：Web服务默认使用8080端口。
        -   HTTPS协议：
            -   **HTTPS端口**：提供公网访问应用的SLB端口，可设置范围为1~65535。
            -   **SSL证书**：SSL协议证书，在下拉列表中选择已上传的SSL证书。
            -   **容器端口**：进程监听的端口。由程序定义，例如：Web服务默认使用8080端口。
    4.  单击**确定**。

4.  结果验证。

    复制配置的SLB的IP地址及端口，例如`192.168.0.184:80`，在浏览器中输入地址并回车，即可分别进入各自的应用首页。

    如果访问地址区域未出现IP地址和端口信息，则表示绑定SLB失败，请查看变更记录并修复失败问题。更多信息，请参见[t1067675.md\#](/cn.zh-CN/应用管理/应用变更记录/查看变更记录.md)。


## 场景二：绑定新建SLB

如果您需要SAE为您全新代购SLB并将其绑定，具体操作，请参见[绑定已有SLB](#section_ibx_pk9_9p1)，在步骤3选择SLB时，在**请选择SLB**下拉列表中选择**新建**。

选择**新建**之后，SAE自动进行SLB配额检查和账户余额检查，检查通过后为应用自动购买全新的SLB实例，并在下方显示具体SLB信息。

![新建SLB](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5565913061/p175171.png)

## 相关操作

1.  修改SLB访问设置
2.  在应用**基本信息**页面的**应用访问设置**区域，请根据网络需求单击**编辑私网SLB访问**或**编辑公网SLB访问**。

    ![编辑删除SLB](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5565913061/p57199.png)

3.  在弹出的**编辑私网SLB访问**或**编辑公网SLB访问**对话框，修改所需信息并单击**确认**。


1.  删除SLB访问设置
2.  在应用**基本信息**页面的**应用访问设置**区域，单击**删除私网SLB访问**或**删除公网SLB访问**。

    ![编辑删除SLB](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5565913061/p57199.png)

3.  单击**确认**，并在**删除私网SLB访问**或者**删除公网SLB访问**对话框，单击**确认**。


## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9515823061/p72048.png)

