# DeployApplication

调用DeployApplication接口部署应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DeployApplication&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
POST /pop/v1/sam/app/deployApplication HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|需要部署的应用ID。 |
|Jdk|String|Query|否|Open JDK 8|部署的包依赖的JDK版本。镜像不支持。 |
|WebContainer|String|Query|否|apache-tomcat-7.0.91|部署的包依赖的Tomcat版本。镜像不支持。 |
|PackageVersion|String|Query|否|1.0.1|部署的包的版本号，**War**或**FatJar**类型必填。 |
|PackageUrl|String|Query|否|http://myoss.oss-cn-hangzhou.aliyuncs.com/my-buc/2019-06-30/sae-test.jar|部署的包地址。只有**FatJar**或**War**类型应用可以配置部署包地址。 |
|ImageUrl|String|Query|否|registry.cn-hangzhou.aliyuncs.com/sae\_test/ali\_sae\_test:0.0.1|镜像地址。只有**Image**类型应用可以配置镜像地址。 |
|Command|String|Query|否|sleep|镜像启动命令。该命令必须为容器内存在的可执行的对象。例如：sleep。设置该命令将导致镜像原本的启动命令失效。 |
|CommandArgs|String|Query|否|1d|镜像启动命令参数。上述启动命令所需参数。例如：1d。 |
|Envs|String|Query|否|\[\{"name":"envtmp","value":"0"\}\]|容器环境变量参数。取值说明如下：

 -   **name**：变量名称。
-   **value**：变量值或变量引用。 |
|CustomHostAlias|String|Query|否|\[\{"hostName":"samplehost","ip":"127.0.0.1"\}\]|容器内自定义Host映射。取值说明如下：

 -   **hostName**：主机名称或域名。
-   **ip**：IP地址 |
|JarStartOptions|String|Query|否|custom-option|JAR包启动应用选项。应用默认启动命令：**$JAVA\_HOME/bin/java $JarStartOptions -jar $CATALINA\_OPTS "$package\_path" $JarStartArgs** |
|JarStartArgs|String|Query|否|-Xms4G -Xmx4G|JAR包启动应用参数。应用默认启动命令：**$JAVA\_HOME/bin/java $JarStartOptions -jar $CATALINA\_OPTS "$package\_path" $JarStartArgs** |
|Liveness|String|Query|否|\{"exec":\{"command":\["sleep","5s"\]\},"initialDelaySeconds":10,"timeoutSeconds":11\}|容器健康检查，健康检查失败的容器将被关闭并恢复。目前仅支持容器内下发命令的方式。例如：\{"exec":\{"command":\["sh","-c","cat /home/admin/start.sh"\]\},"initialDelaySeconds":30,"periodSeconds":30,"timeoutSeconds":2\}

 -   **command**：设置健康检查命令。
-   **initialDelaySeconds**：设置健康检查延迟检测时间，单位为秒。
-   **periodSeconds**：设置健康检查周期，单位为秒。
-   **timeoutSeconds**：设置健康检查超时等待时间，单位为秒。 |
|Readiness|String|Query|否|\{"exec":\{"command":\["sleep","6s"\]\},"initialDelaySeconds":15,"timeoutSeconds":12\}|应用启动状态检查，多次健康检查失败的容器将被关闭并重启。不通过健康检查的容器将不会有SLB流量进入。例如：\{"exec":\{"command":\["sh","-c","cat /home/admin/start.sh"\]\},"initialDelaySeconds":30,"periodSeconds":30,"timeoutSeconds":2\}

 -   **command**：设置健康检查命令。
