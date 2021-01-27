# DescribeInstanceSpecifications

调用DescribeInstanceSpecifications接口获取应用实例规格信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeInstanceSpecifications&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/paas/quota/instanceSpecifications HTTP/1.1
```

## 请求参数

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Array of Data| |实例规格信息。 |
|Cpu|Integer|2000|CPU大小，规格为微核。 |
|Enable|Boolean|true|实例是否可用。取值说明如下：

 -   **true**：表示可用。
-   **false**：表示不可用。 |
|Id|Integer|4|规格配置ID。 |
|Memory|Integer|4096|内存规格，单位为MB。 |
|SpecInfo|String|通用型4|规格配置名称。 |
|Version|Integer|0|规格配置版本号。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取实例规格是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
https://sae.cn-hangzhou.aliyuncs.com/pop/v1/paas/quota/instanceSpecifications?RegionId=cn-hangzhou
```

正常返回示例

`XML`格式

```
<DescribeInstanceSpecifications>
	  <Message>success</Message>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Data>
		    <SpecInfo>通用型1</SpecInfo>
		    <Version>0</Version>
		    <Memory>1024</Memory>
		    <Cpu>1000</Cpu>
		    <Enable>false</Enable>
		    <Id>1</Id>
	  </Data>
	  <Data>
		    <SpecInfo>通用型2</SpecInfo>
		    <Version>0</Version>
		    <Memory>2048</Memory>
		    <Cpu>1000</Cpu>
		    <Enable>true</Enable>
		    <Id>2</Id>
	  </Data>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeInstanceSpecifications>
```

`JSON`格式

```
{
    "Message":"success",
    "RequestId":"91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId":"0a98a02315955564772843261e****",
    "Data":[
        {
            "SpecInfo":"通用型1",
            "Version":0,
            "Memory":1024,
            "Cpu":1000,
            "Enable":false,
            "Id":1
        },
        {
            "SpecInfo":"通用型2",
            "Version":0,
            "Memory":2048,
            "Cpu":1000,
            "Enable":true,
            "Id":2
        }
    ],
    "Code":200,
    "Success":true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

