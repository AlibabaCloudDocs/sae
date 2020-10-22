# CreateConfigMap

调用CreateConfigMap接口创建命名空间中的ConfigMap实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateConfigMap&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/sam/configmap/configMap HTTPS|HTTP
```

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Data|String|是|\{"k1":"v1", "k2":"v2"\}|ConfigMap实例数据。 |
|Name|String|是|name|ConfigMap实例名称。 |
|NamespaceId|String|是|cn-hangzhou|ConfigMap实例所在命名空间ID。 |
|Description|String|否|用于测试|描述信息。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。 |
|Data|Struct| |返回结果。 |
|ConfigMapId|Long|1|创建成功的ConfigMap实例ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|创建ConfigMap实例是否成功。取值说明如下：

 -   **true**：表示创建成功。
-   **false**：表示创建失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID。 |

## 示例

请求示例

```
POST /pop/v1/sam/configmap/configMap HTTP/1.1
<公共请求头>
{
"Data": "{"k1":"v1", "k2":"v2"}",
"Name": "name",
"NamespaceId": "cn-hangzhou"
}
```

正常返回示例

`XML` 格式

```
<CreateConfigMappResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <ConfigMapId>1</ConfigMapId>
      </Data>
      <ErrorCode>success</ErrorCode>
      <Code>200</Code>
      <Success>true</Success>
</CreateConfigMappResponse>
```

`JSON` 格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "ConfigMapId": 1
    },
    "ErrorCode": "success",
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|Exceed.ConfigMap|Too many ConfigMap objects have been created in the namespace.|命名空间中创建的ConfigMap对象过多。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

