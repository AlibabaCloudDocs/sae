# 如何设置MongoDB白名单

应用在SAE托管后，如果您需要访问MongoDB数据库，需要设置MongoDB白名单，本文介绍如何设置MongoDB白名单。

不同场景下，白名单设置的内容不同。本文我们将从以下场景来分别说明白名单设置的相关操作。

-   [场景一：应用访问本VPC内的MongoDB数据库](#section_vwv_u7o_gmg)
-   [场景二：应用跨VPC或跨Region访问MongoDB数据库](#section_c5x_y9m_a4m)

## 场景一：应用访问本VPC内的MongoDB数据库

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在控制台页面左上角，选择实例所在地域。

3.  在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**，找到目标实例，单击实例名称。

4.  在实例基本信息页面的左侧导航栏中，选择**数据安全性** \> **白名单设置**。

5.  在**default**分组右侧的**操作**列选择**手动修改**。

    ![mangodb白名单](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9523933261/p53799.png)

6.  在弹出的对话框中，将SAE应用所在的VPC网络的网段地址配置在白名单中。

    1.  登录[VPC控制台](https://vpc.console.aliyun.com/)，在专有网络页面的列表中找到应用所在的VPC，单击该VPC名称。

    2.  在VPC详情页面，复制应用所在VPC的IPv4网段。

        ![VPC详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9523933261/p53768.png)

    3.  在**允许访问IP名单**设置框中粘贴该VPC的IPv4网段地址，然后单击**确定**。

        ![mangodb修改白名单/手动修改](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9523933261/p53801.png)

        在完成配置后，您部署在SAE上的应用便可访问本VPC内的MongoDB数据库。


## 场景二：应用跨VPC或跨Region访问MongoDB数据库

不同VPC和不同Region之间逻辑上完全隔离，故常规情况下不能跨VPC和跨Region访问 MongoDB数据库。若您的应用想跨VPC或跨Region访问MongoDB数据库，请按照以下步骤进行相关配置。

1.  前提准备
2.  购买NAT网关和弹性公网IP组合包并保证SAE应用可以访问公网。

    具体操作，请参见[部署在SAE上的应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)。

3.  设置白名单
4.  进入修改白名单分组对话框。

    具体操作，请参见[场景一：应用访问本VPC内的MongoDB数据库](#section_vwv_u7o_gmg)步骤1~5。

5.  在修改白名单分组对话框中，将为应用购买的弹性公网IP配置在白名单中。

    1.  登录[VPC控制台](https://vpc.console.aliyun.com/)，在左侧导航栏单击**NAT网关**，复制应用实例所配置的**弹性公网IP**。

        ![NAT网关页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9523933261/p96439.png)

    2.  在**允许访问IP名单**设置框中粘贴该**VPC的弹性公网IP**地址，然后单击**确定**。

        ![mangodb修改白名单/手动修改](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9523933261/p53801.png)

        在完成配置后，您部署在SAE上的应用便可跨VPC、跨Region访问MongoDB数据库。


