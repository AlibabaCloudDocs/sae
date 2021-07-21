# DescribeApplicationSlbs

调用DescribeApplicationSlbs接口获取应用SLB配置信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationSlbs&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/slb HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|017f39b8-dfa4-4e16-a84b-1dcee4b1\*\*\*\*|目标应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|Intranet|Array of Intranet| |内网SLB配置。 |
|HttpsCertId|String|1513561019707729\_16f37aae5f3\_-375882821\_-169099\*\*\*\*|HTTPS协议对应的阿里云证书ID。 |
|Protocol|String|TCP|支持的协议。 |
|TargetPort|Integer|8080|容器端口。 |
|Port|Integer|80|SLB监听端口。 |
|InternetIp|String|59.74.\*\*.\*\*|公网SLB地址。 |
|InternetSlbId|String|lb-uf6xc7wybefehnv45\*\*\*\*|公网SLB ID。 |
|Internet|Array of Internet| |公网SLB配置。 |
|HttpsCertId|String|1513561019707729\_16f37aae5f3\_-375882821\_-169099\*\*\*\*|HTTPS协议对应的阿里云证书ID。 |
|Protocol|String|TCP|支持的协议。 |
|TargetPort|Integer|8080|容器端口。 |
|Port|Integer|80|SLB监听端口。 |
|IntranetSlbId|String|lb-uf6xc7wybefehnv45\*\*\*\*|内网SLB ID。 |
|IntranetIp|String|192.168.0.0|内网SLB地址。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取应用SLB配置信息是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/slb?AppId=017f39b8-dfa4-4e16-a84b-1dcee4b1**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeApplicationSlbsResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <Intranet>
            <HttpsCertId>1513561019707729_16f37aae5f3_-375882821_-169099****</HttpsCertId>
            <Protocol>TCP</Protocol>
            <TargetPort>8080</TargetPort>
            <Port>80</Port>
        </Intranet>
        <InternetIp>59.74.**.**</InternetIp>
        <InternetSlbId>lb-uf6xc7wybefehnv45****</InternetSlbId>
        <Internet>
            <HttpsCertId>1513561019707729_16f37aae5f3_-375882821_-169099****</HttpsCertId>
            <Protocol>TCP</Protocol>
            <TargetPort>8080</TargetPort>
            <Port>80</Port>
        </Internet>
        <IntranetSlbId>lb-uf6xc7wybefehnv45****</IntranetSlbId>
        <IntranetIp>192.168.0.0</IntranetIp>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeApplicationSlbsResponse>
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
    "Intranet" : [ {
      "HttpsCertId" : "1513561019707729_16f37aae5f3_-375882821_-169099****",
      "Protocol" : "TCP",
      "TargetPort" : 8080,
      "Port" : 80
    } ],
    "InternetIp" : "59.74.**.**",
    "InternetSlbId" : "lb-uf6xc7wybefehnv45****",
    "Internet" : [ {
      "HttpsCertId" : "1513561019707729_16f37aae5f3_-375882821_-169099****",
      "Protocol" : "TCP",
      "TargetPort" : 8080,
      "Port" : 80
    } ],
    "IntranetSlbId" : "lb-uf6xc7wybefehnv45****",
    "IntranetIp" : "192.168.0.0"
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

访问[错误中心](https://error-center.aliyun.com/status/product/sae?spm=a2c4g.11186623.2.10.5e356082mBovNa)查看更多错误码。

