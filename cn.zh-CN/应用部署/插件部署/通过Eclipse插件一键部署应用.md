# 通过Eclipse插件一键部署应用

您除了通过控制台方式将应用部署到SAE，还可以通过Alibaba Cloud Toolkit for Eclipse插件进行部署。

-   下载并安装[JDK1.8或更高版本](http://java.com/zh_CN/download/)。
-   下载并安装适用于Java EE开发的[Eclipse IDE、4.5.0（代号：Mars）或更高版本](http://www.eclipse.org/downloads/)。

Cloud Toolkit是阿里巴巴提供的免费IDE插件。您可以注册或使用已有的账号免费下载Cloud Toolkit，下载完成后，将其安装在IntelliJ IDEA中。

在本地完成应用程序的开发、调试及测试后，您可以通过本插件将应用程序快速部署到SAE。

## 安装Cloud Toolkit

1.  启动Eclipse。

2.  在菜单栏中选择**Help** \> **Install New Software**。

3.  在Available Software对话框的**Work with**文本框中，输入Cloud Toolkit for Eclipse的URLhttp://toolkit.aliyun.com/eclipse/，然后回车。

4.  组件配置。

    ![Cloud Toolkit组件配置-eclipse](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796141261/p53391.png)

    1.  在**type filter text**列表区域中，勾选需要的组件。

    2.  在下方**Details**区域中，清除勾选**Connect all update sites during install to find required software**。

    3.  单击**Next**。

5.  按照Eclipse安装页面的提示，完成后续安装步骤。

    **说明：** 如果安装过程中弹出没有数字签名的提示信息，请选择**Install anyway**。

6.  重启Eclipse。

    Cloud Toolkit插件安装完成后，重启Eclipse。重启后在工具栏显示Alibaba Cloud Toolkit 图标。

    ![安装Cloud Toolkit成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796141261/p53395.png)


## 配置Cloud Toolkit账号

使用Cloud Toolkit部署应用到云端时，需要调用阿里云的API，调用API时需要使用访问密钥（AccessKey，包括AccessKey ID和AccessKey Secret）进行云端身份验证。因此在部署应用之前，需要先在Cloud Toolkit中配置账户信息。

1.  [获取AccessKey]()。

2.  启动Eclipse。

3.  在顶部菜单栏，选择 **Windows** \> **Preferences**。

4.  在**Preferences**页面的左侧导航栏，选择**Alibaba Cloud Toolkit**\>**Accounts**。

5.  在Accounts页面，输入**Access Key ID**和**Access Key Secret**，并单击**Apply and Close**。

    ![Accounts设置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796141261/p53416.png)


## 将应用部署到SAE

Cloud Toolkit插件支持将应用以WAR包、JAR包或镜像方式部署到SAE。

1.  在Eclipse页面左侧的**Package Explorer**区域，右键单击待部署的工程名，并在弹出的菜单栏中选择**Alibaba Cloud** \> **Deploy to SAE…**。

    ![deploy_to_SAE](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796141261/p275415.png)

2.  在**Deploy to SAE**对话框中，依据需求选择应用的**Region**、**Namespace**和**Application**，并设置部署方式。

    ![应用部署配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6796141261/p53440.png)

    **说明：** 若您尚未在SAE上创建应用，可在对话框右上角单击**Create Serverless Application on SAE console**，跳转到SAE控制台创建应用。

    部署参数说明如下：

    |参数|参数|描述|
    |--|--|--|
    |应用信息（Application）|**Region**|应用所在地域。|
    |**Namespace**|应用所在命名空间。|
    |**Application**|应用名称。|
    |部署方式（Deploy File）|**Maven Build**|选择Maven Build方式来构建应用时，系统会默认添加一个Maven任务来构建部署包。如果您需要部署多模块工程中的一个子模块，请参见[使用Eclipse部署多模块工程中的子模块]()。|
    |**Upload File**|选择Upload File方式来构建应用时，选择上传您的WAR包或者JAR包，然后进行部署。|
    |**Image Address**|选择Image方式来构建应用时，需要填入一个镜像地址，然后进行部署。|

    **说明：** 若您已使用Jar/War包部署应用，使用Cloud Toolkit部署应用时只能选择Maven Build或Upload File两种部署方式；若您已使用镜像部署应用，使用Cloud Toolkit部署应用时只能选择Image部署方式。

3.  配置完成后，单击**Deploy**。

    -   部署开始后，Eclipse的**Console**区域会打印部署日志，可以根据日志信息检查部署结果。
    -   您可以登录[SAE控制台](https://www.aliyun.com/product/sae)，在应用详情的变更记录页面查看更新记录。

## 终止Cloud Toolkit插件运行

在插件运行过程中，如果现场需要运行其他插件，请在**Progress**页面终止SAE-deploy进程。

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

