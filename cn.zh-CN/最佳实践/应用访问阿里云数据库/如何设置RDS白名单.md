---
keyword: [RDS数据库, RDS, 阿里云数据库]
---

# 如何设置RDS白名单

应用在SA E托管后，如果您需要访问RDS数据库，则需要为应用设置RDS白名单。本文介绍如何设置RDS白名单。

不同场景下，白名单设置的内容不同。本文我们将从以下场景来分别说明白名单设置的相关操作。

-   [场景一：应用访问本VPC内的RDS数据库](#section_03m_fax_xys)
-   [场景二：应用跨VPC或跨Region访问RDS数据库](#section_oig_j0g_gkw)

## 场景一：应用访问本VPC内的RDS数据库

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。

2.  在控制台页面左上角，选择实例所在地域。

3.  在左侧导航栏单击**实例列表**，然后在实例列表页面的**基本信息**页签内单击具体实例名称。

4.  在实例基本信息页面的左侧导航栏中单击**数据安全性**。

5.  在数据安全性页面的**白名单设置**页签中，单击default区域右侧的**修改**。

    ![设置RDS白名单](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8037933261/p283136.png)

6.  在弹出的对话框中，将SAE应用所在的VPC网络的网段地址配置在白名单中。

    1.  登录 [VPC控制台](https://vpc.console.aliyun.com/)，在专有网络列表中找到应用所在的VPC，单击该VPC的名称进入专有网络详情页面。

    2.  复制应用所在的VPC的IPv4网段。

        ![VPC详情页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9523933261/p53768.png)

    3.  在**组内白名单设置**框中粘贴该VPC的IPv4网段地址，然后单击**确定**。

        ![修改RDS白名单分组](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9037933261/p283140.png)

    完成设置后，您部署在SAE上的应用便可访问本VPC内的RDS数据库。


## 场景二：应用跨VPC或跨Region访问RDS数据库

不同VPC和不同Region之间逻辑上完全隔离，故常规情况下不能跨VPC和跨Region访问RDS数据库。若您的应用想跨VPC或跨Region访问RDS数据库，请按照下面步骤进行相关配置。

1.  前提准备。

    购买**NAT网关**和**弹性公网IP组合包**并保证SAE应用可以访问公网。具体步骤，请参见[SAE应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)。

2.  设置白名单。

    1.  进入修改白名单分组对话框。

        具体操作，请参见[场景一：应用访问本VPC内的RDS数据库](#section_03m_fax_xys)步骤1~5 。

    2.  在修改白名单分组对话框中，将SAE应用购买的弹性公网IP配置在白名单输入框中。

        1.  登录[VPC控制台](https://vpc.console.aliyun.com/)，在左侧导航栏单击**NAT网关**，复制应用实例所配置的**弹性公网IP**。

            ![配置NAT网关](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4506933261/p96437.png)

        2.  在**组内白名单**设置框中粘贴该VPC的**弹性公网IP**地址，然后单击**确定**。

            ![修改RDS白名单分组](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9037933261/p283140.png)

        完成配置后，您部署在SAE上的应用便可跨VPC、跨Region访问RDS数据库。


