# CreateIngress

调用CreateIngress接口创建一条路由规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateIngress&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/sam/ingress/Ingress HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|ListenerPort|Integer|Query|是|80|SLB监听端口，该端口不能被占用。 |
|NamespaceId|String|Query|是|cn-beijing:sae-test|应用所在命名空间ID，目前不支持跨命名空间的应用。 |
|Rules|String|Body|是|\[\{"appId":"395b\*\*\*\*-0550-458d-9c54-a265d036d8c8","containerPort":8080,"domain":"www.edas.site","path":"/path1"\},\{"appId":"666403ce-d25b-47cf-87fe-497565d2\*\*\*\*","containerPort":8080,"domain":"edas.site","path":"/path2"\}\]|转发规则。按照域名跟路径转发流量到指定应用。 |
|SlbId|String|Query|是|lb-uf62\*\*\*\*6d13tq2u5|Ingress所使用的SLB。 |
|Description|String|Query|否|ingress-for-sae-test|Ingress描述信息。 |
|CertId|String|Query|否|1362\*\*\*\*\*\*373809\_\*\*\*\*\*\*\_841665875\_-419427029|HTTPS监听所使用的证书ID。 |
|DefaultRule|String|Query|否|\{"appId":"395b\*\*\*\*-0550-458d-9c54-a265d036d8c8","containerPort":8080\}|默认配置。按照IP访问的流量将被转发到这里。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|IngressId|Long|87|路由规则ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|创建路由规则是否成功。取值说明如下：

 -   **true**：表示更新成功。
-   **false**：表示更新失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
POST /pop/v1/sam/ingress/Ingress?RegionId=cn-hangzhou&NamespaceId=cn-hangzhou%3Asae-test&SlbId=lb-uf62****6d13tq2u5&ListenerPort=80
```

正常返回示例

`XML`格式

```
<CreateIngressResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <IngressId>87</IngressId>
      </Data>
      <ErrorCode>success</ErrorCode>
      <Code>200</Code>
      <Success>true</Success>
</CreateIngressResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "IngressId": 87
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
|400|Slb.NotFound|The SLB instance does not exist: slbId \[%s\]|SLB不存在：slbId\[%s\]。|
|400|Exceed.IngressRule|The number of Ingress related rules must be less than or equal to 40.|Ingress配置对应规则不可超过40条。|
|404|InvalidResponse.Api|The response of API %s is empty.|API返回数据为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

