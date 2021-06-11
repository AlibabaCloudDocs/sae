# SAE弹性伸缩最佳实践

SAE弹性伸缩可以实现在瞬时流量波峰到来时应用自动扩容，波峰结束后自动缩容，保障应用平稳运行，具有高可靠性、免运维、低成本的特点。本文介绍通过SAE部署弹性伸缩策略的最佳实践。

## 弹性伸缩准备

-   配置应用健康检查：确保应用在弹性伸缩过程中的整体可用性，仅在启动、运行并且准备完成时才接收流量。具体操作，请参见[设置健康检查](/cn.zh-CN/应用部署/设置健康检查.md)。
-   配置应用生命周期管理：确保缩容时按照预期优雅下线您的应用，配置**停止前处理（PreStop设置）**。具体操作，请参见[设置应用生命周期管理](/cn.zh-CN/应用部署/设置应用生命周期管理.md)。
-   采用指数重试机制：为避免因弹性不及时、应用启动不及时或应用没有优雅上下线导致服务调用异常，采用Java指数重试机制进行服务调用。
-   优化应用启动速度。
    -   软件包优化：优化应用启动时间，降低因类加载、缓存等外部因素对应用启动时长造成的影响。
    -   镜像优化：精简镜像大小，减少创建实例时镜像拉取耗时，可以有的放矢地借助[开源工具](https://github.com/wagoodman/dive)分析并精简镜像层信息。
    -   Java应用启动优化：在SAE上创建应用时，选择Dragonwell 11环境能够开启应用加速功能。具体操作，请参见[设置Java应用的启动加速](/cn.zh-CN/最佳实践/应用加速/设置Java应用的启动加速.md)。

## 弹性规则配置

SAE支持基础监控、应用监控多指标组合配置，您可以根据当前应用的属性（CPU敏感、内存敏感或IO敏感）灵活配置。

您可以通过查看**基础监控**和**应用监控**对应指标的历史数据（ 例如过去6小时、12小时、1天或7天峰值，P95或P99数值）并预估指标目标值，借助[PTS](https://pts.console.aliyun.com/)等压测工具进行压测，了解应用可以应对的并发请求数量、需要的CPU和内存数量，以及高负载状态下的应用响应方式，以评估应用容量峰值大小。

在配置弹性伸缩策略时，您需要考虑以下因素：

-   权衡可用性与成本，配置指标目标值。示例如下：
    -   可用性优化策略：配置指标值为40%。
    -   可用性成本平衡策略：配置指标值为50%。
    -   成本优化策略：配置指标值为70%。
-   考虑梳理上下游、中间件和DB等相关依赖性，并配置对应的弹性规则或限流降级手段，以确保扩容时全链路的可用性。

弹性规则配置完成后，您可以通过监控并调整弹性规则使容量接近应用实际负载。关于查看监控的具体步骤，请参见[基础监控](/cn.zh-CN/监控与报警/监控/基础监控.md)。

Java应用运行时优化是通过释放物理内存，增强内存指标与业务关联性。借助Dragonwell运行时的环境，通过增加JVM参数开启ElasticHeap能力，支持Java堆内存的动态弹性伸缩，从而节约了Java应用在运行时实际使用的物理内存。关于ElasticHeap的更多信息，请参见[G1ElasticHeap](https://github.com/alibaba/dragonwell8/wiki/Alibaba-Dragonwell8-User-Guide#g1elasticheap)。

推荐配置为Dragonwell+ElasticHeap Periodic uncommit模式 （自动模式）。具体操作，请参见[操作步骤](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用JAR文件部署微服务应用.md)和[设置启动命令](/cn.zh-CN/应用部署/设置启动命令.md)。

-   Java环境：Dragonwell

    ![配置Jar包](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7417323261/p282566.png)

-   JVM参数：`-XX:+ElasticHeapPeriodicUncommit`

    ![启动参数](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7417323261/p282356.png)


**说明：** 不适用配置内存指标的应用类型：采用动态内存管理进行内存分配（例如Java JVM内存管理、Glibc Malloc和Free操作）的部分应用，没有及时向操作系统释放其闲置内存，导致无法实时减少实例消耗的物理内存和新增实例消耗的平均内存，进而导致无法触发缩容。

-   最小实例数配置

    确认最小实例数≥2，配置多可用区vSwitch。避免因底层节点异常导致实例驱逐或可用区无可用实例，应用停止工作。

-   最大实例数配置

    确认最大实例数≤可用区IP数。避免因配置的IP数超出限制，应用无法新增实例。


您可以在**基本信息**页面的**应用信息**区域查看当前应用的可用IP数，如果可用IP较少，请替换或新增vSwitch。具体操作，请参见[验证弹性伸缩策略](/cn.zh-CN/应用管理/应用实例/配置弹性伸缩策略.md)。

![应用信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4352223261/p282235.png)

## 弹性伸缩过程

您可以在应用**概览页**页面查看当前开启弹性伸缩配置的应用，并监控当前实例数已经到达峰值的应用，对其弹性伸缩配置重新进行评估。

![弹性生效的应用](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4352223261/p282238.png)

**说明：** 如果单个应用需要弹出超过50个实例，需提交[工单](https://workorder.console.aliyun.com/#/ticket/createIndex)申请白名单。

您可以在应用**基本信息**页面的实例列表中查看实例所属可用区。弹性伸缩触发缩容后，可能会导致可用区分配不均。如果可用区不均衡，您可以通过**重启**实例实现再均衡。

![vSwitch](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1537323261/p282239.png)

进行部署应用等变更单操作时，SAE会停止当前应用的弹性伸缩配置，避免两种操作冲突。如果您希望变更单完成后能够恢复弹性配置，可以在**部署应用**页面选择**系统自动恢复**。

![恢复自动弹性方式](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3119823261/p281870.png)

## 弹性伸缩观测

您可以在**应用事件**页面观测SAE弹性生效行为，包括查看弹性伸缩时间和动作，以此来衡量弹性伸缩策略的有效性并按需调整。

![应用事件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4352223261/p282244.png)

