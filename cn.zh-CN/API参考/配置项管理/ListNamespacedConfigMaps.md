# ListNamespacedConfigMaps

调用ListNamespacedConfigMaps接口获取命名空间内ConfigMap实例列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListNamespacedConfigMaps&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/configmap/listNamespacedConfigMaps HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-hangzhou|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|ConfigMaps|Array of ConfigMap| |ConfigMap实例列表。 |
|UpdateTime|Long|1593760185111|更新时间。 |
|Data|Map| |ConfigMap实例键值对数据。格式如下：

 \{"k1":"v1", "k2":"v2"\}

 k表示键，v表示值。关于配置项的更多信息，请参见[管理和使用配置项](~~171326~~)。 |
|NamespaceId|String|cn-hangzhou|命名空间ID。 |
|Description|String|test-desc|描述信息。 |
|CreateTime|Long|1593760185111|更新时间。 |
|RelateApps|Array of RelateApp| |关联应用。 |
|AppName|String|test-app|应用名称。 |
|AppId|String|f16b4000-9058-4c22-a49d-49a28f0b\*\*\*\*|应用ID。 |
|ConfigMapId|Long|1|ConfigMap实例ID。 |
|Name|String|test-name|ConfigMap实例名称。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|是否成功获取ConfigMap实例列表。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/configmap/listNamespacedConfigMaps?NamespaceId=cn-hangzhou HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListNamespacedConfigMapsResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <ConfigMaps>
            <UpdateTime>1593760185111</UpdateTime>
            <NamespaceId>cn-hangzhou</NamespaceId>
            <Description>test-desc</Description>
            <CreateTime>1593760185111</CreateTime>
            <RelateApps>
                <AppName>test-app</AppName>
                <AppId>f16b4000-9058-4c22-a49d-49a28f0b****</AppId>
            </RelateApps>
            <ConfigMapId>1</ConfigMapId>
            <Name>test-name</Name>
        </ConfigMaps>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListNamespacedConfigMapsResponse>
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
    "ConfigMaps" : [ {
      "UpdateTime" : 1593760185111,
      "NamespaceId" : "cn-hangzhou",
      "Description" : "test-desc",
      "CreateTime" : 1593760185111,
      "RelateApps" : [ {
        "AppName" : "test-app",
        "AppId" : "f16b4000-9058-4c22-a49d-49a28f0b****"
      } ],
      "ConfigMapId" : 1,
      "Name" : "test-name"
    } ]
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
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