-   **initialDelaySeconds**：设置健康检查延迟检测时间，单位为秒。
-   **periodSeconds**：设置健康检查周期，单位为秒。
-   **timeoutSeconds**：设置健康检查超时等待时间，单位为秒。 |
|MinReadyInstances|Integer|Query|否|1|最小可用实例数。任何变更都会保持设置的实例数，保证业务稳定性。 |
|BatchWaitTime|Integer|Query|否|10|分批等待时间，单位为秒。 |
|EdasContainerVersion|String|Query|否|3.5.3|Pandora应用使用的运行环境。 |
|UpdateStrategy|String|Query|否|\{"type":"GrayBatchUpdate","batchUpdate":\{"batch":2,"releaseType":"auto","batchWaitTime":1\},"grayUpdate":\{"gray":1\}\}|部署策略。示例如下：

 -   例1（灰度1台+后续分2批+自动分批+分批间隔1分钟）：\{"type":"GrayBatchUpdate","batchUpdate":\{"batch":2,"releaseType":"auto","batchWaitTime":1\},"grayUpdate":\{"gray":1\}\}
-   例2（灰度1台+后续分2批+手动分批）：\{"type":"GrayBatchUpdate","batchUpdate":\{"batch":2,"releaseType":"manual"\},"grayUpdate":\{"gray":1\}\}
-   例3（分2批+自动分批+分批间隔0分钟）：\{"type":"BatchUpdate","batchUpdate":\{"batch":2,"releaseType":"auto","batchWaitTime":0\}\} |
|SlsConfigs|String|Query|否|\[\{"logDir":"/root/logs/hsf/hsf.log"\}\]|文件日志采集配置。

 -   使用SAE自动创建的SLS资源：\[\{\\"logDir\\":\\"/root/logs/hsf.log\\"\}\]。
-   使用自定义SLS资源：\[\{\\"projectName\\":\\"test-sls\\",\\"logDir\\":\\"/tmp/readiness.txt\\",\\"logstoreName\\":\\"logstore\\","logtailName":"testLogtail"\}\]。
    -   **projectName**：配置SLS上的Project名称。
    -   **logDir**：配置收集日志文件的路径。
    -   **logstoreName**：配置SLS上的Logstore名称。
    -   **logtailName**：配置SLS上的Logtail名称，如果不指定，则表示新建Logtail。


 多次部署时如果SLS采集配置没有变更，则您不需要设置该参数（即请求中无需包含**SlsConfigs**字段）；如果您不再需要使用SLS采集功能，您可以在请求中将该字段的值设置为空字符串（即请求中**SlsConfigs**字段的值为""）。 |
|Timezone|String|Query|否|Asia/Shanghai|时区。 |
|NasId|String|Query|否|10d3b4\*\*\*\*|NAS文件系统的ID。 |
|MountHost|String|Query|否|10d3b4bc9\*\*\*\*.com|NAS在应用VPC内的挂载点。 |
|MountDesc|String|Query|否|\[\{MountPath: "/tmp", NasPath: "/"\}\]|NAS挂载描述。 |
|PostStart|String|Query|否|\["/bin/sh","-c","echo hello"\]|容器启动后钩子，在容器被创建后立刻触发执行，通知容器它已经被创建。 |
|PreStop|String|Query|否|\["/bin/sh","-c","echo hello"\]|容器停止前钩子，在容器被删除前触发，其所对应的Hook Handler必须在删除该容器的请求发送给Docker Daemon之前完成。 |
|ChangeOrderDesc|String|Query|否|启动应用|发布单描述信息。 |
|WarStartOptions|String|Query|否|-Dxxx=xxx|WAR包部署应用时的JVM参数，非必填项。 |
|AutoEnableApplicationScalingRule|Boolean|Query|否|true|是否在应用部署后，自动开启弹性伸缩策略。取值说明如下：

 -   **true**：默认值，部署后自动开启策略。
-   **false**：部署后，禁用策略。 |
|ConfigMapMountDesc|String|FormData|否|\[\{"configMapId":16,"key":"test","mountPath":"/tmp"\}\]|**ConfigMap**挂载描述。 |
|TerminationGracePeriodSeconds|Integer|Query|否|10|优雅下线超时时间，默认为30，单位为秒。取值范围为1~60。 |
|EnableAhas|String|Query|否|false|是否接入AHAS。取值说明如下：

 -   **true**：表示接入AHAS。
