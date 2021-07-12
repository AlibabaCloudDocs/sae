# QueryResourceStatics

调用QueryResourceStatics接口获取应用的资源使用量。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=QueryResourceStatics&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/paas/quota/queryResourceStatics HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|7CCF7092-72CA-4431-90D6-C7D98752\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|ac1a08a015623098794277264e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |资源使用信息。 |
|Summary|Object| |当月资源使用信息。 |
|Cpu|Float|3354|CPU使用量，单位：Core\*min。 |
|Memory|Float|6708|内存使用量，单位：GiB\*min。 |
|RealTimeRes|Object| |实时资源使用量。 |
|Cpu|Float|13|CPU使用量，单位：Core\*min。 |
|Memory|Float|26|内存使用量，单位：GiB\*min。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取应用资源使用量是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/paas/quota/queryResourceStatics?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<QueryResourceStaticsResponse>
    <RequestId>7CCF7092-72CA-4431-90D6-C7D98752****</RequestId>
    <Message>success</Message>
    <TraceId>ac1a08a015623098794277264e****</TraceId>
    <Data>
        <Summary>
            <Cpu>3354</Cpu>
            <Memory>6708</Memory>
        </Summary>
        <RealTimeRes>
            <Cpu>13</Cpu>
            <Memory>26</Memory>
        </RealTimeRes>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</QueryResourceStaticsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "7CCF7092-72CA-4431-90D6-C7D98752****",
  "Message" : "success",
  "TraceId" : "ac1a08a015623098794277264e****",
  "Data" : {
    "Summary" : {
      "Cpu" : 3354,
      "Memory" : 6708
    },
    "RealTimeRes" : {
      "Cpu" : 13,
      "Memory" : 26
    }
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidServerlessRegion.Unsupported|The current region is not supported: %s|不支持当前地域：%s。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|500|Measuredata.Query.Error|An error occurred while querying measurement information.|当查询计量信息时报错。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

