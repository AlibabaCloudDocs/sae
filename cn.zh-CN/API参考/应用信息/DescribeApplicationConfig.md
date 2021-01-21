# DescribeApplicationConfig

调用DescribeApplicationConfig接口获取应用配置信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationConfig&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/app/describeApplicationConfig HTTP|HTTPS
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|VersionId|String|Query|否|0026ff7f-2b57-4127-bdd0-9bf202bb\*\*\*\*|版本ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |应用信息。 |
|AcrAssumeRoleArn|String|acs:ram::123456789012\*\*\*\*:role/adminrole|跨账号拉取镜像时所需的RAM角色的ARN。 |
|AppDescription|String|示例应用|应用描述信息。 |
|AppId|String|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|AppName|String|demo-app|应用名称。 |
|BatchWaitTime|Integer|10|分批发布时批次间的等待时间，单位为秒。 |
|Command|String|/bin/bash|应用容器启动命令。 |
|CommandArgs|String|\["-c","echo 1234"\]|应用容器启动命令参数。 |
|ConfigMapMountDesc|Array of ConfigMapMountDesc| |ConfigMap信息。 |
|ConfigMapId|Long|1|ConfigMap ID。 |
|ConfigMapName|String|test|ConfigMap名称。 |
|Key|String|k1|ConfigMap键值对。 |
|MountPath|String|/tmp|容器挂载路径。 |
|Cpu|Integer|1000|应用CPU规格，单位：毫核。1核=1000毫核。 |
|CustomHostAlias|String|\[\{"hostName":"test.host.name","ip":"0.0.0.0"\}\]|Hosts绑定设置。 |
|EdasContainerVersion|String|3.5.3|EDAS应用环境版本。 |
|EnableAhas|String|true|是否接入AHAS。取值说明如下：

 -   **true**：表示接入AHAS。
