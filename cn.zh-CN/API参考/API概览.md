# API概览

SAE应用引擎提供以下相关API接口。

调用OpenSaeService免费开通SAE服务，请参见[OpenSaeService](/cn.zh-CN/API参考/服务开通/OpenSaeService.md)。

## 命名空间和VPC

|API|描述|
|---|--|
|[CreateNamespace](/cn.zh-CN/API参考/命名空间和VPC/CreateNamespace.md)|调用CreateNamespace接口创建命名空间。|
|[DeleteNamespace](/cn.zh-CN/API参考/命名空间和VPC/DeleteNamespace.md)|调用DeleteNamespace接口删除命名空间。|
|[UpdateNamespace](/cn.zh-CN/API参考/命名空间和VPC/UpdateNamespace.md)|调用UpdateNamespace接口更新命名空间信息。|
|[UpdateNamespaceVpc](/cn.zh-CN/API参考/命名空间和VPC/UpdateNamespaceVpc.md)|调用UpdateNamespaceVpc接口更新命名空间绑定的VPC。|
|[DescribeNamespace](/cn.zh-CN/API参考/命名空间和VPC/DescribeNamespace.md)|调用DescribeNamespace接口查询命名空间详细信息。|
|[DescribeNamespaces](/cn.zh-CN/API参考/命名空间和VPC/DescribeNamespaces.md)|调用DescribeNamespaces接口查询命名空间列表。|
|[DescribeNamespaceList](/cn.zh-CN/API参考/命名空间和VPC/DescribeNamespaceList.md)|调用DescribeNamespaceList接口获取命名空间列表。|
|[DescribeNamespaceResources](/cn.zh-CN/API参考/命名空间和VPC/DescribeNamespaceResources.md)|调用DescribeNamespaceResources接口查询命名空间内的资源信息。|
|[ListNamespaceChangeOrders](/cn.zh-CN/API参考/命名空间和VPC/ListNamespaceChangeOrders.md)|调用ListNamespaceChangeOrders接口获取命名空间发布单列表。|
|[CreateIngress](/cn.zh-CN/API参考/命名空间和VPC/CreateIngress.md)|调用CreateIngress接口创建路由规则。|
|[DeleteIngress](/cn.zh-CN/API参考/命名空间和VPC/DeleteIngress.md)|调用DeleteIngress接口删除Ingress实例。|
|[UpdateIngress](/cn.zh-CN/API参考/命名空间和VPC/UpdateIngress.md)|调用UpdateIngress接口更新Ingress实例配置。|
|[DescribeIngress](/cn.zh-CN/API参考/命名空间和VPC/DescribeIngress.md)|调用DescribeIngress接口查询Ingress配置详情。|
|[ListIngresses](/cn.zh-CN/API参考/命名空间和VPC/ListIngresses.md)|调用ListIngresses接口获取Ingress列表。|
|[ListAppEvents](/cn.zh-CN/API参考/命名空间和VPC/ListAppEvents.md)|调用ListAppEvents接口查看应用事件。|

## 应用信息

|API|描述|
|---|--|
|[DescribeApplicationConfig](/cn.zh-CN/API参考/应用信息/DescribeApplicationConfig.md)|调用DescribeApplicationConfig接口获取应用配置信息。|
|[DescribeRegions](/cn.zh-CN/API参考/应用信息/DescribeRegions.md)|调用DescribeRegions接口查询可用地域。|
|[DescribeInstanceLog](/cn.zh-CN/API参考/应用信息/DescribeInstanceLog.md)|调用DescribeInstanceLog接口获取实例日志。|
|[DescribeComponents](/cn.zh-CN/API参考/应用信息/DescribeComponents.md)|调用DescribeComponents接口获取应用创建部署时所需的组件版本。|
|[DescribeEdasContainers](/cn.zh-CN/API参考/应用信息/DescribeEdasContainers.md)|调用DescribeEdasContainers接口获取应用微服务容器组件列表。|
|[DescribeApplicationImage](/cn.zh-CN/API参考/应用信息/DescribeApplicationImage.md)|调用DescribeApplicationImage接口描述应用镜像信息。|
|[DescribeApplicationInstances](/cn.zh-CN/API参考/应用信息/DescribeApplicationInstances.md)|调用DescribeApplicationInstances接口获取应用实例列表。|
|[DescribeApplicationGroups](/cn.zh-CN/API参考/应用信息/DescribeApplicationGroups.md)|调用DescribeApplicationGroups接口获取应用实例分组。|
|[ListApplications](/cn.zh-CN/API参考/应用信息/ListApplications.md)|调用ListApplications接口获取应用列表。|
|[QueryResourceStatics](/cn.zh-CN/API参考/应用信息/QueryResourceStatics.md)|调用QueryResourceStatics接口获取应用的资源使用量。|
|[ListLogConfigs](/cn.zh-CN/API参考/应用信息/ListLogConfigs.md)|调用ListLogConfigs接口获取应用日志列表。|
|[ListAppVersions](/cn.zh-CN/API参考/应用信息/ListAppVersions.md)|调用ListAppVersions接口查看应用历史版本。|

