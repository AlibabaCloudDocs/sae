# ListIngresses

调用ListIngresses接口获取Ingress列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListIngresses&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/ingress/IngressList HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing|命名空间ID。 |
|AppId|String|Query|否|bbf3a590-6d13-46fe-8ca9-c947a20b\*\*\*\*|应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|IngressList|Array of Ingress| |Ingress列表。 |
|SlbId|String|lb-uf62\*\*\*\*6d13tq2u5|SLB ID。 |
|NamespaceId|String|cn-shanghai|命名空间ID。 |
|Description|String|test|描述信息。 |
|ListenerPort|String|9824|SLB监听端口。 |
|SlbType|String|internet|SLB类型。 |
|CertId|String|13624\*\*\*\*\*73809\_16f8e549a20\_1175189789\_12\*\*\*\*3210|证书ID。 |
|Name|String|test|Ingress名称。 |
|Id|Long|18|Ingress ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取Ingress列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/ingress/IngressList?NamespaceId=cn-beijing&AppId=bbf3a590-6d13-46fe-8ca9-c947a20b**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListIngressesResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <IngressList>
            <SlbId>lb-uf62****6d13tq2u5</SlbId>
            <NamespaceId>cn-shanghai</NamespaceId>
            <Description>test</Description>
            <ListenerPort>9824</ListenerPort>
            <SlbType>internet</SlbType>
            <CertId>13624*****73809_16f8e549a20_1175189789_12****3210</CertId>
            <Name>test</Name>
            <Id>18</Id>
        </IngressList>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListIngressesResponse>
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
    "IngressList" : [ {
      "SlbId" : "lb-uf62****6d13tq2u5",
      "NamespaceId" : "cn-shanghai",
      "Description" : "test",
      "ListenerPort" : "9824",
      "SlbType" : "internet",
      "CertId" : "13624*****73809_16f8e549a20_1175189789_12****3210",
      "Name" : "test",
      "Id" : 18
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

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

