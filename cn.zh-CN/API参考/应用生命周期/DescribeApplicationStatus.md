# DescribeApplicationStatus

调用DescribeApplicationStatus接口获取应用的状态信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationStatus&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/describeApplicationStatus HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*|目标应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|ArmsAdvancedEnabled|String|false|是否开通ARMS高级版。取值说明如下：

 -   **true**：表示开通ARMS高级版。
-   **false**：表示不开通ARMS高级版。 |
|LastChangeOrderId|String|1ccc2339-fc19-49aa-bda0-1e7b8497\*\*\*\*|上一次执行的发布单ID，未执行过或发布单信息过期则为空。 |
|ArmsApmInfo|String|\{"appId":"0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*","licenseKey":"d5cgdt5pu0@7303f55292a\*\*\*\*"\}|该应用在ARMS侧元数据信息。 |
|CreateTime|String|1563373372746|应用创建时间。 |
|CurrentStatus|String|RUNNING|应用当前状态。取值说明如下：

 -   **RUNNING**：表示应用正在运行。
-   **STOPPED**：表示应用停止运行。
-   **UNKNOWN**：表示应用状态未知。 |
|AppId|String|0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*|当前应用ID。 |
|LastChangeOrderRunning|Boolean|false|上一次发布单是否处于执行中。取值说明如下：

 -   **true**：表示上一次发布单处于执行中。
-   **false**：表示上一次发布单不处于执行中。 |
|RunningInstances|Integer|1|当前应用运行中的实例数。 |
|LastChangeOrderStatus|String|SUCCESS|上一次发布单状态。取值说明如下：

 -   **READY**：表示上一次发布单准备就绪。
-   **RUNNING**：表示上一次发布单处于执行中。
-   **SUCCESS**：表示上一次发布单发布成功。
-   **FAIL**：表示上一次发布单发布失败。
-   **ABORT**：表示上一次发布单中止运行。
-   **WAIT\_BATCH\_CONFIRM**：表示上一次发布单等待批量确认。
-   **AUTO\_BATCH\_WAIT**：表示上一次发布单处于自动批量等待状态。
-   **SYSTEM\_FAIL**：表示系统故障。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取应用状态信息是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/describeApplicationStatus?AppId=0099b7be-5f5b-4512-a7fc-56049ef1**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeApplicationStatusResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <ArmsAdvancedEnabled>false</ArmsAdvancedEnabled>
        <LastChangeOrderId>1ccc2339-fc19-49aa-bda0-1e7b8497****</LastChangeOrderId>
        <ArmsApmInfo>{"appId":"0099b7be-5f5b-4512-a7fc-56049ef1****","licenseKey":"d5cgdt5pu0@7303f55292a****"}</ArmsApmInfo>
        <CreateTime>1563373372746</CreateTime>
        <CurrentStatus>RUNNING</CurrentStatus>
        <AppId>0099b7be-5f5b-4512-a7fc-56049ef1****</AppId>
        <LastChangeOrderRunning>false</LastChangeOrderRunning>
        <RunningInstances>1</RunningInstances>
        <LastChangeOrderStatus>SUCCESS</LastChangeOrderStatus>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeApplicationStatusResponse>
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
    "ArmsAdvancedEnabled" : "false",
    "LastChangeOrderId" : "1ccc2339-fc19-49aa-bda0-1e7b8497****",
    "ArmsApmInfo" : "{\"appId\":\"0099b7be-5f5b-4512-a7fc-56049ef1****\",\"licenseKey\":\"d5cgdt5pu0@7303f55292a****\"}",
    "CreateTime" : "1563373372746",
    "CurrentStatus" : "RUNNING",
    "AppId" : "0099b7be-5f5b-4512-a7fc-56049ef1****",
    "LastChangeOrderRunning" : false,
    "RunningInstances" : 1,
    "LastChangeOrderStatus" : "SUCCESS"
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
|404|InvalidAppId.NotFound|The specified AppId does not exist.|指定的AppId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

