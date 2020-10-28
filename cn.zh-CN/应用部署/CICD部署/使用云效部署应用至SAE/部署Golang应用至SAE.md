# 部署Golang应用至SAE

本文以Golang应用为例，指导您如何使用云效将应用以镜像的方式部署至SAE。

-   [注册阿里云账号](https://help.aliyun.com/document_detail/37195.html)
-   [将业务代码上传至阿里云Code](https://help.aliyun.com/document_detail/57904.html)

    **说明：** 业务代码中须包含应用的Dockerfile文件。

-   [将镜像文件上传至阿里镜像库](https://help.aliyun.com/document_detail/60997.html)
-   [开通云效](https://rdc.aliyun.com)

## 部署流程

![old_yunxiao_deploy_process_go](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p132388.png)

1.  如果您的应用已经部署在SAE上，则无需创建新的应用。如果您是第一次部署应用到SAE，则需要在SAE控制台创建应用，以便云效将业务代码推送到该应用中。
2.  在SAE创建应用完成后，需要在云效创建对应的应用，应用的部署方式（如JAR、WAR和镜像）两边需要一致。
3.  在云效应用创建完成后，可以使用云效提供的流水线模板创建应用集成发布的基础流水线。
4.  基础流水线创建完成，需要更改流水线中的构建任务。例如：如果您在SAE控制台创建的应用采用的是镜像方式，那么在该环节您需要将构建任务中的构建步骤配置为**Docker镜像构建上传**。整个流水线运行后，本环节的构建产物将供部署环节发布使用。
5.  构建任务配置完成后，需要指定上一环节（即构建任务环节）构建产物和应用的部署目的地，即应用在SAE上的区域和应用名称。整个流水线运行成功后，应用成功部署到SAE上。

## 步骤一：在SAE上创建应用

如果您第一次使用SAE托管应用，需要预先在SAE上使用Demo应用创建相应的应用。

本文以镜像部署为例，具体操作请参见[在SAE控制台使用镜像部署PHP应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用镜像部署PHP应用.md)。

**说明：** 在SAE控制台创建应用时使用的部署方式（JAR、WAR和镜像），必须与在云效的流水线设置保持一致。简而言之，在SAE上使用镜像方式部署，在云效设置流水线时，构建环节必须是镜像相关配置。

![在SAE以镜像方式创建应用](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p74201.png)

## 步骤二：在云效配置应用基本信息

1.  登录[云效控制台应用列表页面](https://rdc.aliyun.com/appcenter/overview)。

2.  在菜单栏中选择**项目** \> **项目列表**，并在**项目列表**页面单击右上角的**新建项目**，然后在弹出的页面中设置项目信息并单击**确定**。

    项目信息有**项目类型**、**项目名称**、**公开性**和**项目背景**等，请依据实际情况设置。

    ![在云效创建项目](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p73719.png)

3.  在菜单栏中选择**研发** \> **应用**，并在**我的应用**页面中，单击左上角的**创建新应用**，然后在**创建新应用**对话框设置应用基本信息并单击**创建**。

    ![在云效创建应用](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p74205.png)


## 步骤三：在云效使用模板构建基础流水线

1.  在菜单栏中选择**研发** \> **流水线**，在**流水线**页面单击右上角的**新建流水线**。

2.  在**新建流水线**页面设置**编程语言**和**流程模板**，并单击**下一步**。

    ![在云效使用流水线模板创建基础流水线](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p74208.png)

    -   **编程语言**：选择**Go**。
    -   **模板**：选择**Go 测试、构建、部署到主机**。
    **说明：** 如果您的应用编程语言非Go，请根据实际情况选择。

3.  在弹出的流水线配置页面中，进行代码库设置，并单击**下一步**。

    ![在云效配置业务代码阿里云code](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74210.png)

    -   代码库类型：选择**阿里云Code**。
    -   **代码仓库**：选择您的代码仓库地址。
    -   **分支**：选择代码分支。
    -   **别名**：代码的别名，后续用于执行组件代码克隆路径，使用数字、字母或下划线。
4.  在弹出的流水线配置页面中，设置流水线的基本信息如流水线名称、管理员等，并单击**创建**。

    ![在云效使用流水线创建基线](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74212.png)


## 步骤四：在云效中配置构建任务

1.  配置构建任务的基本信息。

    1.  在**编辑流水线**页面单击**构建测试**。

    2.  在弹出的**阶段：构建**面板中设置**阶段名称**和**流转配置**。

        ![在云效修改流水线-构建任务01](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74213.png)

2.  配置构建任务的执行步骤。

    1.  单击**任务列表**中具体任务，在**任务：Go构建Docker**页面删除**构建上传**模块，单击**添加步骤**。

        **说明：** 本文以镜像为例，原模板中构建配置不适合镜像方式，需要将其删除并改为镜像配置。

        删除原模板中**构建物上传**如下图所示。

        ![在云效基础流水线中删除不适用构建物设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74214.png)

    2.  在弹出框中选择**Docker镜像构建上传**。

        ![选择Docker镜像构建上传](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p73762.png)

    3.  在**Docker镜像构建上传**步骤区域，设置镜像信息。

        ![在云效流水线中配置Docker信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74217.png)

        -   **步骤名称**：保持默认，也可以自定义。
        -   **区域**：Docker镜像文件所在的地域。
        -   **仓库**：Docker镜像文件所在地址。
        -   **标签**：Docker镜像Tag，支持固定参数例如1.0，或者动态参数$\{DATETIME\}。
        -   **Dockerfile路径**：Dockerfile相对于代码库根目录所在路径，如META/config/Dockerfile或Dockerfile。该文件云效会自动为您创建，无需自建。
        -   **ContextPath**：填写相对于代码根目录的路径，如target，如果不填则为Dockerfile文件所在目录。
        -   **组件出参**：为本构建环节产生的结果文件，供部署环节使用。

## 步骤五：在云效部署应用至SAE

步骤一所创建应用不包含您的任何业务代码，在本环节将应用代码推送至SAE上。即将SAE上的应用升级为含有您业务代码的应用。

1.  在**编辑流水线**页面的**阶段**区域中，删除原流水线的**部署**任务，然后单击添加![添加](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2157559951/p74261.png)。

    ![在云效使用流水线创建基线](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74212.png)

2.  在弹出的**阶段模板**面板中选择**部署到SAE**。

    ![在云效部署环节选择部署SAE模板](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p73766.png)

3.  单击新增的流水线任务，并设置基本信息，设置完成后单击**部署到SAE**。

    ![在云效设置部署配置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74220.png)

4.  在**任务：部署到SAE**面板中设置部署任务信息。

    ![在云效设置部署SAE信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p74221.png)

    -   **区域**：选择步骤一中所创建的应用所在区域。
    -   **SAE应用**：选择步骤一中所创建应用的应用名称。
    -   **构建产物**：为步骤四中**组件出参**产生的结果。
5.  单击右上角的**运行**。

    云效开始依据配置的流水线将应用部署至SAE。

    ![在云效部署SAE应用成功](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8028827951/p74222.png)


## 步骤六：结果验证

-   方法一

    云效显示部署成功后，在SAE控制台查看应用的变更记录，是否产生应用重新部署的变更记录。

    ![在SAE变更也验证是否部署成功](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8028827951/p74223.png)

-   方法二

    云效显示部署成功后，在SAE控制台查看应用的基本信息，查看镜像地址是否与在云效中设置相同。

    ![在基本信息也验证云效部署SAE是否成功](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8028827951/p74224.png)


## 常见问题

-   其他编程语言怎么使用云效将应用部署到SAE？

    在流水线构建任务环节，您可以选择所需的编程语言模板。具体部署配置操作请参见[云效快速入门](https://help.aliyun.com/document_detail/52223.html)。

    ![云效支持的编程语言](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5694688951/p73774.png)

-   除Golang应用外其他编程语言的应用想要部署在SAE上，在SAE创建应用时使用哪种部署方式（JAR、WAR和镜像）？

    使用镜像方式。使用云效部署时，切记您应用程序代码中须包含应用的Dockerfile文件。


## 更多信息

-   您在SAE部署完应用后，可以对应用进行更新、扩缩容、启停、删除应用等生命周期管理操作，具体操作方式请参见[管理应用生命周期](/cn.zh-CN/应用管理/管理应用生命周期.md)。
-   您在SAE部署完应用后，可以对应用进行自动弹性伸缩、SLB绑定和批量启停等提升应用性能的操作，具体操作方式请参见以下文档：
    -   [绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)
    -   [配置弹性伸缩策略](/cn.zh-CN/应用管理/配置弹性伸缩策略.md)
    -   [一键启停应用](/cn.zh-CN/应用管理/一键启停应用.md)
    -   [配置管理](/cn.zh-CN/应用管理/配置管理/配置管理概述.md)
    -   [变更实例规格](/cn.zh-CN/应用管理/变更实例规格.md)
-   您在SAE部署完应用后，还可以对应用进行日志管理、监控管理、应用事件查看和变更记录查看等聚焦应用运行状态的操作，具体操作方式请参见以下文档：
    -   [日志管理](/cn.zh-CN/日志管理/查看实时日志.md)
    -   [监控管理](/cn.zh-CN/监控管理/基础监控.md)
    -   [应用事件查看](/cn.zh-CN/应用管理/查看应用事件.md)
    -   [变更记录查看](/cn.zh-CN/应用管理/查看变更记录.md)
    -   [使用Webshell诊断应用](/cn.zh-CN/应用管理/使用 Webshell 诊断应用.md)

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![SAE钉钉群2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9515823061/p72048.png)

