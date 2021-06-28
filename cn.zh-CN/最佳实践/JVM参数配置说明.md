# JVM参数配置说明

本文列出了JVM启动参数相关信息。

## 调优栈内存

|配置参数|说明|示例|
|----|--|--|
|`-Xmx`|设置最大堆大小|`-Xmx3550m`，设置JVM最大可用内存为3550 MB。|
|`-Xms`|设置JVM初始内存|`-Xms3550m`，设置JVM初始内存为3550 MB。此值建议与`-Xmx`相同，避免每次垃圾回收完成后JVM重新分配内存。|
|`-Xmn2g`|设置年轻代大小|`-Xmn2g`，设置年轻代大小为2 GB。整个JVM内存大小=年轻代大小+年老代大小+持久代大小。持久代一般固定大小为64 MB，所以增大年轻代后，将会减小年老代大小。此值对系统性能影响较大，Sun官方推荐配置为整个堆的3/8。|
|`-Xss`|设置线程的堆栈大小|`-Xss128k`，设置每个线程的堆栈大小为128 KB。 **说明：** JDK5.0版本以后每个线程堆栈大小为1 MB，JDK5.0以前版本每个线程堆栈大小为256 KB。请依据应用的线程所需内存大小进行调整。在相同物理内存下，减小该值可以生成更多的线程。但是操作系统对一个进程内的线程个数有一定的限制，无法无限生成，一般在3000个~5000个左右。 |
|`-XX:NewRatio=n`|设置年轻代和年老代的比值。|`-XX:NewRatio=4`，设置年轻代（包括Eden和两个Survivor区）与年老代的比值（除去持久代）。如果设置为4，那么年轻代与年老代所占比值为1:4，年轻代占整个堆栈的1/5。|
|`-XX:SurvivorRatio=n`|年轻代中Eden区与两个Survivor区的比值。|`-XX:SurvivorRatio=4`，设置年轻代中Eden区与Survivor区的大小比值。如果设置为4，那么两个Survivor区与一个Eden区的比值为2:4，一个Survivor区占整个年轻代的1/6。|
|`-XX:MaxPermSize=n`|设置持久代大小|`-XX:MaxPermSize=16m`，设置持久代大小为16 MB。|
|`-XX:MaxTenuringThreshold=n`|设置垃圾最大年龄|`-XX:MaxTenuringThreshold=0`，设置垃圾最大年龄。 -   如果设置为0，那么年轻代对象不经过Survivor区，直接进入年老代。对于年老代比较多的应用，提高了效率。
-   如果将此值设置为较大值，那么年轻代对象会在Survivor区进行多次复制，增加了对象在年轻代的存活时间，增加在年轻代即被回收的概率。 |

## 调优回收器GC

|配置参数|说明|示例|
|----|--|--|
|`-XX:+UseParallelGC`|选择垃圾收集器为并行收集器。|`-Xmx3800m -Xms3800m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:ParallelGCThreads=20`，`-XX:+UseParallelGC`此配置仅对年轻代有效，即在示例配置下，年轻代使用并发收集，而年老代仍旧使用串行收集。|
|`-XX:ParallelGCThreads`|配置并行收集器的线程数，即同时多少个线程一起进行垃圾回收。 **说明：** 此值建议配置与处理器数目相等。

|`-Xmx3800m -Xms3800m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:ParallelGCThreads=20`，`-XX:ParallelGCThreads=20`表示配置并行收集器的线程数为20个。|
|`-XX:+UseParallelOldGC`|配置年老代垃圾收集方式为并行收集。 **说明：** JDK6.0支持对年老代并行收集。

|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:ParallelGCThreads=20 -XX:+UseParallelOldGC`，`-XX:+UseParallelOldGC`表示对年老代进行并行收集。|
|`-XX:MaxGCPauseMillis`|设置每次年轻代垃圾回收的最长时间，如果无法满足此时间，JVM会自动调整年轻代大小，以满足此值。|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:MaxGCPauseMillis=100`，`-XX:MaxGCPauseMillis=100`设置每次年轻代垃圾回收的最长时间为100 ms。|
|`-XX:+UseAdaptiveSizePolicy`|设置此选项后，并行收集器自动选择年轻代区大小和相应的Survivor区比例，以达到目标系统规定的最低响应时该间或者收集频率，该值建议使用并行收集器时，并且一直打开。|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:+UseParallelGC -XX:MaxGCPauseMillis=100 -XX:+UseAdaptiveSizePolicy`|

|配置参数|说明|示例|
|----|--|--|
|`-XX:+UseConcMarkSweepGC`|设置年老代为并发收集。 **说明：** 配置了`-XX:+UseConcMarkSweepGC`，建议年轻代大小使用`-Xmn`设置。

|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:ParallelGCThreads=20 -XX:+UseConcMarkSweepGC -XX:+UseParNewGC`|
|`-XX:+UseParNewGC`|设置年轻代为并行收集。 可与CMS收集同时使用。JDK5.0以上版本，JVM根据系统配置自行设置，无需再设置此值。

|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:ParallelGCThreads=20 -XX:+UseConcMarkSweepGC -XX:+UseParNewGC`|
|`-XX:CMSFullGCsBeforeCompaction`|由于并发收集器不对内存空间进行压缩、整理，所以运行一段时间以后会产生“碎片”，使得运行效率降低。此值设置运行多少次GC以后对内存空间进行压缩、整理。|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:+UseConcMarkSweepGC -XX:CMSFullGCsBeforeCompaction=5 -XX:+UseCMSCompactAtFullCollection`，`-XX:CMSFullGCsBeforeCompaction=5`，表示运行GC5次后对内存空间进行压缩、整理。|
|`-XX:+UseCMSCompactAtFullCollection`|打开对年老代的压缩。 **说明：** 该值可能会影响性能，但是可以消除碎片。

|`-Xmx3550m -Xms3550m -Xmn2g -Xss128k -XX:+UseConcMarkSweepGC -XX:CMSFullGCsBeforeCompaction=5 -XX:+UseCMSCompactAtFullCollection`|

|配置参数|说明|
|----|--|
|`-XX:+PrintGC`|用于输出GC日志。|
|`-XX:+PrintGCDetails`|用于输出GC日志。|
|``-XX:+PrintGCTimeStamps``|用于输出GC时间戳（基准时间形式）。|
|`-XX:+PrintGCDateStamps`|用于输出GC的时间戳（日期形式，例如2019-12-24T21:53:59.234+0800）。|
|`-XX:+PrintHeapAtGC`|在进行GC前后打印出堆的信息。|
|`-Xloggc:../logs/gc.log`|日志文件的输出路径。|

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索钉钉群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1176199061/p72048.png)

