# ListLogConfigs

调用ListLogConfigs接口获取应用日志列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListLogConfigs&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/log/listLogConfigs HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|56f77b65-788d-442a-9885-7f20d91f\*\*\*\*|应用ID。 |
|PageSize|Integer|Query|是|10|页面大小。 |
|CurrentPage|Integer|Query|是|1|当前页。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|ac1d5e2c15671581252413581d\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |文件日志信息。 |
|LogConfigs|Array of LogConfig| |日志配置。 |
|ConfigName|String|sae-1f240907a6faf58c653f09e81b7e\*\*\*\*|日志服务配置名称。 |
|LogDir|String|/root/logs/hsf/hsf.log|日志文件路径。 |
|SlsLogStore|String|sae-1f240907a6faf58c653f09e81b7e\*\*\*\*|日志服务日志存储名。 |
|CreateTime|String|2019-08-29 17:18:00|日志配置创建时间。 |
|StoreType|String|sls|日志服务存储类型。 |
|SlsProject|String|sae-56f77b65-788d-442a-9885-7f20d91f\*\*\*\*|日志服务项目ID。 |
|LogType|String|file\_log|日志类型，当前只支持**file\_log**。 |
|RegionId|String|cn-beijing|地域ID。 |
|CurrentPage|Integer|1|当前页面。 |
|TotalSize|Integer|1|总条数。 |
|PageSize|Integer|10|页面大小。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取应用日志列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/log/listLogConfigs?AppId=56f77b65-788d-442a-9885-7f20d91f****&PageSize=10&CurrentPage=1 HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListLogConfigsResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>ac1d5e2c15671581252413581d****</TraceId>
    <Data>
        <LogConfigs>
            <ConfigName>sae-1f240907a6faf58c653f09e81b7e****</ConfigName>
            <LogDir>/root/logs/hsf/hsf.log</LogDir>
            <SlsLogStore>sae-1f240907a6faf58c653f09e81b7e****</SlsLogStore>
            <CreateTime>2019-08-29 17:18:00</CreateTime>
            <StoreType>sls</StoreType>
            <SlsProject>sae-56f77b65-788d-442a-9885-7f20d91f****</SlsProject>
            <LogType>file_log</LogType>
            <RegionId>cn-beijing</RegionId>
        </LogConfigs>
        <CurrentPage>1</CurrentPage>
        <TotalSize>1</TotalSize>
        <PageSize>10</PageSize>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListLogConfigsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "ac1d5e2c15671581252413581d****",
  "Data" : {
    "LogConfigs" : [ {
      "ConfigName" : "sae-1f240907a6faf58c653f09e81b7e****",
      "LogDir" : "/root/logs/hsf/hsf.log",
      "SlsLogStore" : "sae-1f240907a6faf58c653f09e81b7e****",
      "CreateTime" : "2019-08-29 17:18:00",
      "StoreType" : "sls",
      "SlsProject" : "sae-56f77b65-788d-442a-9885-7f20d91f****",
      "LogType" : "file_log",
      "RegionId" : "cn-beijing"
    } ],
    "CurrentPage" : 1,
    "TotalSize" : 1,
    "PageSize" : 10
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