## 弹性伸缩

|API|描述|
|---|--|
|[CreateApplicationScalingRule](/cn.zh-CN/API参考/弹性伸缩/CreateApplicationScalingRule.md)|调用CreateApplicationScalingRule接口创建应用弹性伸缩策略。|
|[DeleteApplicationScalingRule](/cn.zh-CN/API参考/弹性伸缩/DeleteApplicationScalingRule.md)|调用CreateApplicationScalingRule接口删除应用弹性伸缩策略。|
|[EnableApplicationScalingRule](/cn.zh-CN/API参考/弹性伸缩/EnableApplicationScalingRule.md)|调用EnableApplicationScalingRule接口启用应用弹性伸缩策略。|
|[DisableApplicationScalingRule](/cn.zh-CN/API参考/弹性伸缩/DisableApplicationScalingRule.md)|调用DisableApplicationScalingRule接口禁用应用弹性伸缩策略。|
|[UpdateApplicationScalingRule](/cn.zh-CN/API参考/弹性伸缩/UpdateApplicationScalingRule.md)|调用UpdateApplicationScalingRule接口更新应用弹性伸缩策略。|
|[DescribeApplicationScalingRules](/cn.zh-CN/API参考/弹性伸缩/DescribeApplicationScalingRules.md)|调用DescribeApplicationScalingRules接口查询应用弹性伸缩策略。|

## 应用生命周期

|API|描述|
|---|--|
|[DescribeApplicationStatus](/cn.zh-CN/API参考/应用生命周期/DescribeApplicationStatus.md)|调用DescribeApplicationStatus接口获取应用的状态信息。|
|[DeployApplication](/cn.zh-CN/API参考/应用生命周期/DeployApplication.md)|调用DeployApplication接口部署应用。|
|[CreateApplication](/cn.zh-CN/API参考/应用生命周期/CreateApplication.md)|调用CreateApplication接口创建一个SAE应用。|
|[DeleteApplication](/cn.zh-CN/API参考/应用生命周期/DeleteApplication.md)|调用DeleteApplication接口删除应用。|
|[StartApplication](/cn.zh-CN/API参考/应用生命周期/StartApplication.md)|调用StartApplication接口启动应用。|
|[BatchStartApplications](/cn.zh-CN/API参考/应用生命周期/BatchStartApplications.md)|调用BatchStartApplications接口批量启动应用。|
|[RestartApplication](/cn.zh-CN/API参考/应用生命周期/RestartApplication.md)|调用RestartApplication接口重启应用。|
|[RestartInstances](/cn.zh-CN/API参考/应用生命周期/RestartInstances.md)|调用RestartInstances接口重启应用实例。|
|[RollbackApplication](/cn.zh-CN/API参考/应用生命周期/RollbackApplication.md)|调用RollbackApplication接口回退历史版本。|
|[RescaleApplication](/cn.zh-CN/API参考/应用生命周期/RescaleApplication.md)|调用RescaleApplication接口应用扩缩。|
|[RescaleApplicationVertically](/cn.zh-CN/API参考/应用生命周期/RescaleApplicationVertically.md)|调用RescaleApplicationVertically接口改变应用实例规格。|
|[ReduceApplicationCapacityByInstanceIds](/cn.zh-CN/API参考/应用生命周期/ReduceApplicationCapacityByInstanceIds.md)|调用ReduceApplicationCapacityByInstanceIds接口根据实例ID缩容。|
|[StopApplication](/cn.zh-CN/API参考/应用生命周期/StopApplication.md)|调用StopApplication接口停止应用。|
|[BatchStopApplications](/cn.zh-CN/API参考/应用生命周期/BatchStopApplications.md)|调用BatchStopApplications接口批量停止应用。|
|[UpdateAppSecurityGroup](/cn.zh-CN/API参考/应用生命周期/UpdateAppSecurityGroup.md)|调用UpdateAppSecurityGroup接口更新应用安全组。|
|[AbortChangeOrder](/cn.zh-CN/API参考/应用生命周期/AbortChangeOrder.md)|调用AbortChangeOrder接口中止变更单。|
|[AbortAndRollbackChangeOrder](/cn.zh-CN/API参考/应用生命周期/AbortAndRollbackChangeOrder.md)|调用AbortAndRollbackChangeOrder接口中止或回滚变更单。|
|[ConfirmPipelineBatch](/cn.zh-CN/API参考/应用生命周期/ConfirmPipelineBatch.md)|调用ConfirmPipelineBatch接口确认是否开始下一批次。|
|[DescribePipeline](/cn.zh-CN/API参考/应用生命周期/DescribePipeline.md)|调用DescribePipeline接口查看批次信息。|
|[DescribeInstanceSpecifications](/cn.zh-CN/API参考/应用生命周期/DescribeInstanceSpecifications.md)|调用DescribeInstanceSpecifications接口获取应用实例规格信息。|
|[DescribeChangeOrder](/cn.zh-CN/API参考/应用生命周期/DescribeChangeOrder.md)|调用ListChangeOrders接口获取变更单列表。|
|[ListChangeOrders](/cn.zh-CN/API参考/应用生命周期/ListChangeOrders.md)|调用ListChangeOrders接口获取变更单列表。|

