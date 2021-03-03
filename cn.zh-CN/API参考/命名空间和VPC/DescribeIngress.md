# DescribeIngress

调用DescribeIngress接口查询Ingress配置详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeIngress&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/ingress/Ingress HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|IngressId|Long|Query|是|87|需要查询的Ingress ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|CertId|String|13623\*\*\*\*809\_16cad216b32\_845\_-419427029|证书ID。 |
|DefaultRule|Struct| |默认规则。 |
|AppId|String|395b60e4-0550-458d-9c54-a265d036\*\*\*\*|默认规则的应用。 |
|AppName|String|app1|默认规则的应用名称。 |
|ContainerPort|Integer|8080|默认规则应用的后端端口。 |
|Description|String|ingress-sae-test|Ingress描述信息。 |
|Id|Long|87|Ingress ID。 |
|ListenerPort|Integer|443|SLB监听端口。 |
|Name|String|sae-test|Ingress名称 |
|NamespaceId|String|cn-beijing:sae-test|命名空间ID。 |
|Rules|Array of Rule| |转发规则。 |
|AppId|String|395b60e4-0550-458d-9c54-a265d036\*\*\*\*|目标应用ID。 |
|AppName|String|app1|目标应用名称。 |
|ContainerPort|Integer|8080|应用后端端口。 |
|Domain|String|edas.site|应用域名。 |
|Path|String|/path1|URL路径。 |
|SlbId|String|lb-uf62\*\*\*\*6d13tq2u5|SLB ID。 |
|SlbType|String|internet|SLB类型。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|查询Ingress详情是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |
|TraceId|String|0a981dd515966966104121683d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/ingress/Ingress?RegionId=cn-beijing&IngressId=87
```

正常返回示例

`XML`格式

```
<DescribeIngressResponse>
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <TraceId>0a981dd515966966104121683d****</TraceId>
      <Data>
            <SlbId>lb-uf62****6d13tq2u5</SlbId>
            <DefaultRule>
                  <AppId>395b60e4-0550-458d-9c54-a265d036****</AppId>
                  <ContainerPort>8080</ContainerPort>
                  <AppName>app1</AppName>
            </DefaultRule>
            <ListenerPort>443</ListenerPort>
            <Description>ingress-sae-test</Description>
            <CertId>13623****809_16cad216b32_845_-419427029</CertId>
            <NamespaceId>cn-beijing:sae-test</NamespaceId>
            <Id>87</Id>
            <Rules>
                  <Path>/path1</Path>
                  <ContainerPort>8080</ContainerPort>
                  <AppId>395b60e4-0550-458d-9c54-a265d036****</AppId>
                  <Domain>edas.site</Domain>
                  <AppName>app1</AppName>
            </Rules>
            <SlbType>internet</SlbType>
            <Name>sae-test</Name>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</DescribeIngressResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a981dd515966966104121683d****",
    "Data": {
        "SlbId": "lb-uf62****6d13tq2u5",
        "DefaultRule": {
            "AppId": "395b60e4-0550-458d-9c54-a265d036****",
            "ContainerPort": 8080,
            "AppName": "app1"
        },
        "ListenerPort": 443,
        "Description": "ingress-sae-test",
        "CertId": "13623****809_16cad216b32_845_-419427029",
        "NamespaceId": "cn-beijing:sae-test",
        "Id": 87,
        "Rules": {
            "Path": "/path1",
            "ContainerPort": 8080,
            "AppId": "395b60e4-0550-458d-9c54-a265d036****",
            "Domain": "edas.site",
            "AppName": "app1"
        },
        "SlbType": "internet",
        "Name": "sae-test"
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

