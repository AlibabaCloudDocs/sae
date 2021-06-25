# CreateConfigMap

调用CreateConfigMap接口创建命名空间中的ConfigMap实例。ConfigMap是一种用于存储应用所需配置信息的资源类型，它将配置和运行的镜像解耦，使应用程序具有更强的移植性。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateConfigMap&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
POST /pop/v1/sam/configmap/configMap HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|Name|String|Query|是|name|ConfigMap实例名称。 |
|NamespaceId|String|Query|是|cn-hangzhou|ConfigMap实例所在命名空间ID。 |
|Data|String|FormData|是|\{"env.home": "/root", "env.shell": "/bin/sh"\}|ConfigMap实例名称。格式如下：

 \{"k1":"v1", "k2":"v2"\}

 k表示键，v表示值。关于配置项的更多信息，请参见[管理和使用配置项](~~171326~~)。 |
|Description|String|Query|否|test-desc|描述信息。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|ConfigMapId|Long|1|创建成功的ConfigMap实例ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|创建ConfigMap实例是否成功。取值说明如下：

 -   **true**：表示创建成功。
-   **false**：表示创建失败。 |

## 示例

请求示例

```
POST /pop/v1/sam/configmap/configMap?Name=name&NamespaceId=cn-hangzhou&Description=test-desc HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

Data={"env.home": "/root", "env.shell": "/bin/sh"}

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateConfigMapResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <ConfigMapId>1</ConfigMapId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</CreateConfigMapResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : {
    "ConfigMapId" : 1
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|Exceed.ConfigMap|Too many ConfigMap objects have been created in the namespace.|命名空间中创建的ConfigMap对象过多。|
|500|OperationFailed.RPCError|Internal RPC request processing error.|内部RPC请求处理报错。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