## SLB

|API|描述|
|---|--|
|[BindSlb](/cn.zh-CN/API参考/SLB/BindSlb.md)|调用BindSlb接口为应用绑定SLB。|
|[UnbindSlb](/cn.zh-CN/API参考/SLB/UnbindSlb.md)|调用UnbindSlb接口解绑内网或公网SLB。|
|[DescribeApplicationSlbs](/cn.zh-CN/API参考/SLB/DescribeApplicationSlbs.md)|调用DescribeApplicationSlbs接口获取应用SLB配置信息。|

## 微服务列表

|API|描述|
|---|--|
|[ListConsumedServices](/cn.zh-CN/API参考/微服务列表/ListConsumedServices.md)|调用ListConsumedServices接口获取订阅的微服务列表。|
|[ListPublishedServices](/cn.zh-CN/API参考/微服务列表/ListPublishedServices.md)|调用ListPublishedServices接口获取发布的微服务列表。|

## 标签管理

|API|描述|
|---|--|
|[TagResources](/cn.zh-CN/API参考/标签管理/TagResources.md)|调用TagResources接口给指定的资源打上标签。|
|[UntagResources](/cn.zh-CN/API参考/标签管理/UntagResources.md)|调用UntagResources接口移除指定资源和标签之间的绑定关系。|
|[ListTagResources](/cn.zh-CN/API参考/标签管理/ListTagResources.md)|调用ListTagResources接口查询资源和标签的对应关系。|

## 配置项管理

|API|描述|
|---|--|
|[CreateConfigMap](/cn.zh-CN/API参考/配置项管理/CreateConfigMap.md)|调用CreateConfigMap接口创建ConfigMap实例。|
|[DeleteConfigMap](/cn.zh-CN/API参考/配置项管理/DeleteConfigMap.md)|调用DeleteConfigMap接口删除ConfigMap实例。|
|[UpdateConfigMap](/cn.zh-CN/API参考/配置项管理/UpdateConfigMap.md)|调用UpdateConfigMap接口更新ConfigMap实例。|
|[DescribeConfigMap](/cn.zh-CN/API参考/配置项管理/DescribeConfigMap.md)|调用DescribeConfigMap接口查询ConfigMap实例详情。|
|[ListNamespacedConfigMaps](/cn.zh-CN/API参考/配置项管理/ListNamespacedConfigMaps.md)|调用ListNamespacedConfigMaps接口获取ConfigMap实例列表。|

## 灰度规则

|API|描述|
|---|--|
|[CreateGreyTagRoute](/cn.zh-CN/API参考/灰度规则/CreateGreyTagRoute.md)|调用CreateGreyTagRoute接口为Spring Cloud或Dubbo应用创建灰度规则。|
|[DeleteGreyTagRoute](/cn.zh-CN/API参考/灰度规则/DeleteGreyTagRoute.md)|调用DeleteGreyTagRoute接口根据规则ID删除灰度规则。|
|[DescribeGreyTagRoute](/cn.zh-CN/API参考/灰度规则/DescribeGreyTagRoute.md)|调用DescribeGreyTagRoute接口根据规则ID查询灰度规则详情。|
|[ListGreyTagRoute](/cn.zh-CN/API参考/灰度规则/ListGreyTagRoute.md)|调用ListGreyTagRoute接口根据应用ID查询灰度规则详情。|
|[UpdateGreyTagRoute](/cn.zh-CN/API参考/灰度规则/UpdateGreyTagRoute.md)|调用UpdateGreyTagRoute接口更新灰度规则。|

