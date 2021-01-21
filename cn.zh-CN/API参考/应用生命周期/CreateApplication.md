# CreateApplication

调用CreateApplication接口创建一个应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateApplication&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/sam/app/createApplication HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppName|String|Query|是|test|应用名称。允许数字、字母以及短划线（-）组合。必须以字母开始，最大长度36个字符。 |
|PackageType|String|Query|是|FatJar|应用包类型。支持**FatJar**、**War**和**Image**。 |
|Replicas|Integer|Query|是|1|初始实例数。 |
|NamespaceId|String|Query|否|cn-beijing:test|SAE命名空间ID。仅支持名称为小写字母加短划线（-）的命名空间，必须以字母开始。

 命名空间可通过调用[DescribeNamespaceList](~~126547~~)接口获取。 |
|AppDescription|String|Query|否|This is a test description.|应用描述信息。不超过1024个字符。 |
|VpcId|String|Query|否|vpc-bp1aevy8sofi8mh1q\*\*\*\*|SAE命名空间对应的VPC。在SAE中，一个命名空间只能对应一个VPC，且不能修改。第一次在命名空间内创建SAE应用将形成绑定关系。多个命名空间可以对应一个VPC。不填则默认为命名空间绑定的VPC ID。 |
|VSwitchId|String|Query|否|vsw-bp12mw1f8k3jgygk9\*\*\*\*|应用实例弹性网卡所在的虚拟交换机。该交换机必须位于上述VPC内。该交换机与SAE命名空间同样存在绑定关系。不填则默认为命名空间绑定的VSwitch ID。 |
|PackageVersion|String|Query|否|1.0.0|部署包的版本号。当**Package Type**为**War**和**FatJar**时必填。 |
|PackageUrl|String|Query|否|http://myoss.oss-cn-hangzhou.aliyuncs.com/my-buc/2019-06-30/sae-test.jar|部署包地址。只有**FatJar**或**War**类型的应用可以配置部署包地址。 |
|ImageUrl|String|Query|否|registry.cn-hangzhou.aliyuncs.com/sae\_test/ali\_sae\_test:0.0.1|镜像地址。只有**Image**类型的应用可以配置镜像地址。 |
|Jdk|String|Query|否|Open JDK 8|部署包依赖的JDK版本。**Image**类型的应用不支持。 |
|WebContainer|String|Query|否|apache-tomcat-7.0.91|部署包依赖的tomcat版本。**Image**类型的应用不支持。 |
|Cpu|Integer|Query|否|1000|每个实例所需的CPU，单位为毫核，不能为0。目前仅支持以下固定规格：

 -   **500**
-   **1000**
-   **2000**
-   **4000**
-   **8000**
-   **16000**
-   **32000** |
|Memory|Integer|Query|否|1024|每个实例所需的内存，单位为MB，不能为0。与CPU为一一对应关系，目前仅支持以下固定规格：

 -   **1024**：对应CPU为500毫核。
-   **2048**：对应CPU为500和1000毫核。
-   **4096**：对应CPU为1000和2000毫核。
-   **8192**：对应CPU为2000和4000毫核。
-   **16384**：对应CPU为4000和8000毫核。
-   **32768**：对应CPU为16000毫核。
-   **65536**：对应CPU为8000、16000和32000毫核。
-   **131072**：对应CPU为32000毫核。 |
|Command|String|Query|否|sleep|镜像启动命令。该命令必须为容器内存在的可执行的对象。例如：sleep。设置该命令将导致镜像原本的启动命令失效。 |
|CommandArgs|String|Query|否|1d|镜像启动命令参数。上述启动命令所需参数。例如：1d |
|Envs|String|Query|否|\[\{"name":"envtmp","value":"0"\}\]|容器环境变量参数。例如： \[\{"name":"envtmp","value":"0"\}\] |
|CustomHostAlias|String|Query|否|\[\{"hostName":"samplehost","ip":"127.0.0.1"\}\]|容器内自定义host映射。例如： \[\{"hostName":"samplehost","ip":"127.0.0.1"\}\] |
|JarStartOptions|String|Query|否|-Xms4G -Xmx4G|Jar包启动应用选项。应用默认启动命令：$JAVA\_HOME/bin/java $JarStartOptions -jar $CATALINA\_OPTS "$package\_path" $JarStartArgs |
|JarStartArgs|String|Query|否|custom-args|Jar包启动应用参数。应用默认启动命令：$JAVA\_HOME/bin/java $JarStartOptions -jar $CATALINA\_OPTS "$package\_path" $JarStartArgs |
|Liveness|String|Query|否|\{"exec":\{"command":\["sh","-c","cat /home/admin/start.sh"\]\},"initialDelaySeconds":30,"periodSeconds":30,"timeoutSeconds":2\}|容器健康检查，健康检查失败的容器将被关闭并恢复。目前仅支持容器内下发命令的方式。例如：\{"exec":\{"command":\["sh","-c","cat /home/admin/start.sh"\]\},"initialDelaySeconds":30,"periodSeconds":30,"timeoutSeconds":2\}

 -   **command**：设置健康检查命令。
