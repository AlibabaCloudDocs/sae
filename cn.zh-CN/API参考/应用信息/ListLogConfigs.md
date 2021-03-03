# ListLogConfigs

调用ListLogConfigs接口获取应用日志列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListLogConfigs&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/log/listLogConfigs HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|56f77b65-788d-442a-9885-7f20d91f\*\*\*\*|应用ID。 |
|CurrentPage|Integer|Query|是|1|当前页。 |
|PageSize|Integer|Query|是|10|页面大小。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口返状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |文件日志信息。 |
|CurrentPage|Integer|1|当前页面。 |
|LogConfigs|Array of LogConfig| |日志配置。 |
|ConfigName|String|sae-1f240907a6faf58c653f09e81b7e\*\*\*\*|日志服务配置名称。 |
|CreateTime|String|2019-08-29 17:18:00|日志配置创建时间。 |
|LogDir|String|/root/logs/hsf/hsf.log|日志文件路径。 |
|LogType|String|file\_log|日志类型，当前只支持**file\_log**。 |
|RegionId|String|cn-beijing|地域ID。 |
|SlsLogStore|String|sae-1f240907a6faf58c653f09e81b7e\*\*\*\*|日志服务日志存储名。 |
|SlsProject|String|sae-56f77b65-788d-442a-9885-7f20d91f\*\*\*\*|日志服务项目ID。 |
|StoreType|String|sls|日志服务存储类型。 |
|PageSize|Integer|10|页面大小。 |
|TotalSize|Integer|1|总条数。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用日志列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|ac1d5e2c15671581252413581d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/log/listLogConfigs?RegionId=cn-beijing&AppId=56f77b65-788d-442a-9885-7f20d91f****&PageSize=1&CurrentPage=10
```

正常返回示例

`XML`格式

```
<ListLogConfigsResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>ac1d5e2c15671581252413581d****</TraceId>
      <Data>
            <LogConfigs>
                  <SlsLogStore>sae-1f240907a6faf58c653f09e81b7e****</SlsLogStore>
                  <StoreType>sls</StoreType>
                  <SlsProject>sae-56f77b65-788d-442a-9885-7f20d91f****</SlsProject>
                  <ConfigName>sae-1f240907a6faf58c653f09e81b7e****</ConfigName>
                  <LogDir>/root/logs/hsf/hsf.log</LogDir>
                  <CreateTime>2019-08-29 17:18:00</CreateTime>
                  <LogType>file_log</LogType>
                  <RegionId>cn-beijing</RegionId>
            </LogConfigs>
            <PageSize>10</PageSize>
            <CurrentPage>1</CurrentPage>
            <TotalSize>1</TotalSize>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</ListLogConfigsResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "ac1d5e2c15671581252413581d****",
    "Data": {
        "LogConfigs": {
            "SlsLogStore": "sae-1f240907a6faf58c653f09e81b7e****",
            "StoreType": "sls",
            "SlsProject": "sae-56f77b65-788d-442a-9885-7f20d91f****",
            "ConfigName": "sae-1f240907a6faf58c653f09e81b7e****",
            "LogDir": "/root/logs/hsf/hsf.log",
            "CreateTime": "2019-08-29 17:18:00",
            "LogType": "file_log",
            "RegionId": "cn-beijing"
        },
        "PageSize": 10,
        "CurrentPage": 1,
        "TotalSize": 1
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

