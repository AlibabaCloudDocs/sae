# 使用Cloud Toolkit实现端云互联（IntelliJ IDEA）

在开发应用时，您可以使用Alibaba Cloud Toolkit插件实现本地应用和部署在SAE中的应用的相互调用，即端云互联，帮助您提升开发效率。本文介绍使用Cloud Toolkit实现端云互联的前提条件及操作步骤。

-   不同的开发框架使用限制如下：
    -   基于Dubbo框架开发的应用需满足下面的版本条件才可支持端云互联：
        -   Dubbo 2.7.2、edas-dubbo-extension 2.0.2或以上版本
        -   Dubbo 2.7.2、dubbo-nacos-registry 2.7.2或以上版本
    -   基于Spring Cloud框架开发的应用使用Nacos进行配置管理时，Spring Cloud Alibaba需满足下面的版本才可支持端云互联：

        Spring Cloud Alibaba 1.0.0或以上版本

    -   基于HSF框架开发的应用无限制。
-   安装[IntelliJ IDEA](https://www.jetbrains.com/idea/download)，请选择2018.3或以上版本。

    **说明：** 因JetBrains插件市场官方服务器在海外，如因访问速度缓慢而无法下载，请使用钉钉扫描文章末尾的二维码进入用户群，向Cloud Toolkit工作人员获取离线安装包。

-   在应用所在VPC内创建一台可使用SSH登录的ECS，用于建立端云互联通道，详情请参见[通过控制台使用ECS实例（快捷版）云服务器ECS快速入门](/cn.zh-CN/快速入门/通过控制台使用ECS实例（快捷版）.md)。

    **说明：**

    -   ECS与应用必须处于同一VPC内。
    -   SSH通道需要使用密码方式登录，暂不支持使用密钥对登录。

## 步骤一：安装Cloud Toolkit

1.  启动IntelliJ IDEA。

2.  在IntelliJ IDEA中安装插件。

    -   **macOS系统**： 在顶部菜单栏选择**IntelliJ IDEA** \> **Preference...**，在**Preference**配置页面左边导航栏单击**Plugins**，搜索Alibaba Cloud Toolkit，并单击**Install**安装。

        ![在IntelliJ IDEA中安装插件—mac](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9395552061/p133847.png)

    -   **Windows系统**：在顶部菜单栏选择**File** \> **Settings**，在**Settings**页面的左侧导航栏单击**Plugins**，搜索Alibaba Cloud Toolkit，并单击**Install**安装。

        ![在IntelliJ IDEA中安装插件—windows](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9395552061/p133851.png)

3.  在IntelliJ IDEA中插件安装成功后，重启IntelliJ IDEA，您可以在工具栏看到Alibaba Cloud Toolkit的图标（![Alibaba Cloud Toolkit图标](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9067688951/p133853.png)）。


## 步骤二：配置Cloud Toolkit账号

在安装完Alibaba Cloud Toolkit后，您需使用AccessKey ID和AccessKey Secret来配置Cloud Toolkit的账号。

1.  在顶部菜单栏中选择**Tools** \> **Alibaba Cloud** \> **Preferences...**。

2.  在Settings对话框中选择**Alibaba Cloud Toolkit** \> **Accounts**。

3.  在**Accounts**界面中设置**AccessKey ID**和**AccessKey Secret**，然后单击**OK**。

    如果您使用子账号的AccessKey ID和AccessKey Secret，请确认该子账号至少拥有**部署应用**的权限，具体操作步骤请参见[为RAM用户授权](/cn.zh-CN/用户管理/为RAM用户授权.md)。

    ![Accounts](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0495552061/p133860.png)

    关于阿里云账号说明如下：

    -   如果您已经注册过阿里云账号，在**Accounts**界面中单击**Get existing AK/SK**，进入阿里云登录页面。用已有账号登录后，跳转至安全信息管理页面，获取**AccessKey ID**和**AccessKey Secret**。
    -   如果您还没有阿里云账号，在**Accounts**界面中单击**Sign up**，进入阿里云账号注册页面，注册账号。注册完成后按照上述方式获取**AccessKey ID**和**AccessKey Secret**。

## 步骤三：端云互联配置

1.  在顶部菜单栏中选择**Tools** \> **Alibaba Cloud** \> **Preferences...**。

2.  在**Settings**对话框中选择**Alibaba Cloud Toolkit** \> **Microservice**。

3.  在**Microservice**界面中选中**端云互联**，配置端云互联相关参数，然后单击**Apply**。

    ![配置端云互联参数](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6827562061/p173025.png)

    参数说明如下：

    |参数|描述|
    |--|--|
    |**产品**|选择**Serverless 应用引擎（SAE）**。|
    |**云端互联环境**|设置端云互联应用所在的地域和命名空间。|
    |**SpringCloud服务端口**|如果是Spring Cloud应用，您需要在**SpringCloud服务端口**区域内添加该应用的服务端口，其他类型应用则不需要填写。|
    |**跳板机配置**|    -   **跳板机IP**：输入您创建的ECS实例的**公网IP**地址。
    -   **跳板机账号**：输入用于建立端云互联通道的用户名。
    -   **跳板机密码**：输入用于建立端云互联通道的密码。
**说明：** 您可以直接输入您用于建立端云互联通道的ECS实例的用户名和密码，也可以在这里输入新的用户名和密码，然后通过单击**初始化账号...**增加新用户及密码。 |
    |**初始化账号...**|    -   如果您输入的是ECS实例的root用户名和密码，则会使用此root账号进行配置。如果成功则会出现**配置已添加成功**的提示弹窗。
    -   如果使用新账号或其他非root账号进行互联，那么需要root权限对此账号进行代理配置，在Add SSH Rule对话框中输入Password，然后单击**Add**即可。

**说明：**

        -   此处使用ECS实例的密码只是用来创建一个网络代理，不会将ECS实例的用户名和密码用于其他用途。
        -   推荐您使用新账号或其他非root账号进行互联，后续可将此新账号或非root账号直接共享给其他需要端云互联的团队成员使用，避免泄漏root信息。 |


## 步骤四：启动本地应用进行端云互联

启动本地应用，如果当前状态处于端云互联状态，那么会有如下提示：

![启动本地应用进行端云互联](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1790652061/p66859.png)

并且，在启动应用之后会启动一个etrans的进程：

![启动etrans的进程](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1790652061/p66860.png)

## 更多信息

-   如果您在使用Cloud Toolkit实现端云互联时遇到相关问题，请参见[端云互联问题]()排查解决。
-   如果您想使用IntelliJ IDEA插件快速在SAE上部署应用，详情请参见[通过IntelliJ IDEA插件部署应用](/cn.zh-CN/应用部署/插件部署/通过IntelliJ IDEA插件部署应用.md)。

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![SAE钉钉群2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5885359951/p72048.png)

