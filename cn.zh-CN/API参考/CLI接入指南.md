# CLI接入指南

您可以使用[阿里云CLI](https://help.aliyun.com/product/29991.html)接入SAE的API，完成日常的管理操作。

## 安装CLI

安装CLI的步骤，请参见以下文档：

-   [在Windows上安装阿里云CLI]()
-   [在Linux上安装阿里云CLI]()
-   [在macOS上安装阿里云CLI]()

## 配置CLI

配置CLI的步骤，请参见[简介]()。

## 使用CLI调用API

CLI的基本使用方法，请参见[调用RPC API和RESTful API]()。在使用SAE前，您还需要了解SAE的[API概览](/cn.zh-CN/API参考/API概览.md)及各API的请求参数、返回参数等信息。

**说明：** 对于API中不同类型的字段，请遵循阿里云CLI的参数格式要求。更多信息，请参见[参数格式说明]()。

下面以几个样例说明如何使用CLI调用API。

-   创建应用

    ```
    aliyun sae CreateApplication --AppName test --NamespaceId cn-shenzhen --PackageType=Image --Replicas=2 --ImageUrl=registry-vpc.cn-shenzhen.aliyuncs.com/sae-demo-image/consumer:1.0 --Cpu 1000 --Memory 2048 --Deploy=true
    ```

-   查询应用列表

    ```
    aliyun sae ListApplications --region cn-beijing
    ```


## 使用建议

当您需要使用CLI调用API完成相对复杂的任务时，建议将CLI整理成Shell脚本，然后执行，可以提高效率。

## 更多信息

[OpenAPI Explorer](https://api.aliyun.com/?spm=a2c4g.11186623.2.26.431ce517xwquq1#/?product=Edas)

