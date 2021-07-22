# DescribeIngress

调用DescribeIngress接口查询Ingress配置详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeIngress&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

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
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a981dd515966966104121683d\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|SlbId|String|lb-uf62\*\*\*\*6d13tq2u5|SLB ID。 |
|NamespaceId|String|cn-beijing:sae-test|命名空间ID。 |
|Description|String|ingress-sae-test|Ingress描述信息。 |
|ListenerPort|Integer|443|SLB监听端口。 |
|SlbType|String|internet|SLB类型。取值说明如下：

 -   **internet**：公网。
-   **intranet**：私网。 |
|CertId|String|13623\*\*\*\*809\_16cad216b32\_845\_-419427029|证书ID。 |
|Name|String|sae-test|Ingress名称。 |
|DefaultRule|Object| |默认规则。 |
|ContainerPort|Integer|8080|默认规则应用的后端端口。 |
|AppName|String|app1|默认规则的应用名称。 |
|AppId|String|395b60e4-0550-458d-9c54-a265d036\*\*\*\*|默认规则的应用。 |
|Rules|Array of Rule| |转发规则。 |
|AppName|String|app1|目标应用名称。 |
|ContainerPort|Integer|8080|应用后端端口。 |
|Domain|String|edas.site|应用域名。 |
|AppId|String|395b60e4-0550-458d-9c54-a265d036\*\*\*\*|目标应用ID。 |
|Path|String|/path1|URL路径。 |
|Id|Long|87|Ingress ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|查询Ingress详情是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/ingress/Ingress?IngressId=87 HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeIngressResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a981dd515966966104121683d****</TraceId>
    <Data>
        <SlbId>lb-uf62****6d13tq2u5</SlbId>
        <NamespaceId>cn-beijing:sae-test</NamespaceId>
        <Description>ingress-sae-test</Description>
        <ListenerPort>443</ListenerPort>
        <SlbType>internet</SlbType>
        <CertId>13623****809_16cad216b32_845_-419427029</CertId>
        <Name>sae-test</Name>
        <DefaultRule>
            <ContainerPort>8080</ContainerPort>
            <AppName>app1</AppName>
            <AppId>395b60e4-0550-458d-9c54-a265d036****</AppId>
        </DefaultRule>
        <Rules>
            <AppName>app1</AppName>
            <ContainerPort>8080</ContainerPort>
            <Domain>edas.site</Domain>
            <AppId>395b60e4-0550-458d-9c54-a265d036****</AppId>
            <Path>/path1</Path>
        </Rules>
        <Id>87</Id>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeIngressResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a981dd515966966104121683d****",
  "Data" : {
    "SlbId" : "lb-uf62****6d13tq2u5",
    "NamespaceId" : "cn-beijing:sae-test",
    "Description" : "ingress-sae-test",
    "ListenerPort" : 443,
    "SlbType" : "internet",
    "CertId" : "13623****809_16cad216b32_845_-419427029",
    "Name" : "sae-test",
    "DefaultRule" : {
      "ContainerPort" : 8080,
      "AppName" : "app1",
      "AppId" : "395b60e4-0550-458d-9c54-a265d036****"
    },
    "Rules" : [ {
      "AppName" : "app1",
      "ContainerPort" : 8080,
      "Domain" : "edas.site",
      "AppId" : "395b60e4-0550-458d-9c54-a265d036****",
      "Path" : "/path1"
    } ],
    "Id" : 87
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