-   **initialDelaySeconds**：设置健康检查延迟检测时间，单位为秒。
-   **periodSeconds**：设置健康检查周期，单位为秒。
-   **timeoutSeconds**：设置健康检查超时等待时间，单位为秒。 |
|Readiness|String|Query|否|\{"exec":\{"command":\["sh","-c","cat /home/admin/start.sh"\]\},"initialDelaySeconds":30,"periodSeconds":30,"timeoutSeconds":2\}|应用启动状态检查，多次健康检查失败的容器将被关闭并重启。不通过健康检查的容器将不会有SLB流量进入。例如：\{"exec":\{"command":\["sh","-c","cat /home/admin/start.sh"\]\},"initialDelaySeconds":30,"periodSeconds":30,"timeoutSeconds":2\}

 -   **command**：设置健康检查命令。
-   **initialDelaySeconds**：设置健康检查延迟检测时间，单位为秒。
-   **periodSeconds**：设置健康检查周期，单位为秒。
-   **timeoutSeconds**：设置健康检查超时等待时间，单位为秒。 |
|Deploy|Boolean|Query|否|true|是否立即部署。取值说明如下：

 -   **true**：立即部署。
-   **false**：稍后部署。

 不填则默认为**false**。 |
|EdasContainerVersion|String|Query|否|3.5.3|Pandora应用使用的运行环境。 |
|Timezone|String|Query|否|Asia/Shanghai|应用时区默认为**Asia/Shanghai**。 |
|SlsConfigs|String|Query|否|\[\{\\"logDir\\":\\"/root/logs/hsf.log\\"\}\]|文件日志采集配置。

 -   使用SAE自动创建的SLS资源：\[\{\\"logDir\\":\\"/root/logs/hsf.log\\"\}\]。
-   使用自定义SLS资源：\[\{\\"logDir\\":\\"/tmp/readiness.txt\\",\\"logstoreName\\":\\"logstore\\",\\"projectName\\":\\"test-sls\\"\}\]。
    -   **logDir**：配置收集日志文件的路径。
    -   **logstoreName**：配置SLS上的Logstore名称。
    -   **projectName**：配置SLS上的Project名称。 |
|NasId|String|Query|否|KSAK\*\*\*\*|挂载的NAS的ID，必须与集群处在同一个地域。它必须有可用的挂载点创建额度，或者其挂载点已经在VPC内的交换机上。如果不填，且存在mountDescs字段，则默认将自动购买一个NAS并挂载至VPC内的交换机上。 |
|MountHost|String|Query|否|example.com|NAS在应用VPC内的挂载点。 |
|MountDesc|String|Query|否|\[\{MountPath: "/tmp", NasPath: "/"\}\]|挂载描述。 |
|PreStop|String|Query|否|\{"exec":\{"command":\["cat","/etc/group"\]\}\}|停止前执行脚本，格式如：\{"exec":\{"command":\["cat","/etc/group"\]\}\} |
|PostStart|String|Query|否|\{"exec":\{"command":\["cat","/etc/group"\]\}\}|启动后执行脚本，格式如：\{"exec":\{"command":\["cat","/etc/group"\]\}\} |
|WarStartOptions|String|Query|否|custom-option|War包启动应用选项。应用默认启动命令：java $JAVA\_OPTS $CATALINA\_OPTS \[-Options\] org.apache.catalina.startup.Bootstrap "$@" start |
|ConfigMapMountDesc|String|Body|否|\[\{"configMapId":16,"key":"test","mountPath":"/tmp"\}\]|ConfigMap挂载描述。 |
|SecurityGroupId|String|Query|否|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |
|AutoConfig|Boolean|Query|否|true|是否自动配置网络环境。取值说明如下：

 -   **true**：创建应用时SAE自动配置网络环境。**NamespaceId**、**VpcId**、**VSwitchId**和**SecurityGroupId**的取值将被忽略。
