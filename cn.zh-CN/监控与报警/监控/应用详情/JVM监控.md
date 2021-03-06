# JVM监控

JVM监控功能用于监控重要的JVM指标，包括堆内存指标、非堆内存指标、直接缓冲区指标、内存映射缓冲区指标、GC（Garbage Collection）累计详情和JVM线程数等。本文介绍JVM监控功能和查看JVM监控指标的操作步骤。

## 功能入口

1.  在左侧导航栏中单击**应用列表**，在顶部菜单栏选择地域并在页面上方选择微服务空间，然后在**应用列表**页面单击具体的应用名称。

2.  在应用列表中单击您想查看的应用。

3.  在左侧导航栏单击**应用详情**。

4.  在**应用详情**页面选择您想查看的实例，并在页面右侧单击**JVM监控**页签。

    ![JVM监控-PaaS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0402026061/p184824.png)


## 查看JVM监控指标

**JVM监控**页签内展示了GC瞬时次数、GC瞬时耗时、堆内存详情、元空间详情、非堆内存、直接缓冲区和JVM线程数的时序曲线。

-   单击**GC瞬时次数/每分钟**和**GC瞬时耗时/每分钟**面板右上角的**瞬时值**和**累计值**按钮，可以切换查看GC瞬时次数和GC瞬时耗时的时序曲线。
-   单击各监控面板上的指标名称（例如FullGC次数），可打开或关闭该指标在图表中的可见性。

    **说明：** 每个图表必须至少有一个指标设为可见，这意味着当图表中只有一个指标时，您无法关闭该指标的可见性。

-   单击**堆内存详情/每分钟**、**元空间详情/每分钟**、**非堆内存/每分钟**、**直接缓冲区/每分钟**和**JVM线程数/每分钟**的右上角的查看API按钮，可看该监控指标的API详情。

## 功能介绍

JVM监控功能可监控以下指标：

-   GC（垃圾收集）瞬时和累计详情
    -   FullGC次数
    -   YoungGC次数
    -   FullGC耗时
    -   YoungGC耗时
-   堆内存详情
    -   堆内存总和
    -   堆内存老年代字节数
    -   堆内存年轻代Survivor区字节数
    -   堆内存年轻代Eden区字节数
-   非堆内存
    -   非堆内存提交字节数
    -   非堆内存初始字节数
    -   非堆内存最大字节数
-   元空间

    元空间字节数

-   直接缓冲区
    -   DirectBuffer总大小（字节）
    -   DirectBuffer使用大小（字节）
-   JVM线程数
    -   线程总数量
    -   死锁线程数量
    -   新建线程数量
    -   阻塞线程数量
    -   可运行线程数量
    -   终结线程数量
    -   限时等待线程数量
    -   等待中线程数量

