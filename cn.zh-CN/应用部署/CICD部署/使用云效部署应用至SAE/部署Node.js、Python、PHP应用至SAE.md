# 部署Node.js、Python、PHP应用至SAE

SAE支持如Node.js、Python、PHP等多种编程语言开发的应用，如果您的Node.js应用、Python应用或者PHP应用等想要部署到SAE，那么您可以使用云效部署。本文介绍如何使用云效部署应用至SAE。

-   [注册阿里云账号](https://help.aliyun.com/document_detail/37195.html)。
-   [将业务代码上传至阿里云Code](https://help.aliyun.com/document_detail/57904.html)。

    **说明：** 业务代码中须包含应用的Dockerfile文件。

-   [将镜像文件上传至阿里镜像库](https://help.aliyun.com/document_detail/60997.html)。
-   [开通云效](https://rdc.aliyun.com)。

## 部署流程

![old_yunxiao_deploy_process_go](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p132388.png)

\[/task/taskbody/section/ol \{"ol"\}\)\[/task/taskbody/section/ol/li \{"li"\}\)如果您的应用已经部署在SAE上，则无需创建新的应用。如果您是第一次部署应用到SAE，则需要在SAE控制台创建应用，以便云效将业务代码推送到该应用中。\(li\]\[/task/taskbody/section/ol/li \{"li"\}\)在SAE创建应用完成后，需要在云效创建对应的应用，应用的部署方式（如JAR、WAR和镜像）两边需要一致。\(li\]\[/task/taskbody/section/ol/li \{"li"\}\)在云效应用创建完成后，可以使用云效提供的流水线模板创建出应用集成发布的基础流水线。\(li\]\[/task/taskbody/section/ol/li \{"li"\}\)基础流水线创建完成，需要更改流水线中的构建任务。例如：如果您在SAE控制台创建的应用采用的是镜像方式，那么在该环节您需要将构建任务中的构建步骤配置为**Docker镜像构建上传**。整个流水线运行后，本环节的构建产物将供部署环节发布使用。\(li\]\[/task/taskbody/section/ol/li \{"li"\}\)构建任务配置完成后，需要指定上一环节（即构建任务环节）构建产物和应用的部署目的地，即应用在SAE上的区域和应用名称。整个流水线运行成功后，应用成功部署到SAE上。\(li\]\(ol\]

## 操作指导

使用云效将Node.js应用、Python应用或者PHP应用等部署到SAE的流程和操作步骤，与使用云效将Java应用、Golang应用部署到SAE相同，详细操作请参见[部署Java应用至SAE](/cn.zh-CN/应用部署/CICD部署/使用云效2020部署应用至SAE/部署Java应用至SAE.md)或者[部署Golang应用至SAE](/cn.zh-CN/应用部署/CICD部署/使用云效2020部署应用至SAE/部署Golang应用至SAE.md)。本文仅描述操作过程中的关键配置。

如果您对云效有一定的了解，那么可以依据部署流程和关键配置内容，将应用部署到SAE。

关键配置：

-   在SAE控制台以镜像方式创建并部署Demo应用。

    ![在SAE以镜像方式创建应用](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p74201.png)

-   在新建流水线时选择相应的编程语言和流水线模板。

    ![在云效使用流水线模板创建基础流水线](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6028827951/p74208.png)

-   在配置构建任务时，将原步骤**构建物上传**删除，新建**Docker镜像构建上传**步骤，然后配置您的镜像信息。

    ![选择Docker镜像构建上传](../images/p73762.png "构建步骤模板选择示意图")

    ![在云效流水线中配置Docker信息](../images/p74217.png "配置镜像信息示意图")

-   在部署任务配置时，将部署任务模板选择**部署到 SAE**，并设置部署信息。

    ![在云效部署环节选择部署SAE模板](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p73766.png)


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

