# QueryResourceStatics

调用QueryResourceStatics接口获取应用的资源使用量。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=QueryResourceStatics&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

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
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |资源使用信息。 |
|RealTimeRes|Struct| |实时资源使用量。 |
|Cpu|Float|13|CPU使用量，单位：Core\*min。 |
|Memory|Float|26|内存使用量，单位：GiB\*min。 |
|Summary|Struct| |当月资源使用信息。 |
|Cpu|Float|3354|CPU使用量，单位：Core\*min。 |
|Memory|Float|6708|内存使用量，单位：GiB\*min。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|7CCF7092-72CA-4431-90D6-C7D98752\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用的资源使用量是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|ac1a08a015623098794277264e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/paas/quota/queryResourceStatics?RegionId=cn-beijing&AppId=7171a6ca-d1cd-4928-8642-7d5cfe69****
```

正常返回示例

`XML`格式

```
<QueryResourceStaticsResponse>
      <Message>success</Message>
      <RequestId>7CCF7092-72CA-4431-90D6-C7D98752****</RequestId>
      <TraceId>ac1a08a015623098794277264e****</TraceId>
      <Data>
            <Summary>
                  <Memory>6708</Memory>
                  <Cpu>3354</Cpu>
            </Summary>
            <RealTimeRes>
                  <Memory>6708</Memory>
                  <Cpu>3354</Cpu>
            </RealTimeRes>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</QueryResourceStaticsResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "RequestId": "7CCF7092-72CA-4431-90D6-C7D98752****",
    "TraceId": "ac1a08a015623098794277264e****",
    "Data": {
        "Summary": {
            "Memory": 6708,
            "Cpu": 3354
        },
        "RealTimeRes": {
            "Memory": 6708,
            "Cpu": 3354
        }
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidServerlessRegion.Unsupported|The current region is not supported: %s|不支持当前地域：%s。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