-   **false**：表示不接入AHAS。 |
|PhpArmsConfigLocation|String|Query|否|/usr/local/etc/php/conf.d/arms.ini|PHP应用监控挂载路径，需要您保证PHP服务器一定会加载这个路径的配置文件。您无需关注配置内容，SAE会自动渲染正确的配置文件。 |
|PhpConfigLocation|String|Query|否|/usr/local/etc/php/php.ini|PHP应用启动配置挂载路径，需要您保证PHP服务器会使用这个配置文件启动。 |
|PhpConfig|String|FormData|否|k1=v1|PHP配置文件内容。 |
|TomcatConfig|String|Query|否|\{"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false\}|Tomcat文件配置，设置为""或"\{\}"表示删除配置。取值说明如下：

 -   **useDefaultConfig**：是否使用自定义配置，若为**true**，则表示不使用自定义配置；若为**false**，则表示使用自定义配置。若不使用自定义配置，则下面的参数配置将不会生效。
-   **contextInputType**：选择应用的访问路径。
    -   **war**：无需填写自定义路径，应用的访问路径是WAR包名称。
    -   **root**：无需填写自定义路径，应用的访问路径是/。
    -   **custom**：需要在下面的自定义路径中填写自定义的路径。
-   **contextPath**：自定义路径，当**contextInputType**类型为**custom**时，才需要配置此参数。
-   **httpPort**：端口范围为1024~65535，小于1024的端口需要Root权限才能操作。因为容器配置的是Admin权限，所以请填写大于1024的端口。如果不配置，则默认为8080。
-   **maxThreads**：配置连接池的连接数大小，默认大小为400。
-   **uriEncoding**：Tomcat的编码格式，包括**UTF-8**、**ISO-8859-1**、**GBK和GB2312**。如果不设置，则默认为**ISO-8859-1**。
-   **useBodyEncoding**：是否使用**BodyEncoding for URL**。 |
|AcrAssumeRoleArn|String|Query|否|acs:ram::123456789012\*\*\*\*:role/adminrole|跨账号拉取镜像时所需的RAM角色的ARN。 |
|OssMountDescs|String|FormData|否|\[\{"bucketName": "oss-bucket", "bucketPath": "data/user.data", "mountPath": "/usr/data/user.data", "readOnly": true\}\]|OSS挂载描述信息。 |
|OssAkId|String|FormData|否|xxxxxx|OSS读写的AccessKey ID。 |
|OssAkSecret|String|FormData|否|xxxxxx|OSS读写的AccessKey Secret。 |
|EnableGreyTagRoute|Boolean|Query|否|false|是否启用流量灰度规则。该规则仅适用于Spring Cloud和Dubbo框架的应用。取值说明如下：

 -   **true**：启用灰度规则。
-   **false**：禁用灰度规则。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|01CF26C7-00A3-4AA6-BA76-7E95F2A3\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|ac1a0b2215622246421415014e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88\*\*\*\*|返回的发布单ID，用于查询任务执行状态。 |
|AppId|String|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|部署应用是否成功。取值说明如下：

 -   **true**：表示部署成功。
-   **false**：表示部署失败。 |

## 示例

请求示例

```
POST /pop/v1/sam/app/deployApplication?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69****&Jdk=Open JDK 8&WebContainer=apache-tomcat-7.0.91&PackageVersion=1.0.1&PackageUrl=http://myoss.oss-cn-hangzhou.aliyuncs.com/my-buc/2019-06-30/sae-test.jar&ImageUrl=registry.cn-hangzhou.aliyuncs.com/sae_test/ali_sae_test:0.0.1&Command=sleep&CommandArgs=1d&Envs=[{"name":"envtmp","value":"0"}]&CustomHostAlias=[{"hostName":"samplehost","ip":"127.0.0.1"}]&JarStartOptions=custom-option&JarStartArgs=-Xms4G -Xmx4G&Liveness={"exec":{"command":["sleep","5s"]},"initialDelaySeconds":10,"timeoutSeconds":11}&Readiness={"exec":{"command":["sleep","6s"]},"initialDelaySeconds":15,"timeoutSeconds":12}&MinReadyInstances=1&BatchWaitTime=10&EdasContainerVersion=3.5.3&UpdateStrategy={"type":"GrayBatchUpdate","batchUpdate":{"batch":2,"releaseType":"auto","batchWaitTime":1},"grayUpdate":{"gray":1}}&SlsConfigs=[{"logDir":"/root/logs/hsf/hsf.log"}]&Timezone=Asia/Shanghai&NasId=10d3b4****&MountHost=10d3b4bc9****.com&MountDesc=[{MountPath: "/tmp", NasPath: "/"}]&PostStart=["/bin/sh","-c","echo hello"]&PreStop=["/bin/sh","-c","echo hello"]&ChangeOrderDesc=启动应用&WarStartOptions=-Dxxx=xxx&AutoEnableApplicationScalingRule=true&TerminationGracePeriodSeconds=10&EnableAhas=false&PhpArmsConfigLocation=/usr/local/etc/php/conf.d/arms.ini&PhpConfigLocation=/usr/local/etc/php/php.ini&TomcatConfig={"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false}&AcrAssumeRoleArn=acs:ram::123456789012****:role/adminrole&EnableGreyTagRoute=false HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数

ConfigMapMountDesc=[{"configMapId":16,"key":"test","mountPath":"/tmp"}]&PhpConfig=k1=v1&OssMountDescs=[{"bucketName": "oss-bucket", "bucketPath": "data/user.data", "mountPath": "/usr/data/user.data", "readOnly": true}]&OssAkId=xxxxxx&OssAkSecret=xxxxxx
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DeployApplicationResponse>
    <RequestId>01CF26C7-00A3-4AA6-BA76-7E95F2A3***</RequestId>
    <Message>success</Message>
    <TraceId>ac1a0b2215622246421415014e****</TraceId>
    <Data>
        <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88****</ChangeOrderId>
        <AppId>7171a6ca-d1cd-4928-8642-7d5cfe69****</AppId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DeployApplicationResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "01CF26C7-00A3-4AA6-BA76-7E95F2A3***",
  "Message" : "success",
  "TraceId" : "ac1a0b2215622246421415014e****",
  "Data" : {
    "ChangeOrderId" : "01db03d3-3ee9-48b3-b3d0-dfce2d88****",
    "AppId" : "7171a6ca-d1cd-4928-8642-7d5cfe69****"
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Application.MissingJdk|Your application must at least contain a JDK component.|应用必须至少包含JDK组件。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidComponent.NotFound|The current component \(such as JDK, Tomcat, or EDASWebContainer\) does not exist.|找不到当前组件（JDK、Tomcat、EDASWebContainer等）。|
|400|InvalidHostnameIp.Invalid|The hostname and/or IP is invalid: Hostname \[%s\], IP \[%s\].|主机名和/或IP不合法：主机名\[%s\]，IP\[%s\]。|
|400|InvalidInstanceSpecification.Unsupported|The instance specification is not supported: CPU \[%s\], memory \[%s\].|不支持的实例规格。CPU\[%s\]，Memory\[%s\]。|
|400|InvalidPackageType.NotFound|The package type must be War, FatJar, or Image.|包类型必须为War、Fatjar或Image。|
|400|InvalidParameter.FileName|The application deployment package name is invalid. This name can contain only alphanumeric characters, hyphens \(-\), and underscores \(\_\). In addition, you can upload JAR files only if the selected deployment version supports JAR file. Otherwise, upload WAR files only.|应用部署程序包名称无效。名称只能包含字母、数字和特殊字符“-”“\_”。另外，仅当选择的部署版本支持JAR部署时方可上传JAR包，否则只能上传WAR包。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|JarApplication.MissingJdk|A FatJar application must contain JDK.|FatJAR类型应用必须包含JDK。|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|
|400|PandoraApplication.MissingJdk|The Pandora application is missing a JDK component.|Pandora应用缺少JDK组件。|
|400|PandoraApplication.OnlyJdk|A Pandora application only requires JDK component.|Pandora应用只需要JDK组件。|
|400|WarApplication.MissingJdkWebcontainer|A War application must contain JDK and Tomcat.|War类型应用必须包含JDK和Tomcat。|
|400|LogService.ConfigQuotaExceed|The maximum number of Log Service configs is exceeded.|日志服务配置个数超过配额限制，请提工单解决。|
|400|LogService.InternalError|An exception occurred while calling Log Service. Please submit a ticket to solve the problem.|调用日志服务异常，请提工单解决。|
|400|LogService.LogDirInvalid|The log collection path is invalid.|日志采集路径不合法。|
|400|LogService.NotAvailable|Log Service is unavailable. Please activate Log Service first.|日志服务不可用，请先开通日志服务。|
|400|LogService.ProjectNumQuotaExceed|The maximum number of Log Service projects is exceeded.|日志服务项目个数超过配额限制，请提工单解决。|
|400|user.indebt|The user has an outstanding payment.|当前用户处于欠费状态。|
|400|NoComputeResourceQuota.App.Exceed|You can create %s instances for each application. Please submit a ticket to raise the quota.|每个应用只允许创建%s个实例，请提交工单增加计算资源额度。|
|400|NoComputeResourceQuota.User.Exceed|Your account is limited to create %s instances. Please submit a ticket to raise the quota.|您的账户限额%s个实例，请提交工单增加计算资源额度。|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|VolumnPath.Conflict|Conflict between log collection directory and persistent storage directory.|日志采集目录与持久化存储目录冲突。|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|MountConflict.ConfigMap|Conflict detected for ConfigMap path %s.|ConfigMap挂载路径%s存在冲突。|
|400|NotFound.ConfigMap|The ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）。|
|400|NotFound.ConfigMapKey|The key %s of ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）的Key %s。|
|400|Package.Version.Too.Long|The maximum length of package version is exceeded.|应用部署包版本号长度超过限制。|
|400|App.Package.Version.Exists|The package version of application already exists.|应用部署包版本号已经存在。|
|400|Slb.Occupied|The SLB instance is occupied.|SLB实例被占用。|
|400|Slb.Tag.Not.Qualified|The current SLB instance cannot be reused because it may have been occupied by %s.|SLB实例正在被%s使用，不建议复用。|
|400|MinReadyInstances.Not.Smaller.Replicas|The minimum number of available instances must be less than the number of application instances.|最小可用实例数必须小于应用实例数。|
|400|BatchWaitTime.Not.Smaller.Zero|BatchWaitTime must not be smaller than zero.|分批间隔时间必须大于零。|
|400|Sls.Config.Mixed.Multi.Project|The specified Config contains multiple projects.|用户输入的SLS Config中指定了多个project|
|400|Sls.Config.User.Defined.Missing.Logstore.Info|The specified Config is invalid. Both Project and Logstore must be specified.|用户输入的SLS Config为自定义SLS配置，但是只有Project配置，缺失Logstore配置|
|400|Sls.Config.User.Defined.Missing.Project.Info|The specified Config is invalid. Both Project and Logstore must be specified.|用户输入的SLS Config为自定义SLS配置，但是只有Logstore配置，缺失Project配置|
|400|Sls.Logstore.Name.Invalid|The specified name of Logstore is invalid. The Logstore name must not contain the prefix "sae-".|用户输入的SLS Logstore名称不合法，前缀包含了"sae-"，会与SAE自动创建的Logstore混淆|
|400|Sls.Logstore.User.Defined.Not.Exist|The user defined Logstore does not exist.|用户输入的自建Logstore，不存在|
|400|Sls.Project.Name.Invalid|The specified project name is invalid. The project name must not contain the prefix "sae-".|用户输入的SLS Project名称不合法，前缀包含了"sae-"，会与SAE自动创建的Project混淆|
|400|Sls.Project.User.Defined.Not.Exist|The user defined project does not exist.|用户输入的自建Project，不存在|
|400|Sae.Errorcode.Ahas.Create.Error.Message|Failed to create AHAS.|创建ahas失败|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

