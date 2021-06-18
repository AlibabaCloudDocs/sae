# DescribeApplicationConfig

调用DescribeApplicationConfig接口获取应用配置信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationConfig&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/describeApplicationConfig HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|VersionId|String|Query|否|0026ff7f-2b57-4127-bdd0-9bf202bb\*\*\*\*|版本ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|01CF26C7-00A3-4AA6-BA76-7E95F2A3\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|ac1a0b2215622246421415014e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |应用信息。 |
|VpcId|String|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |
|Readiness|String|\{"exec":\{"command":\["curl http://localhost:8080"\]\},"initialDelaySeconds":20,"timeoutSeconds":5\}|应用业务就绪检查，即Readiness配置。 |
|ConfigMapMountDesc|Array of ConfigMapMountDesc| |ConfigMap信息。 |
|Key|String|k1|ConfigMap键值对。 |
|ConfigMapName|String|test|ConfigMap名称。 |
|MountPath|String|/tmp|容器挂载路径。 |
|ConfigMapId|Long|1|ConfigMap ID。 |
|SecurityGroupId|String|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |
|BatchWaitTime|Integer|10|分批发布时批次间的等待时间，单位为秒。 |
|Jdk|String|Open JDK 8|应用使用的JDK版本信息。 |
|ImageUrl|String|docker.io/library/nginx:1.14.2|镜像地址。 |
|SlsConfigs|String|\[\{\\"logDir\\":\\"/root/logs/hsf.log\\"\}\]|文件日志采集配置。 |
|Liveness|String|\{"exec":\{"command":\["curl http://localhost:8080"\]\},"initialDelaySeconds":20,"timeoutSeconds":3\}|应用实例存活检查，即Liveness配置。 |
|Tags|Array of Tag| |标签信息。 |
|Key|String|k1|标签键。 |
|Value|String|v1|标签值。 |
|PackageUrl|String|https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S\_APP\_ID/d4c97c37-aba3-403e-ae1e-6f7d8742\*\*\*\*/hello-edas.war|应用部署包地址。 |
|PackageType|String|War|应用部署类型。 |
|PreStop|String|\{"exec":\{"command":\["cat","/etc/group"\]\}\}|停止前执行的脚本。 |
|PackageVersion|String|1.0|应用部署包版本。 |
|JarStartArgs|String|start|JAR包部署应用的Args设置。 |
|AppName|String|demo-app|应用名称。 |
|AppId|String|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|JarStartOptions|String|-Dtest=true|JAR包部署应用的Options设置。 |
|Replicas|Integer|2|应用实例个数。 |
|MinReadyInstances|Integer|1|最小存活实例数。 |
|Memory|Integer|2048|应用内存规格，单位：MB。 |
|PhpConfig|String|k1=v1|PHP配置文件内容。 |
|PhpConfigLocation|String|/usr/local/etc/php/php.ini|PHP应用启动配置挂载路径。 |
|PostStart|String|\{"exec":\{"command":\["cat","/etc/group"\]\}\}|启动后执行的脚本。 |
|TerminationGracePeriodSeconds|Integer|10|优雅下线超时时间，默认为30，单位为秒。取值范围为1~60。 |
|CommandArgs|String|\["-c","echo 1234"\]|应用容器启动命令参数。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|MountHost|String|example.com|NAS在当前vSwtich上的挂载点Host。 |
|TomcatConfig|String|\{"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false\}|Tomcat文件配置。 |
|RegionId|String|cn-beijing|地域ID。 |
|VSwitchId|String|vsw-2ze559r1z1bpwqxwp\*\*\*\*|VSwitch ID。 |
|Cpu|Integer|1000|应用CPU规格，单位：毫核。1核=1000毫核。 |
|Envs|String|\[\{"name":"TEST\_ENV\_KEY","value":"TEST\_ENV\_VAR"\}\]|环境变量。 |
|MountDesc|Array of MountDesc| |挂载描述信息。 |
|MountPath|String|/tmp|容器挂载路径。 |
|NasPath|String|/|NAS相对文件目录。 |
|EnableAhas|String|true|是否接入AHAS。取值说明如下：

 -   **true**：表示接入AHAS。
-   **false**：表示不接入AHAS。 |
|CustomHostAlias|String|\[\{"hostName":"test.host.name","ip":"0.0.0.0"\}\]|Hosts绑定设置。 |
|WebContainer|String|apache-tomcat-7.0.91|部署时设置的WebContainer。 |
|Command|String|/bin/bash|应用容器启动命令。 |
|WarStartOptions|String|custom-option|WAR包启动应用选项。应用默认启动命令：`java $JAVA_OPTS $CATALINA_OPTS -Options org.apache.catalina.startup.Bootstrap "$@" start`。 |
|PhpArmsConfigLocation|String|/usr/local/etc/php/conf.d/arms.ini|PHP应用监控挂载路径。 |
|NasId|String|AKSN89\*\*|NAS ID。 |
|OssAkId|String|xxxxxx|OSS读写的AccessKey ID。 |
|OssAkSecret|String|xxxxxx|OSS读写的AccessKey Secret。 |
|OssMountDescs|Array of ossMountDesc| |OSS挂载描述信息。 |
|bucketName|String|oss-bucket|Bucket名称。 |
|bucketPath|String|data/user.data|您在OSS创建的目录或OSS对象，如果OSS挂载目录不存在，会触发异常。 |
|mountPath|String|/usr/data/user.data|您在SAE的容器路径。如果路径已存在，为覆盖关系；如果路径不存在，会新建。 |
|readOnly|Boolean|true|容器路径是否对挂载目录资源有可读权限，取值如下：

 -   **true**：只读权限。
-   **false**：读写权限。 |
|EdasContainerVersion|String|3.5.3|EDAS应用环境版本。 |
|Timezone|String|Asia/Shanghai|时区，默认为**Asia/Shanghai**。 |
|AppDescription|String|示例应用|应用描述信息。 |
|AcrAssumeRoleArn|String|acs:ram::123456789012\*\*\*\*:role/adminrole|跨账号拉取镜像时所需的RAM角色的ARN。 |
|EnableGreyTagRoute|Boolean|false|是否启用流量灰度规则。该规则仅适用于Spring Cloud和Dubbo框架的应用。取值如下：

 -   **true**：启用灰度规则。
-   **false**：禁用灰度规则。 |
|MseApplicationId|String|xxxxxxx@xxxxx|对应MSE产品侧应用ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|获取应用配置信息是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/describeApplicationConfig?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69****&VersionId=0026ff7f-2b57-4127-bdd0-9bf202bb**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeApplicationConfigResponse>
    <RequestId>01CF26C7-00A3-4AA6-BA76-7E95F2A3****</RequestId>
    <Message>success</Message>
    <TraceId>ac1a0b2215622246421415014e****</TraceId>
    <Data>
        <VpcId>vpc-2ze0i263cnn311nvj****</VpcId>
        <Readiness>{"exec":{"command":["curl http://localhost:8080"]},"initialDelaySeconds":20,"timeoutSeconds":5}</Readiness>
        <ConfigMapMountDesc>
            <Key>k1</Key>
            <ConfigMapName>test</ConfigMapName>
            <MountPath>/tmp</MountPath>
            <ConfigMapId>1</ConfigMapId>
        </ConfigMapMountDesc>
        <SecurityGroupId>sg-wz969ngg2e49q5i4****</SecurityGroupId>
        <BatchWaitTime>10</BatchWaitTime>
        <Jdk>Open JDK 8</Jdk>
        <ImageUrl>docker.io/library/nginx:1.14.2</ImageUrl>
        <SlsConfigs>[{\"logDir\":\"/root/logs/hsf.log\"}]</SlsConfigs>
        <Liveness>{"exec":{"command":["curl http://localhost:8080"]},"initialDelaySeconds":20,"timeoutSeconds":3}</Liveness>
        <Tags>
            <Key>k1</Key>
            <Value>v1</Value>
        </Tags>
        <PackageUrl>https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S_APP_ID/d4c97c37-aba3-403e-ae1e-6f7d8742****/hello-edas.war</PackageUrl>
        <PackageType>War</PackageType>
        <PreStop>{"exec":{"command":["cat","/etc/group"]}}</PreStop>
        <PackageVersion>1.0</PackageVersion>
        <JarStartArgs>start</JarStartArgs>
        <AppName>demo-app</AppName>
        <AppId>7171a6ca-d1cd-4928-8642-7d5cfe69****</AppId>
        <JarStartOptions>-Dtest=true</JarStartOptions>
        <Replicas>2</Replicas>
        <MinReadyInstances>1</MinReadyInstances>
        <Memory>2048</Memory>
        <PhpConfig>k1=v1</PhpConfig>
        <PhpConfigLocation>/usr/local/etc/php/php.ini</PhpConfigLocation>
        <PostStart>{"exec":{"command":["cat","/etc/group"]}}</PostStart>
        <TerminationGracePeriodSeconds>10</TerminationGracePeriodSeconds>
        <CommandArgs>["-c","echo 1234"]</CommandArgs>
        <NamespaceId>cn-beijing:test</NamespaceId>
        <MountHost>example.com</MountHost>
        <TomcatConfig>{"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false}</TomcatConfig>
        <RegionId>cn-beijing</RegionId>
        <VSwitchId>vsw-2ze559r1z1bpwqxwp****</VSwitchId>
        <Cpu>1000</Cpu>
        <Envs>[{"name":"TEST_ENV_KEY","value":"TEST_ENV_VAR"}]</Envs>
        <MountDesc>
            <MountPath>/tmp</MountPath>
            <NasPath>/</NasPath>
        </MountDesc>
        <EnableAhas>true</EnableAhas>
        <CustomHostAlias>[{"hostName":"test.host.name","ip":"0.0.0.0"}]</CustomHostAlias>
        <WebContainer>apache-tomcat-7.0.91</WebContainer>
        <Command>/bin/bash</Command>
        <WarStartOptions>custom-option</WarStartOptions>
        <PhpArmsConfigLocation>/usr/local/etc/php/conf.d/arms.ini</PhpArmsConfigLocation>
        <NasId>AKSN89**</NasId>
        <OssAkId>xxxxxx</OssAkId>
        <OssAkSecret>xxxxxx</OssAkSecret>
        <OssMountDescs>
            <bucketName>oss-bucket</bucketName>
            <bucketPath>data/user.data</bucketPath>
            <mountPath>/usr/data/user.data</mountPath>
            <readOnly>true</readOnly>
        </OssMountDescs>
        <EdasContainerVersion>3.5.3</EdasContainerVersion>
        <Timezone>Asia/Shanghai</Timezone>
        <AppDescription>示例应用</AppDescription>
        <AcrAssumeRoleArn>acs:ram::123456789012****:role/adminrole</AcrAssumeRoleArn>
        <EnableGreyTagRoute>false</EnableGreyTagRoute>
        <MseApplicationId>xxxxxxx@xxxxx</MseApplicationId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeApplicationConfigResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "01CF26C7-00A3-4AA6-BA76-7E95F2A3****",
  "Message" : "success",
  "TraceId" : "ac1a0b2215622246421415014e****",
  "Data" : {
    "VpcId" : "vpc-2ze0i263cnn311nvj****",
    "Readiness" : "{\"exec\":{\"command\":[\"curl http://localhost:8080\"]},\"initialDelaySeconds\":20,\"timeoutSeconds\":5}",
    "ConfigMapMountDesc" : [ {
      "Key" : "k1",
      "ConfigMapName" : "test",
      "MountPath" : "/tmp",
      "ConfigMapId" : 1
    } ],
    "SecurityGroupId" : "sg-wz969ngg2e49q5i4****",
    "BatchWaitTime" : 10,
    "Jdk" : "Open JDK 8",
    "ImageUrl" : "docker.io/library/nginx:1.14.2",
    "SlsConfigs" : "[{\\\"logDir\\\":\\\"/root/logs/hsf.log\\\"}]",
    "Liveness" : "{\"exec\":{\"command\":[\"curl http://localhost:8080\"]},\"initialDelaySeconds\":20,\"timeoutSeconds\":3}",
    "Tags" : [ {
      "Key" : "k1",
      "Value" : "v1"
    } ],
    "PackageUrl" : "https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S_APP_ID/d4c97c37-aba3-403e-ae1e-6f7d8742****/hello-edas.war",
    "PackageType" : "War",
    "PreStop" : "{\"exec\":{\"command\":[\"cat\",\"/etc/group\"]}}",
    "PackageVersion" : "1.0",
    "JarStartArgs" : "start",
    "AppName" : "demo-app",
    "AppId" : "7171a6ca-d1cd-4928-8642-7d5cfe69****",
    "JarStartOptions" : "-Dtest=true",
    "Replicas" : 2,
    "MinReadyInstances" : 1,
    "Memory" : 2048,
    "PhpConfig" : "k1=v1",
    "PhpConfigLocation" : "/usr/local/etc/php/php.ini",
    "PostStart" : "{\"exec\":{\"command\":[\"cat\",\"/etc/group\"]}}",
    "TerminationGracePeriodSeconds" : 10,
    "CommandArgs" : "[\"-c\",\"echo 1234\"]",
    "NamespaceId" : "cn-beijing:test",
    "MountHost" : "example.com",
    "TomcatConfig" : "{\"useDefaultConfig\":false,\"contextInputType\":\"custom\",\"contextPath\":\"hello\",\"httpPort\":8088,\"maxThreads\":400,\"uriEncoding\":\"UTF-8\",\"useBodyEncoding\":true,\"useAdvancedServerXml\":false}",
    "RegionId" : "cn-beijing",
    "VSwitchId" : "vsw-2ze559r1z1bpwqxwp****",
    "Cpu" : 1000,
    "Envs" : "[{\"name\":\"TEST_ENV_KEY\",\"value\":\"TEST_ENV_VAR\"}]",
    "MountDesc" : [ {
      "MountPath" : "/tmp",
      "NasPath" : "/"
    } ],
    "EnableAhas" : "true",
    "CustomHostAlias" : "[{\"hostName\":\"test.host.name\",\"ip\":\"0.0.0.0\"}]",
    "WebContainer" : "apache-tomcat-7.0.91",
    "Command" : "/bin/bash",
    "WarStartOptions" : "custom-option",
    "PhpArmsConfigLocation" : "/usr/local/etc/php/conf.d/arms.ini",
    "NasId" : "AKSN89**",
    "OssAkId" : "xxxxxx",
    "OssAkSecret" : "xxxxxx",
    "OssMountDescs" : [ {
      "bucketName" : "oss-bucket",
      "bucketPath" : "data/user.data",
      "mountPath" : "/usr/data/user.data",
      "readOnly" : true
    } ],
    "EdasContainerVersion" : "3.5.3",
    "Timezone" : "Asia/Shanghai",
    "AppDescription" : "示例应用",
    "AcrAssumeRoleArn" : "acs:ram::123456789012****:role/adminrole",
    "EnableGreyTagRoute" : false,
    "MseApplicationId" : "xxxxxxx@xxxxx"
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|404|InvalidAppId.NotFound|The specified AppId does not exist.|指定的AppId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

