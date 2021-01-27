# DescribeApplicationSlbs

调用DescribeApplicationSlbs接口获取应用SLB配置信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationSlbs&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

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
|Code|String|200|接口状态或POP错误码。 |
|Data|Struct| |返回结果。 |
|Internet|Array of Internet| |公网SLB配置。 |
|HttpsCertId|String|1513561019707729\_16f37aae5f3\_-375882821\_-169099\*\*\*\*|HTTPS协议对应的阿里云证书ID。 |
|Port|Integer|80|SLB监听端口。 |
|Protocol|String|TCP|支持的协议。 |
|TargetPort|Integer|8080|容器端口。 |
|InternetIp|String|59.74.\*\*.\*\*|公网SLB地址。 |
|InternetSlbId|String|lb-uf6xc7wybefehnv45\*\*\*\*|公网SLB ID。 |
|Intranet|Array of Intranet| |内网SLB配置。 |
|HttpsCertId|String|1513561019707729\_16f37aae5f3\_-375882821\_-169099\*\*\*\*|HTTPS协议对应的阿里云证书ID。 |
|Port|Integer|80|SLB监听端口。 |
|Protocol|String|TCP|支持的协议。 |
|TargetPort|Integer|8080|容器端口。 |
|IntranetIp|String|192.168.0.0|内网SLB地址。 |
|IntranetSlbId|String|lb-uf6xc7wybefehnv45\*\*\*\*|内网SLB ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用SLB配置信息是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/slb?RegionId=cn-hangzhou&AppId=017f39b8-dfa4-4e16-a84b-1dcee4b1****
```

正常返回示例

`XML`格式

```
<DescribeApplicationSlbsResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <InternetSlbId>lb-uf6xc7wybefehnv45****</InternetSlbId>
            <InternetIp>59.74.**.**</InternetIp>
            <Intranet>
                  <TargetPort>8080</TargetPort>
                  <Protocol>TCP</Protocol>
                  <Port>80</Port>
                  <HttpsCertId>1513561019707729_16f37aae5f3_-375882821_-169099****</HttpsCertId>
            </Intranet>
            <IntranetSlbId>lb-uf6xc7wybefehnv45****</IntranetSlbId>
            <Internet>
                  <TargetPort>8080</TargetPort>
                  <Protocol>TCP</Protocol>
                  <Port>80</Port>
                  <HttpsCertId>1513561019707729_16f37aae5f3_-375882821_-169099****</HttpsCertId>
            </Internet>
            <IntranetIp>192.168.0.0</IntranetIp>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</DescribeApplicationSlbsResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "InternetSlbId": "lb-uf6xc7wybefehnv45****",
        "InternetIp": "59.74.**.**",
        "Intranet": {
            "TargetPort": 8080,
            "Protocol": "TCP",
            "Port": 80,
            "HttpsCertId": "1513561019707729_16f37aae5f3_-375882821_-169099****"
        },
        "IntranetSlbId": "lb-uf6xc7wybefehnv45****",
        "Internet": {
            "TargetPort": 8080,
            "Protocol": "TCP",
            "Port": 80,
            "HttpsCertId": "1513561019707729_16f37aae5f3_-375882821_-169099****"
        },
        "IntranetIp": "192.168.0.0"
    },
    "Code": 200,
    "Success": true
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

