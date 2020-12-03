# 使用Jenkins创建Java应用的持续集成

本文介绍使用Jenkins构建SAE Java应用的持续集成。

在开始持续集成之前，您需要完成以下准备工作：

-   获取阿里云的AccessKey ID和AccessKey Secret。具体操作，请参见[创建AccessKey]()。
-   在[SAE控制台](https://sae.console.aliyun.com)中创建一个可以部署的应用。具体步骤，请参见[在SAE控制台使用WAR包部署Java Web应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用WAR包部署Java Web应用.md)。
-   使用GitLab托管您的代码。您可以自行搭建GitLab或者使用[阿里云Code](https://code.aliyun.com/)。

    本文使用通过自行搭建的GitLab做演示，更多信息，请参见[GitLab](https://about.gitlab.com/)。

-   安装Maven。具体操作，请参见[Maven](http://maven.apache.org/download.cgi)。
-   安装Jenkins。具体操作，请参见[Jenkins官网](https://jenkins.io/)。

您可以使用Jenkins构建SAE应用的持续集成方案。本文适用于对以下语言或工具有一定了解的开发人员。

|工具|说明|
|--|--|
|Maven|[Maven](https://maven.apache.org/)是一个项目管理和构建的自动化工具。|
|Jenkins|[Jenkins](https://jenkins.io/)是一个可扩展的持续集成引擎。|
|GitLab|[GitLab](https://about.gitlab.com/)是一个利用Ruby on Rails开发的开源应用程序，实现一个自托管的Git项目仓库，可通过Web界面进行访问公开的或者私人项目。 它拥有与GitHub类似的功能，能够浏览源代码，管理缺陷和注释。|

## 步骤一：配置项目

修改Maven项目配置，添加toolkit-maven-plugin及部署信息，具体操作，请参见[通过Maven插件自动化部署应用](https://help.aliyun.com/document_detail/110639.html)。

**说明：** 修改项目配置后，建议您在本地使用Maven构建验证配置是否正确。

## 步骤二：配置Jenkins

1.  在Jenkins控制台的菜单栏中选择**Manage Jenkins** \> **Manage Plugins**，安装Git和GitLab插件。

    **说明：**

    -   GIT Client Plugin和GIT Plugin插件可以帮助Jenkins拉取Git仓库中的代码。
    -   Gitlab Hook Plugin插件可以帮助Jenkins在收到Gitlab发来的Hook后触发一次构建任务。
    ![安装和配置 Jenkins](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66447.png)

2.  在Jenkins控制台的菜单栏中选择**Manage Jenkins** \> **Global Tool Configuration**，设置Maven版本名称并配置路径，单击**保存**。

    ![ Jenkins 控制台设置Maven](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66449.png)

3.  在Jenkins服务器上生成SSH RSA密钥对，并将公钥导入GitLab，实现Jenkins拉取GitLab代码时的自动认证。

    1.  在Jenkins服务器生成SSH RSA密钥对。具体信息，请参见[GitLab文档](http://docs.gitlab.com/ce/ssh/README.html)。

        ![EDAS在 Jenkins 服务器运行 Jenkins 软件的用户下，生成 SSH RSA 密钥对](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66453.png)

    2.  进入GitLab首页，在菜单栏选择**Settings** \> **Deploy Keys** ，并单击**New Deploy Key** ，导入在Jenkins服务器上创建的SSH RSA公钥。

        ![EDAS使用Jenkins在gitlab导公钥1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66455.png)


## 步骤三：创建Jenkins任务

1.  在Jenkins首页左侧导航栏中单击**新建Item**，在创建任务界面输入任务名称，并选择**Freestyle project**，单击**确定**，配置任务信息。

    ![EDAS使用Jenkins集成之创建项目](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66460.png)

2.  单击**源码管理**，在**源码管理**页签中选择**Git**，并设置相关参数。

    -   **Repository URL**：您的项目的Git协议地址。
    -   **Credentials**：安全凭证，选择**无**即可。

        **说明：** 请确保您的SSH RSA公匙已添加到该Git项目所在的GitLab中，否则将会报错。

    ![EDAS使用Jenkins集成之源码管理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66461.png)

3.  单击**构建触发器**，在**构建触发器**页签选中**GitHub hook trigger for GITScm polling**。

4.  单击**构建环境**，在**构建环境**页签选中**Add timestamps to the Console Output**，为控制台输出的信息添加时间戳。

5.  单击**构建**，在**构建**页签单击**增加构建步骤**，在下拉列表中选择**Invoke top-level Maven targets**。

6.  在**Invoke top-level Maven targets**区域设置**Maven Version**和**Goals**。如果您想部署多模块工程，请参见[（可选）创建多模块工程的Jenkins任务](#section_isk_faz_uj2)。

    -   **Maven Version**：单击该选项后面的下拉框，选择在**全局工具配置**里配置的**Maven版本名称**。
    -   **Goals**：输入mvn clean package toolkit:deploy -Dtoolkit\_profile=toolkit\_profile.yaml -Dtoolkit\_package=toolkit\_package.yaml -Dtoolkit\_deploy=toolkit\_deploy.yaml （如有其它参数，请根据实际情况输入）。
    ![SAE](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p128282.png)

    **说明：** Maven配置完成后，在[步骤五：提交变更到GitLab](#section_xr3_c84_xgp)步骤中便可通过POP API方式触发应用部署。


## 步骤四：配置GitLab的Web Hook

1.  在Gitlab首页右键单击GitLab工程，然后选择**Setting** \> **Web Hooks**。

2.  在**Web Hooks**页面的**URL**区域中输入`http://jenkins服务器地址:jenkins服务器监听端口/git/notifyCommit?url=本项目的git协议地址`。

    图中表示的Jenkins服务器地址为您的Jenkins服务器的Web访问地址如`192.168.XX.XX:8080`。

    ![配置 Gitlab 的 Web Hook，实现自动构建](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66465.png)

3.  配置完成后，单击**Test Hook**，测试配置结果。

    ![配置 Gitlab 的 Web Hook结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p66467.png)


## 步骤五：提交变更到GitLab

如果上述步骤配置正确，提交后将会触发一次GitLab Hook。Jenkins在接收到该Hook后会构建您的Maven项目，并在构建结束时调用SAE POP API脚本触发部署。

**说明：** 构建的Maven项目中配置了通过SAE POP API方式部署应用的脚本。

提交部署成功输出的日志信息（**Build Number** \> **控制台输出**）。

```
15:58:51 [INFO] Deploy application successfully!
15:58:51 [INFO] ------------------------------------------------------------------------
15:58:51 [INFO] BUILD SUCCESS
15:58:51 [INFO] ------------------------------------------------------------------------
15:58:51 [INFO] Total time: 24.330 s
15:58:51 [INFO] Finished at: 2018-12-25T15:58:51+08:00
15:58:51 [INFO] Final Memory: 23M/443M
15:58:51 [INFO] ------------------------------------------------------------------------
15:58:51 Finished: SUCCESS
            
```

如果部署失败，您可以登录[SAE控制台](https://sae.console.aliyun.com)，查看此次部署任务的执行过程。具体步骤，请参见[查看变更记录](/cn.zh-CN/应用管理/应用变更记录/查看变更记录.md)。

## （可选）创建多模块工程的Jenkins任务

如果您需要创建多模块工程的Jenkins任务，您可以参考以下内容设置。

创建多模块工程的Jenkins任务和[步骤二：配置Jenkins](#section_mb4_l2b_y3q)的第5步基本相同，只需要修改**调用顶层Maven目标**。如果工程为多模块工程，想在Jenkins中部署子模块的话，那么需要在父模块中调用`mvn clean install`命令，然后在子模块中调用`mvn clean package toolkit:deploy -Dtoolkit_profile=toolkit_profile.yaml -Dtoolkit_package=toolkit_package.yaml -Dtoolkit_deploy=toolkit_deploy.yaml`命令。以[Demo工程](http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/edas-app-demo/edas-app-demo.zip)为例，工程结构如下。

```
sh-3.2# tree -L 1 carshop
carshop
├── detail
├── itemcenter
├── itemcenter-api
└── pom.xml            
```

其中，detail、itemcenter、itemcenter-api为子模块，如果您想部署itemcenter模块的话，需要在父工程中设置一个clean install构建目标，然后在itemcenter模块中设置`clean package toolkit:deploy -Dtoolkit_profile=toolkit_profile.yaml -Dtoolkit_package=toolkit_package.yaml -Dtoolkit_deploy=toolkit_deploy.yaml`构建目标。

![SAE](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7411355061/p128286.png)

