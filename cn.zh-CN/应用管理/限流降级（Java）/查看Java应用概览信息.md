# 查看Java应用概览信息

开启限流降级后，SAE将通过AHAS监控各应用、接口、机器的实时数据，从而评估系统的整体表现，并为流控降级规则提供重要依据。本文介绍查看Java应用限流降级概览信息的操作步骤。

请确保您的Java应用已开启限流降级功能，详情请参见[设置限流降级]()。

## 操作步骤

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击具体应用名称。

3.  在左侧导航栏中选择**限流降级（Java）** \> **应用概览**。

4.  在**应用概览**页面，查看应用信息。

    -   限流指标详情：统计了近5分钟应用接口的通过QPS、流控QPS、异常QPS、响应时间、系统负载情况以及防护事件。

        **说明：** **应用概览**页面涉及到的QPS、响应时间、并发线程均为应用入口接口的统计，不包括应用内部方法调用的统计。

        ![限流指标](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1833858951/p111855.png)

        -   单击**QPS统计**、**响应时间**、**系统负载**的![箭头](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1833858951/p134465.png)图标，可以查看各个指标更详细的历史数据。
        -   单击**防护事件**的![箭头](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1833858951/p134465.png)图标，可以进入**事件中心**页面，查看防护事件的详细信息，包括级别、类型、起始时间等。单击目标事件**操作**列的**查看详情**，可以查看该接口的历史监控数据。
    -   QPS热力图：包括通过QPS热力图、流控QPS热力图、异常QPS热力图等。

        ![QPS热力图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1833858951/p111854.png)

        -   鼠标悬浮在热力图的图标中，可以查看各指标TOP节点的设备ID等相关信息；单击热力图中的图标，可查看各指标的历史数据。
        -   单击右侧的**图表**或**表格**，可以选择以不同的形式展现TOP节点的信息。
        -   单击右侧的**查看全部**，进入**机器监控**页面，查看各节点的QPS、CPU、Load等详细信息。
    -   TOP接口列表会动态刷新，按通过QPS由大到小排列接口。

        ![top列表](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1833858951/p111853.png)

        -   单击目标资源**操作**列的**流控**、**隔离**或**降级**，可为该资源配置相应规则，详情请参见以下文档：
            -   [配置流控规则]()
            -   [配置降级规则]()
            -   [配置隔离规则]()
        -   单击接口名称进入**接口详情**页面，可以查看该接口的详细信息。

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![SAE钉钉群2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5885359951/p72048.png)