-   **false**：创建应用时SAE手动配置网络环境。 |
|TerminationGracePeriodSeconds|Integer|Query|否|30|优雅下线超时时间，默认为30，单位为秒。取值范围为1~60。 |
|PhpArmsConfigLocation|String|Query|否|/usr/local/etc/php/conf.d/arms.ini|PHP应用监控挂载路径，需要您保证PHP服务器一定会加载这个路径的配置文件。

 您无需关注配置内容，SAE会自动渲染正确的配置文件。 |
|PhpConfigLocation|String|Query|否|/usr/local/etc/php/php.ini|PHP应用启动配置挂载路径，需要您保证PHP服务器会使用这个配置文件启动。 |
|PhpConfig|String|Body|否|k1=v1|PHP配置文件内容。 |
|TomcatConfig|String|Query|否|\{"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false\}|Tomcat文件配置，设置为""或"\{\}"表示删除配置：

 -   **useDefaultConfig**：是否使用自定义配置，若为**true**，则表示不使用自定义配置；若为**false**，则表示使用自定义配置。若不使用自定义配置，则下面的参数配置将不会生效。
-   **contextInputType**：选择应用的访问路径。
    -   **war**：无需填写自定义路径，应用的访问路径是WAR包名称。
    -   **root**：无需填写自定义路径，应用的访问路径是/。
    -   **custom**：需要在下面的自定义路径中填写自定义的路径。
-   **contextPath**：自定义路径，当**contextInputType**类型为**custom**时，才需要配置此参数。
-   **httpPort**：端口范围为1024~65535，小于1024的端口需要Root权限才能操作。因为容器配置的是Admin权限，所以请填写大于1024的端口。如果不配置，则默认为8080。
-   **maxThreads**：配置连接池的连接数大小，默认大小是400。
-   **uriEncoding**：Tomcat的编码格式，包括**UTF-8**、**ISO-8859-1**、**GB**K和**GB2312**。如果不设置则默认为**ISO-8859-1**。
-   **useBodyEncoding**：是否使用**BodyEncoding for URL**。 |
|AcrAssumeRoleArn|String|Query|否|acs:ram::123456789012\*\*\*\*:role/adminrole|跨账号拉取镜像时所需的RAM角色的ARN。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|AppId|String|017f39b8-dfa4-4e16-a84b-1dcee4b1\*\*\*\*|创建成功的应用ID。 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88\*\*\*\*|返回的发布单ID，用于查询任务执行状态。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|创建应用是否成功。取值说明如下：

 -   **true**：表示创建成功。
-   **false**：表示创建失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
POST /pop/v1/sam/app/createApplication?RegionId=cn-beijing&AppName=test&PackageType=FatJar&Replicas=1
```

正常返回示例

`XML`格式

```
<CreateApplicationResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <AppId>017f39b8-dfa4-4e16-a84b-1dcee4b1****</AppId>
            <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88****</ChangeOrderId>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</CreateApplicationResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "AppId": "017f39b8-dfa4-4e16-a84b-1dcee4b1****",
        "ChangeOrderId": "01db03d3-3ee9-48b3-b3d0-dfce2d88****"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Application.MissingJdk|Your application must at least contain a JDK component.|应用必须至少包含JDK组件。|
|400|InvalidPackageType.NotFound|The package type must be War, FatJar, or Image.|包类型必须为WAR、FatJAR或Image。|
|400|InvalidParameter.FileName|The application deployment package name is invalid. This name can contain only alphanumeric characters, hyphens \(-\), and underscores \(\_\). In addition, you can upload JAR files only if the selected deployment version supports JAR file. Otherwise, upload WAR files only.|应用部署程序包名称无效。名称只能包含字母、数字和特殊字符“-”“\_”。另外，仅当选择的部署版本支持JAR部署时方可上传JAR包，否则只能上传WAR包。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|JarApplication.MissingJdk|A FatJar application must contain JDK.|FatJAR类型应用必须包含JDK。|
|400|NoAvailableCluster.NotFound|No clusters are available for the current region.|当前地域没有可用集群。|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|
|400|PandoraApplication.MissingJdk|The Pandora application is missing a JDK component.|Pandora应用缺少JDK组件。|
|400|PandoraApplication.OnlyJdk|A Pandora application only requires JDK component.|Pandora应用只需要JDK组件。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|InvalidComponent.NotFound|The current component \(such as JDK, Tomcat, or EDASWebContainer\) does not exist.|找不到当前组件（JDK、Tomcat、EDASWebContainer等）。|
|400|InvalidHostnameIp.Invalid|The hostname and/or IP is invalid: Hostname \[%s\], IP \[%s\].|主机名或IP不合法：主机名\[%s\]，IP\[%s\]。|
|400|InvalidInstanceSpecification.Unsupported|The instance specification is not supported: CPU \[%s\], memory \[%s\].|不支持的实例规格。CPU\[%s\]，Memory\[%s\]。|
|400|InvalidServerlessRegion.Unsupported|The current region is not supported: %s|不支持当前地域：%s。|
|400|WarApplication.MissingJdkWebcontainer|A War application must contain JDK and Tomcat.|WAR类型应用必须包含JDK和Tomcat。|
|400|InvalidNamespace.WithUppercase|This namespace does not support creating SAE apps because it contains uppercase letters.|命名空间不支持创建SAE应用，因为它带有大写字母。|
|400|LogService.ConfigQuotaExceed|The maximum number of Log Service configs is exceeded.|日志服务配置个数超过配额限制，请提工单解决。|
|400|LogService.InternalError|An exception occurred while calling Log Service. Please submit a ticket to solve the problem.|调用日志服务异常，请提工单解决。|
|400|LogService.LogDirInvalid|The log collection path is invalid.|日志采集路径不合法。|
|400|LogService.NotAvailable|Log Service is unavailable. Please activate Log Service first.|日志服务不可用，请先开通日志服务。|
|400|LogService.ProjectNumQuotaExceed|The maximum number of Log Service projects is exceeded.|日志服务项目个数超过配额限制，请提工单解决。|
|400|vswitch.not.exist|The specified VSwitch does not exist.|VSwitch不存在，请更换VSwitch。|
|400|user.indebt|The user has an outstanding payment.|您处于欠费状态。|
|400|NoComputeResourceQuota.App.Exceed|You can create %s instances for each application. Please submit a ticket to raise the quota.|每个应用只允许创建%s个实例，请提交工单增加计算资源额度。|
|400|NoComputeResourceQuota.User.Exceed|Your account is limited to create %s instances. Please submit a ticket to raise the quota.|您的账户限额%s个实例，请提交工单增加计算资源额度。|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|VolumnPath.Conflict|Conflict between log collection directory and persistent storage directory.|日志采集目录与持久化存储目录冲突。|
|400|MountConflict.ConfigMap|Conflict detected for ConfigMap path %s.|ConfigMap挂载路径%s存在冲突。|
|400|NotFound.ConfigMap|The ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）。|
|400|NotFound.ConfigMapKey|The key %s of ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）的Key %s。|
|400|Sls.Config.Mixed.Multi.Project|The specified Config contains multiple projects.|您输入的SLS Config中指定了多个Project。|
|400|Sls.Config.User.Defined.Missing.Logstore.Info|The specified Config is invalid. Both Project and Logstore must be specified.|您输入的SLS Config为自定义SLS配置，但是只有Project配置，缺失Logstore配置。|
|400|Sls.Config.User.Defined.Missing.Project.Info|The specified Config is invalid. Both Project and Logstore must be specified.|您输入的SLS Config为自定义SLS配置，但是只有Logstore配置，缺失Project配置。|
|400|Sls.Logstore.Name.Invalid|The specified name of Logstore is invalid. The Logstore name must not contain the prefix "sae-".|您输入的SLS Logstore名称不合法，前缀包含了"sae-"，会与SAE自动创建的Logstore混淆。|
|400|Sls.Logstore.User.Defined.Not.Exist|The user defined Logstore does not exist.|您输入的自建Logstore不存在。|
|400|Sls.Project.Name.Invalid|The specified project name is invalid. The project name must not contain the prefix "sae-".|您输入的SLS Project名称不合法，前缀包含了"sae-"，会与SAE自动创建的Project混淆。|
|400|Sls.Project.User.Defined.Not.Exist|The user defined project does not exist.|您输入的自建Project不存在。|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|
|404|InvalidVpcId.NotFound|The specified VpcId does not exist.|指定的VpcId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

