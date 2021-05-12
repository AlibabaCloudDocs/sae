# JVM -D启动配置参数

本文介绍HSF应用开发时JVM -D启动参数的配置信息。

## -D`hsf.server.port`

指定HSF的启动服务绑定端口，默认值为`12200`。如果在本地启动多个HSF Provider，则需要修改此端口。

## -D`hsf.server.max.poolsize`

指定HSF的服务端最大线程池大小，默认值为`720`。

## -D`hsf.server.min.poolsize`

指定HSF的服务端最小线程池大小，默认值为`50`。

## -D`hsf.client.localcall`

打开或者关闭本地优先调用，默认值为`true`。

## -D`pandora.qos.port`

指定Pandora监控端口，默认值为`12201`。如果在本地启动多个HSF Provider，则需要修改此端口。

## -D`hsf.http.enable`

是否开启HTTP端口，默认值为`true`。

## -D`hsf.http.port`

指定HSF暴露的HTTP接口，默认值为`12220`。如果在本地启动多个HSF Provider，则需要修改此端口。

## -D`hsf.run.mode`

指定HSF客户端是否指定target进行调用，即绕开ConfigServer。值为`1`，表示不允许指定target调用；值为`0`，表示允许指定target调用。默认值为`1`时，不推荐指定为`0`。

## -D`hsf.shuthook.wait`

HSF优雅关闭的等待时间，默认值为`10000`，单位：毫秒。

## -D`hsf.publish.delayed`

是否所有的服务都需要延迟发布，默认值为`false`，不需要延迟发布 。

## -D`hsf.server.ip`

指定需要绑定的IP地址。在多网卡情况下默认绑定第一个网卡，通过该参数指定需要绑定的IP地址。

## -D`HsfBindHost`

指定需要绑定的Host。在多网卡情况下默认绑定和上报给地址注册中心第一个网卡的IP地址，通过该参数可以指定需要绑定的Host，列如`-DHsfBindHost=0.0.0.0`将HSF Server端口绑定本机所有网卡。

## -D`hsf.publish.interval=400`

指定发布服务之间的时间间隔。HSF服务发布时会瞬间暴露出去，在应用启动时如果承受不住压力，可以配置该参数。默认值为`400`，单位：毫秒。

## -D`hsf.client.low.water.mark=32`-D`hsf.client.high.water.mark=64`-D`hsf.server.low.water.mark=32`-D`hsf.server.high.water.mark=64`

指定客户端或者服务端的每个channel写缓冲的限制。

-   客户端每个channel的写缓冲的限制，单位：KB，一旦超过高水位，channel禁写，新的请求放弃写出，直接报错。禁写之后，等到缓冲区低于低水位才能恢复。
-   服务端每个channel的写缓冲的限制，单位：KB，超过高水位时，新的响应放弃写出，客户端收不到响应会超时。缓冲区低于低水位时才能恢复写。
-   高低水位需成对设置，并且需要高水位大于低水位。

## -D`hsf.generic.remove.class=true`

获取泛化调用的结果，但不输出`class`字段信息。

## -D`defaultHsfClientTimeout`

全局的客户端超时配置。

## -D`hsf.invocation.timeout.sensitive`

`hsf.invocation.timeout.sensitive`默认值为`false`，决定HSF调用时间是否包含创建连接、选址等耗时逻辑。

