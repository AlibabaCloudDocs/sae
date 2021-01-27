# RollbackApplication

调用RollbackApplication接口回退应用历史版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=RollbackApplication&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/app/rollbackApplication HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|017f39b8-dfa4-4e16-a84b-1dcee4b1\*\*\*\*|应用ID。 |
|VersionId|String|Query|是|0026ff7f-2b57-4127-bdd0-9bf202bb9\*\*\*\*|版本ID，需要调用[ListAppVersions](~~162054~~)接口查看。 |
|BatchWaitTime|Integer|Query|否|10|分批等待时间（单位：秒）。 |
|MinReadyInstances|Integer|Query|否|1|为保证业务稳定性而设置的最小可用实例数。 |
|UpdateStrategy|String|Query|否|\{"type":"GrayBatchUpdate","batchUpdate":\{"batch":2,"releaseType":"auto","batchWaitTime":1\},"grayUpdate":\{"gray":1\}\}|部署策略。示例如下：

 -   示例1：灰度1台+后续分2批+自动分批+分批间隔1分钟。`{"type":"GrayBatchUpdate","batchUpdate":{"batch":2,"releaseType":"auto","batchWaitTime":1},"grayUpdate":{"gray":1}}`
-   示例2：灰度1台+后续分2批+手动分批。`{"type":"GrayBatchUpdate","batchUpdate":{"batch":2,"releaseType":"manual"},"grayUpdate":{"gray":1}}`
-   示例3：分2批+自动分批+分批间隔0分钟。`{"type":"BatchUpdate","batchUpdate":{"batch":2,"releaseType":"auto","batchWaitTime":0}}` |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态，取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88\*\*\*\*|变更流程ID。 |
|ErrorCode|String|Application.ChangerOrderRunning|错误码。 |
|Message|String|success|附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D5557|请求ID。 |
|Success|Boolean|true|回退历史版本是否成功。取值说明如下：

 -   **true**：表示回退历史版本成功。
-   **false**：表示回退历史版本失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID。 |

## 示例

请求示例

```
PUT /pop/v1//sam/app/rollbackApplication?RegionId=cn-hangzhou&AppId=017f39b8-dfa4-4e16-a84b-1dcee4b1****&VersionId=0026ff7f-2b57-4127-bdd0-9bf202bb9****
```

正常返回示例

`XML`格式

```
<RollbackApplicationResponse>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88****</ChangeOrderId>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</RollbackApplicationResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "ChangeOrderId": "01db03d3-3ee9-48b3-b3d0-dfce2d88****"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|
|400|vswitch.not.exist|The specified VSwitch does not exist.|VSwitch不存在，请更换VSwitch。|
|400|user.indebt|The user has an outstanding payment.|您处于欠费状态。|
|400|NoComputeResourceQuota.App.Exceed|You can create %s instances for each application. Please submit a ticket to raise the quota.|每个应用只允许创建%s个实例，请提交工单增加计算资源额度。|
|400|NoComputeResourceQuota.User.Exceed|Your account is limited to create %s instances. Please submit a ticket to raise the quota.|您的账户限额%s个实例，请提交工单增加计算资源额度。|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|Application.NotDeployYet|The application has not been deployed. Please deploy it and try again.|应用没有部署，请部署后重试。|
|400|rollback.error|Failed to roll back.|回滚异常。|
|400|Application.MissingJdk|Your application must at least contain a JDK component.|应用必须至少包含JDK组件。|
|400|JarApplication.MissingJdk|A FatJar application must contain JDK.|FatJAR类型应用必须包含JDK。|
|400|PandoraApplication.MissingJdk|The Pandora application is missing a JDK component.|Pandora应用缺少JDK组件。|
|400|WarApplication.MissingJdkWebcontainer|A War application must contain JDK and Tomcat.|WAR类型应用必须包含JDK和Tomcat。|
|400|InvalidComponent.NotFound|The current component \(such as JDK, Tomcat, or EDASWebContainer\) does not exist.|找不到当前组件（JDK、Tomcat、EDASWebContainer等）。|
|400|InvalidHostnameIp.Invalid|The hostname and/or IP is invalid: Hostname \[%s\], IP \[%s\].|主机名或IP不合法：主机名\[%s\]，IP\[%s\]。|
|400|InvalidInstanceSpecification.Unsupported|The instance specification is not supported: CPU \[%s\], memory \[%s\].|不支持的实例规格。CPU\[%s\]，Memory\[%s\]。|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|
|400|InvalidPackageType.NotFound|The package type must be War, FatJar, or Image.|包类型必须为WAR、FatJAR或Image。|
|400|InvalidParameter.FileName|The application deployment package name is invalid. This name can contain only alphanumeric characters, hyphens \(-\), and underscores \(\_\). In addition, you can upload JAR files only if the selected deployment version supports JAR file. Otherwise, upload WAR files only.|应用部署程序包名称无效。名称只能包含字母、数字和特殊字符“-”“\_”。另外，仅当选择的部署版本支持JAR部署时方可上传JAR包，否则只能上传WAR包。|
|400|LogService.ConfigQuotaExceed|The maximum number of Log Service configs is exceeded.|日志服务配置个数超过配额限制，请提工单解决。|
|400|LogService.InternalError|An exception occurred while calling Log Service. Please submit a ticket to solve the problem.|调用日志服务异常，请提工单解决。|
|400|LogService.LogDirInvalid|The log collection path is invalid.|日志采集路径不合法。|
|400|LogService.NotAvailable|Log Service is unavailable. Please activate Log Service first.|日志服务不可用，请先开通日志服务。|
|400|LogService.ProjectNumQuotaExceed|The maximum number of Log Service projects is exceeded.|日志服务项目个数超过配额限制，请提工单解决。|
|400|VolumnPath.Conflict|Conflict between log collection directory and persistent storage directory.|日志采集目录与持久化存储目录冲突。|
|400|MountConflict.ConfigMap|Conflict detected for ConfigMap path %s.|ConfigMap挂载路径%s存在冲突。|
|400|NotFound.ConfigMap|The ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）。|
|400|NotFound.ConfigMapKey|The key %s of ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）的Key %s。|
|400|MinReadyInstances.Not.Smaller.Replicas|The minimum number of available instances must be less than the number of application instances.|最小可用实例数必须小于应用实例数。|
|400|Package.Version.Too.Long|The maximum length of package version is exceeded.|应用部署包版本号长度超过限制。|
|400|App.Package.Version.Exists|The package version of application already exists.|应用部署包版本号已经存在。|
|400|Slb.Occupied|The SLB instance is occupied.|SLB实例被占用。|
|400|Slb.Tag.Not.Qualified|The current SLB instance cannot be reused because it may have been occupied by %s.|SLB实例正在被%s使用，不建议复用。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