-   **false**：表示不接入AHAS。 |
|Envs|String|\[\{"name":"TEST\_ENV\_KEY","value":"TEST\_ENV\_VAR"\}\]|环境变量。 |
|ImageUrl|String|docker.io/library/nginx:1.14.2|镜像地址。 |
|JarStartArgs|String|start|JAR包部署应用的Args设置。 |
|JarStartOptions|String|-Dtest=true|JAR包部署应用的Options设置。 |
|Jdk|String|Open JDK 8|应用使用的JDK版本信息。 |
|Liveness|String|\{"exec":\{"command":\["curl http://localhost:8080"\]\},"initialDelaySeconds":20,"timeoutSeconds":3\}|应用实例存活检查，即Liveness配置。 |
|Memory|Integer|2048|应用内存规格，单位：MB。 |
|MinReadyInstances|Integer|1|最小存活实例数。 |
|MountDesc|Array of MountDesc| |挂载描述信息。 |
|MountPath|String|/tmp|容器挂载路径。 |
|NasPath|String|/|NAS相对文件目录。 |
|MountHost|String|example.com|NAS在当前VSwtich上的挂载点Host。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|NasId|String|AKSN89\*\*|NAS ID。 |
|PackageType|String|War|应用部署类型。 |
|PackageUrl|String|https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S\_APP\_ID/d4c97c37-aba3-403e-ae1e-6f7d8742\*\*\*\*/hello-edas.war|应用部署包地址。 |
|PackageVersion|String|1.0|应用部署包版本。 |
|PhpArmsConfigLocation|String|/usr/local/etc/php/conf.d/arms.ini|PHP应用监控挂载路径。 |
|PhpConfig|String|k1=v1|PHP配置文件内容。 |
|PhpConfigLocation|String|/usr/local/etc/php/php.ini|PHP应用启动配置挂载路径。 |
|PostStart|String|\{"exec":\{"command":\["cat","/etc/group"\]\}\}|启动后执行的脚本。 |
|PreStop|String|\{"exec":\{"command":\["cat","/etc/group"\]\}\}|停止前执行的脚本。 |
|Readiness|String|\{"exec":\{"command":\["curl http://localhost:8080"\]\},"initialDelaySeconds":20,"timeoutSeconds":5\}|应用业务就绪检查，即Readiness配置。 |
|RegionId|String|cn-beijing|地域ID。 |
|Replicas|Integer|2|应用实例个数。 |
|SecurityGroupId|String|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |
|SlsConfigs|String|\[\{\\"logDir\\":\\"/root/logs/hsf.log\\"\}\]|文件日志采集配置。 |
|Tags|Array of Tag| |标签信息。 |
|Key|String|k1|标签键。 |
|Value|String|v1|标签值。 |
|TerminationGracePeriodSeconds|Integer|10|优雅下线超时时间，默认为30，单位为秒。取值范围为1~60。 |
|Timezone|String|Asia/Shanghai|时区，默认为**Asia/Shanghai**。 |
|TomcatConfig|String|\{"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false\}|Tomcat文件配置。 |
|VSwitchId|String|vsw-2ze559r1z1bpwqxwp\*\*\*\*|VSwitch ID。 |
|VpcId|String|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |
|WarStartOptions|String|custom-option|WAR包启动应用选项。应用默认启动命令：`java $JAVA_OPTS $CATALINA_OPTS -Options org.apache.catalina.startup.Bootstrap "$@" start`。 |
|WebContainer|String|apache-tomcat-7.0.91|部署时设置的WebContainer。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|01CF26C7-00A3-4AA6-BA76-7E95F2A3\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用配置信息是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|ac1a0b2215622246421415014e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/describeApplicationConfig?RegionId=cn-beijing&AppId=7171a6ca-d1cd-4928-8642-7d5cfe69****
```

正常返回示例

`XML` 格式

```
<DescribeApplicationConfigResponse>
      <RequestId>01CF26C7-00A3-4AA6-BA76-7E95F2A3****</RequestId>
      <Message>success</Message>
      <TraceId>ac1a0b2215622246421415014e****</TraceId>
      <Data>
            <Timezone>Asia/Shanghai</Timezone>
            <PhpConfig>k1=v1</PhpConfig>
            <AppDescription>示例应用</AppDescription>
            <NasId>AKSN89**</NasId>
            <MountDesc>
                  <MountPath>/tmp</MountPath>
                  <NasPath>/</NasPath>
            </MountDesc>
            <Liveness>{"exec":{"command":["curl http://localhost:8080"]},"initialDelaySeconds":20,"timeoutSeconds":3}</Liveness>
            <WarStartOptions>custom-option</WarStartOptions>
            <Memory>2048</Memory>
            <WebContainer>apache-tomcat-7.0.91</WebContainer>
            <SlsConfigs>[{\"logDir\":\"/root/logs/hsf.log\"}]</SlsConfigs>
            <Cpu>1000</Cpu>
            <PackageVersion>1</PackageVersion>
            <AppName>demo-app</AppName>
            <Jdk>Open JDK 8</Jdk>
            <JarStartArgs>start</JarStartArgs>
            <Readiness>{"exec":{"command":["curl http://localhost:8080"]},"initialDelaySeconds":20,"timeoutSeconds":5}</Readiness>
            <PreStop>{"exec":{"command":["cat","/etc/group"]}}</PreStop>
            <MinReadyInstances>1</MinReadyInstances>
            <PhpArmsConfigLocation>/usr/local/etc/php/conf.d/arms.ini</PhpArmsConfigLocation>
            <PackageType>War</PackageType>
            <Tags>
                  <Value>v1</Value>
                  <Key>k1</Key>
            </Tags>
            <CommandArgs>["-c","echo 1234"]</CommandArgs>
            <AcrAssumeRoleArn>acs:ram::123456789012****:role/adminrole</AcrAssumeRoleArn>
            <TerminationGracePeriodSeconds>10</TerminationGracePeriodSeconds>
            <SecurityGroupId>sg-wz969ngg2e49q5i4****</SecurityGroupId>
            <VSwitchId>vsw-2ze559r1z1bpwqxwp****</VSwitchId>
            <Envs>[{"name":"TEST_ENV_KEY","value":"TEST_ENV_VAR"}]</Envs>
            <ImageUrl>docker.io/library/nginx:1.14.2</ImageUrl>
            <PostStart>{"exec":{"command":["cat","/etc/group"]}}</PostStart>
            <JarStartOptions>-Dtest=true</JarStartOptions>
            <MountHost>example.com</MountHost>
            <Replicas>2</Replicas>
            <CustomHostAlias>[{"hostName":"test.host.name","ip":"0.0.0.0"}]</CustomHostAlias>
            <ConfigMapMountDesc>
                  <MountPath>/tmp</MountPath>
                  <ConfigMapId>1</ConfigMapId>
                  <ConfigMapName>test</ConfigMapName>
               <Key>k1</Key>
            </ConfigMapMountDesc>
            <VpcId>vpc-2ze0i263cnn311nvj****</VpcId>
            <AppId>7171a6ca-d1cd-4928-8642-7d5cfe69****</AppId>
            <Command>/bin/bash</Command>
            <EdasContainerVersion>3.5.3</EdasContainerVersion>
            <PackageUrl>https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S_APP_ID/d4c97c37-aba3-403e-ae1e-6f7d8742****/hello-edas.war</PackageUrl>
            <PhpConfigLocation>/usr/local/etc/php/php.ini</PhpConfigLocation>
            <BatchWaitTime>10</BatchWaitTime>
            <NamespaceId>cn-beijing:test</NamespaceId>
            <RegionId>cn-beijing</RegionId>
            <EnableAhas>true</EnableAhas>
            <TomcatConfig>{"useDefaultConfig":false,"contextInputType":"custom","contextPath":"hello","httpPort":8088,"maxThreads":400,"uriEncoding":"UTF-8","useBodyEncoding":true,"useAdvancedServerXml":false}</TomcatConfig>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</DescribeApplicationConfigResponse>
```

`JSON` 格式

```
{
    "RequestId": "01CF26C7-00A3-4AA6-BA76-7E95F2A3****",
    "Message": "success",
    "TraceId": "ac1a0b2215622246421415014e****",
    "Data": {
        "Timezone": "Asia/Shanghai",
        "PhpConfig": "k1=v1",
        "AppDescription": "示例应用",
        "NasId": "AKSN89**",
        "MountDesc": {
            "MountPath": "/tmp",
            "NasPath": "/"
        },
        "Liveness": "{\"exec\":{\"command\":[\"curl http://localhost:8080\"]},\"initialDelaySeconds\":20,\"timeoutSeconds\":3}",
        "WarStartOptions": "custom-option",
        "Memory": 2048,
        "WebContainer": "apache-tomcat-7.0.91",
        "SlsConfigs": "[{\\\"logDir\\\":\\\"/root/logs/hsf.log\\\"}]",
        "Cpu": 1000,
        "PackageVersion": 1,
        "AppName": "demo-app",
        "Jdk": "Open JDK 8",
        "JarStartArgs": "start",
        "Readiness": "{\"exec\":{\"command\":[\"curl http://localhost:8080\"]},\"initialDelaySeconds\":20,\"timeoutSeconds\":5}",
        "PreStop": "{\"exec\":{\"command\":[\"cat\",\"/etc/group\"]}}",
        "MinReadyInstances": 1,
        "PhpArmsConfigLocation": "/usr/local/etc/php/conf.d/arms.ini",
        "PackageType": "War",
        "Tags": {
            "Value": "v1",
            "Key": "k1"
        },
        "CommandArgs": "[\"-c\",\"echo 1234\"]",
        "AcrAssumeRoleArn": "acs:ram::123456789012****:role/adminrole",
        "TerminationGracePeriodSeconds": 10,
        "SecurityGroupId": "sg-wz969ngg2e49q5i4****",
        "VSwitchId": "vsw-2ze559r1z1bpwqxwp****",
        "Envs": "[{\"name\":\"TEST_ENV_KEY\",\"value\":\"TEST_ENV_VAR\"}]",
        "ImageUrl": "docker.io/library/nginx:1.14.2",
        "PostStart": "{\"exec\":{\"command\":[\"cat\",\"/etc/group\"]}}",
        "JarStartOptions": "-Dtest=true",
        "MountHost": "example.com",
        "Replicas": 2,
        "CustomHostAlias": "[{\"hostName\":\"test.host.name\",\"ip\":\"0.0.0.0\"}]",
        "ConfigMapMountDesc": {
            "MountPath": "/tmp",
            "ConfigMapId": 1,
            "ConfigMapName": "test",
            "Key": "k1"
        },
        "VpcId": "vpc-2ze0i263cnn311nvj****",
        "AppId": "7171a6ca-d1cd-4928-8642-7d5cfe69****",
        "Command": "/bin/bash",
        "EdasContainerVersion": "3.5.3",
        "PackageUrl": "https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S_APP_ID/d4c97c37-aba3-403e-ae1e-6f7d8742****/hello-edas.war",
        "PhpConfigLocation": "/usr/local/etc/php/php.ini",
        "BatchWaitTime": 10,
        "NamespaceId": "cn-beijing:test",
        "RegionId": "cn-beijing",
        "EnableAhas": true,
        "TomcatConfig": "{\"useDefaultConfig\":false,\"contextInputType\":\"custom\",\"contextPath\":\"hello\",\"httpPort\":8088,\"maxThreads\":400,\"uriEncoding\":\"UTF-8\",\"useBodyEncoding\":true,\"useAdvancedServerXml\":false}"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|404|InvalidAppId.NotFound|The specified AppId does not exist.|指定的AppId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

