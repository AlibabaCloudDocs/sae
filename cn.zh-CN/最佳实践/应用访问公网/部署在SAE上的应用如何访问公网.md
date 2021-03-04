---
keyword: [SAE访问公网, 访问公网, 应用访问公网]
---

# 部署在SAE上的应用如何访问公网

部署在SAE上的应用，其业务通常需要获取公网资源或者跨VPC访问，本文介绍部署在SAE上的应用如何从VPC内网环境访问公网。

## 背景信息

在业务部署过程中，可能会遇到以下几种场景需要访问公网：

-   容器在运行时需要建立公网依赖。
-   与第三方有合作，例如使用微信小程序需要上公网。
-   应用需要跨VPC或地域访问数据库。

## 实施方案

为同一VPC下的所有应用实例配置一个公共NAT网关代理并绑定EIP，通过SNAT功能为VPC内所有无公网IP地址的应用实例配置访问公网代理。

**说明：**

-   如果VPC内多个VSwitch下的实例需要出公网，那么针对多个VSwitch都需要配置SNAT。
-   单个VPC内存在多个应用访问公网，配置代理后仅需绑定1个EIP。

## 注意事项

如果您的VPC内存在多个NAT实例，您需要确保VPC内的路由表中的路由规则是绑定了SAE所关联的NAT实例。关于修改路由表的操作步骤，请参见[使用路由表](/cn.zh-CN/网络连接/路由策略/使用路由表.md)。

![路由表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4169501161/p226753.png)

## 步骤一：创建NAT网关

1.  登录[VPC控制台](https://vpc.console.aliyun.com)，在左侧导航栏单击**NAT网关**。

2.  在**NAT网关**页面，单击**组合购买EIP**。

3.  在**组合购买（NAT网关+弹性公网IP）**页面，设置相关信息，单击**立即购买**。

    参数说明如下。

    |参数|说明|
    |--|--|
    |地区|选择部署在SAE上的应用所在的地域。|
    |网关类型|默认为**增强型**。|
    |VPC ID|选择部署在SAE上的应用所在的VPC ID。|
    |交换机ID|选择交换机ID。|
    |EIP|    -   **选择已有**：您只需为所购买的NAT网关付费。
    -   **新购EIP**：您需设置弹性公网IP的参数，并为NAT网关和EIP付费。 |
    |计费周期|默认为**按天**。|
    |计费类型|选择**计费周期**。更多信息，请参见[NAT网关计费说明](/cn.zh-CN/购买指南/NAT网关计费说明.md)。|

4.  购买完成，并和NAT网关创建成功后，在**NAT网关**页面的NAT网关列表内可以查看到实例的弹性公网IP。

    ![网关信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6698501161/p96426.png)


## 步骤二：创建SNAT条目

创建SNAT条目，为专有网络中没有公网IP地址的应用实例，提供访问公网代理服务。

1.  在目标NAT网关的**操作**列单击**设置SNAT**。

    ![访问公网_NAT网关](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6698501161/p96430.png)

2.  在**SNAT管理**页签下方，**SNAT条目列表**区域单击**创建SNAT条目**。

    ![创建SANT条目](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6698501161/p226746.png)

3.  在**创建SNAT条目**页面，配置SNAT条目信息，单击**确定创建**。

    ![创建SNAT条目02](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6698501161/p57245.png)

    参数说明如下。

    |参数|说明|
    |--|--|
    |SANT条目粒度|选择**交换机粒度**。|
    |选择交换机|选择VPC中的交换机，该交换机下所有的应用实例均可通过SNAT功能进行公网访问。**说明：** 如果持有公网IP的应用实例（例如已经绑定了EIP）发起互联网访问，系统将优先使用其持有的公网IP地址，而不会使用NAT网关的SNAT功能。 |
    |交换机网段|选择交换机后，该区域会自动显示该交换机的网段。|
    |选择公网IP地址|选择用来提供互联网访问的公网IP地址。**说明：** 您创建SNAT条目的公网IP地址不能再用来创建SNAT条目。 |
    |条目名称|设置条目名称。|


