# DeleteConfigMap

调用DeleteConfigMap接口删除ConfigMap实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DeleteConfigMap&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
DELETE /pop/v1/sam/configmap/configMap HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|ConfigMapId|Long|Query|是|1|需要删除的ConfigMap实例ID。需要调用[ListNamespacedConfigMaps](~~176917~~)接口查看。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|ConfigMapId|Long|1|被删除的ConfigMap实例ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|删除ConfigMap实例是否成功。取值说明如下：

 -   **true**：表示删除实例成功。
-   **false**：表示删除实例失败。 |

## 示例

请求示例

```
DELETE /pop/v1/sam/configmap/configMap?ConfigMapId=1 HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DeleteConfigMapResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <ConfigMapId>1</ConfigMapId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DeleteConfigMapResponse>
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
|400|MountConflict.ConfigMap|Conflict detected for ConfigMap path %s.|ConfigMap挂载路径%s存在冲突。|
|400|NotFound.ConfigMap|The ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）。|
|400|NotFound.ConfigMapKey|The key %s of ConfigMap object \(ID: %s\) does not exist.|找不到ConfigMap对象（ID=%s）的Key %s。|
|400|DeleteFail.ConfigMapReferenced|Failed to delete the ConfigMap. It has been used by other applications.|删除ConfigMap失败，ConfigMap已被其他应用使用。|
|500|OperationFailed.RPCError|Internal RPC request processing error.|内部RPC请求处理报错。|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

