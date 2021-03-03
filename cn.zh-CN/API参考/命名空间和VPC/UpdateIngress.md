# UpdateIngress

调用UpdateIngress接口更新Ingress实例配置。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateIngress&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

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
|Rules|String|Body|否|\[\{"appId":"\*\*\*\*\*\*\*\*-0550-458d-9c54-a265d036d8c8","containerPort":8080,"domain":"www.edas.site","path":"/path1"\},\{"appId":"xxxxxxx-d25b-47cf-87fe-497565d20935","containerPort":8080,"domain":"edas.site","path":"/path2"\}\]|转发规则。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|IngressId|Long|87|Ingress ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|更新Ingress实例配置是否成功。取值说明如下：

 -   **true**：表示更新成功。
-   **false**：表示更新失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID。 |

## 示例

请求示例

```
PUT /pop/v1/sam/ingress/Ingress?RegionId=cn-beijing&IngressId=87
```

正常返回示例

`XML`格式

```
<UpdateIngressResponse>
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <IngressId>87</IngressId>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</UpdateIngressResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "IngressId": 87
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
|400|Exceed.IngressRule|The number of Ingress related rules must be less than or equal to 40.|Ingress配置对应规则不可超过40条。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

