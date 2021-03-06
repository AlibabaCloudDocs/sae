# UpdateIngress

调用UpdateIngress接口更新Ingress实例配置。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateIngress&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
PUT /pop/v1/sam/ingress/Ingress HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|IngressId|Long|Query|是|87|Ingress ID。 |
|CertId|String|Query|否|136\*\*\*\*\*\*\*\*3809\_16f8e549a20\_-175189789\_122xxxxx10|证书ID。 |
|Description|String|Query|否|ingress-sae-test|描述信息。 |
|ListenerPort|String|Query|否|443|SLB监听端口。 |
|DefaultRule|String|Query|否|\{"appId":"\*\*\*\*\*\*\*\*-0550-458d-9c54-a265d036d8c8","containerPort":8080\}|默认规则。 |
|Rules|String|FormData|否|\[\{"appId":"\*\*\*\*\*\*\*\*-0550-458d-9c54-a265d036d8c8","containerPort":8080,"domain":"www.edas.site","path":"/path1"\},\{"appId":"xxxxxxx-d25b-47cf-87fe-497565d20935","containerPort":8080,"domain":"edas.site","path":"/path2"\}\]|转发规则。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID。 |
|Data|Object| |返回结果。 |
|IngressId|Long|87|Ingress ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误 |
|Success|Boolean|true|更新Ingress实例配置是否成功。取值说明如下：

 -   **true**：表示更新成功。
-   **false**：表示更新失败。 |

## 示例

请求示例

```
PUT /pop/v1/sam/ingress/Ingress?IngressId=87&CertId=136********3809_16f8e549a20_-175189789_122xxxxx10&Description=ingress-sae-test&ListenerPort=443&DefaultRule={"appId":"********-0550-458d-9c54-a265d036d8c8","containerPort":8080} HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

Rules=[{"appId":"********-0550-458d-9c54-a265d036d8c8","containerPort":8080,"domain":"www.edas.site","path":"/path1"},{"appId":"xxxxxxx-d25b-47cf-87fe-497565d20935","containerPort":8080,"domain":"edas.site","path":"/path2"}]

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UpdateIngressResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <IngressId>87</IngressId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</UpdateIngressResponse>
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
    "IngressId" : 87
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
|400|Exceed.IngressRule|The number of Ingress related rules must be less than or equal to 40.|Ingress配置对应规则不可超过40条。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

