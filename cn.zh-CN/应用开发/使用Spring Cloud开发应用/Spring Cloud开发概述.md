# Spring Cloud开发概述

SAE支持原生Spring Cloud微服务框架，在该框架下开发的应用只需添加服务依赖和修改注册中心配置，便可获取SAE企业级的应用托管、应用治理、监控报警和应用诊断等能力，实现零代码工作量的应用迁移。

## 为什么使用Spring Cloud

Spring Cloud提供了简化应用开发的一系列标准和规范。该标准和规范包含服务发现、负载均衡、熔断、配置管理、消息事件驱动、消息总线等，同时Spring Cloud在该规范的基础上，提供了服务网关、全链路跟踪、安全、分布式任务调度和分布式任务协调等功能的实现机制。

目前业界流行的Spring Cloud具体实现有Spring Cloud Netflix、Spring Cloud Consul、Spring Cloud Gateway、Spring Cloud Sleuth和Spring Cloud Alibaba等。

如果您已经使用Spring Cloud Netflix、Spring Cloud Consul等Spring Cloud组件开发应用，该应用可以直接部署到SAE上，获得应用托管能力。不需要修改任何代码，便可直接使用SAE所提供的高级监控功能，以及实现全链路跟踪、监控报警和应用诊断等监控功能。

如果您的Spring Cloud应用还想使用SAE中更多的服务治理相关功能，那么需要将您的Spring Cloud组件替换为Spring Cloud Alibaba中的组件或增加Spring Cloud Alibaba组件。

## 兼容性说明

SAE目前支持Spring Cloud Greenwich、Spring Cloud Finchley和Spring Cloud Edgware三个版本。Spring Cloud、Spring Boot和Spring Cloud Alibaba及各组件的版本对应关系请参见[版本配套关系说明](#section_2vw_cs7_oqi)。

Spring Cloud功能、开源实现及SAE兼容性如下表所示。

|Spring Cloud功能|开源实现|SAE兼容性|
|--------------|----|------|
|通用功能|服务注册与发现|-   Netflix Eureka
-   Consul Discovery

|兼容且提供替换组件|
|负载均衡|Netflix Ribbon|兼容|
|服务调用|-   Feign
-   RestTemplate

|兼容|
|配置管理|-   Config Server
-   Consul Config

|兼容且提供替换组件|
|服务网关|-   Spring Cloud Gateway
-   Netflix Zuul

|兼容|
|链路跟踪|Spring Cloud Sleuth|兼容且提供替换组件|
|消息驱动Spring Cloud Stream|-   RabbitMQ binder
-   Kafka binder

|兼容且提供替换组件|
|消息总线Spring Cloud Bus|-   RabbitMQ
-   Kafka

|兼容且提供替换组件|
|安全|Spring Cloud Security|兼容|
|分布式任务调度|Spring Cloud Task|兼容|
|分布式协调|Spring Cloud Cluster|兼容|

## 版本配套关系说明

Spring Cloud、Spring Boot和Spring Cloud Alibaba及SAE提供的正式商用组件的版本配套关系如下表所示。

|Spring Cloud|Spring Boot|Spring Cloud Alibaba|
|------------|-----------|--------------------|
|ANS|ACM|SchedulerX|
|Greenwich|2.1.x|2.1.1.RELEASE|
|Finchley|2.0.x|2.0.1.RELEASE|
|Edgware|1.5.x|1.5.1.RELEASE|

**说明：** Spring Cloud Alibaba Nacos Discovery和Spring Cloud Alibaba Nacos Config分别是ANS和ACM对应的开源组件。

