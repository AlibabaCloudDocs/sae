# ListIngresses

调用ListIngresses接口获取Ingress列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListIngresses&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/ingress/IngressList HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|IngressList|Array of Ingress| |Ingress列表。 |
|CertId|String|13624\*\*\*\*\*73809\_16f8e549a20\_1175189789\_12\*\*\*\*3210|证书ID。 |
|Description|String|test|描述信息。 |
|Id|Long|18|Ingress ID。 |
|ListenerPort|String|9824|SLB监听端口。 |
|Name|String|test|Ingress名称。 |
|NamespaceId|String|cn-shanghai|命名空间ID。 |
|SlbId|String|lb-uf62\*\*\*\*6d13tq2u5|SLB ID。 |
|SlbType|String|internet|SLB类型。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取Ingress列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/ingress/IngressList?RegionId=cn-beijing&NamespaceId=cn-beijing
```

正常返回示例

`XML` 格式

```
<ListIngressesResponse>
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <IngressList>
                  <SlbId>lb-uf62****6d13tq2u5</SlbId>
                  <ListenerPort>9824</ListenerPort>
                  <Description>test</Description>
                  <CertId>13624*****73809_16f8e549a20_1175189789_12****3210</CertId>
                  <NamespaceId>cn-shanghai</NamespaceId>
                  <Id>18</Id>
                  <SlbType>internet</SlbType>
                  <Name>test</Name>
            </IngressList>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</ListIngressesResponse>
```

`JSON` 格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "IngressList": {
            "SlbId": "lb-uf62****6d13tq2u5",
            "ListenerPort": 9824,
            "Description": "test",
            "CertId": "13624*****73809_16f8e549a20_1175189789_12****3210",
            "NamespaceId": "cn-shanghai",
            "Id": 18,
            "SlbType": "internet",
            "Name": "test"
        }
    },
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

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

