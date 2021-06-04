# DescribeApplicationScalingRules

调用DescribeApplicationScalingRules接口查询应用弹性伸缩策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationScalingRules&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/scale/applicationScalingRules HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|CurrentPage|Integer|1|当前页数。 |
|TotalSize|Integer|1|应用弹性伸缩策略总数。 |
|PageSize|Integer|10|页面大小。 |
|ApplicationScalingRules|Array of ApplicationScalingRule| |应用弹性伸缩策略列表。 |
|Timer|Object| |定时弹性伸缩。 |
|EndDate|String|2021-04-25|短期结束日期。若为**null**，则为长期。 |
|BeginDate|String|2021-03-25|短期开始日期。若为**null**，则为长期。 |
|Schedules|Array of Schedule| |单天内触发时间点。 |
|AtTime|String|08:00|时间点。格式：**时:分**。 |
|TargetReplicas|Integer|3|目标实例数。 |
|Period|String|\* \* \*|周期。 |
|UpdateTime|Long|1616642248938|伸缩策略更新时间。单位：毫秒。 |
|AppId|String|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|CreateTime|Long|1616642248938|伸缩策略创建时间。单位：毫秒。 |
|ScaleRuleEnabled|Boolean|true|伸缩策略是否启用。取值说明如下：

 -   **true**：启用状态
-   **false**：禁用状态 |
|ScaleRuleType|String|timing|弹性策略类型。取值说明如下：

 -   **timing**: 定时弹性 |
|ScaleRuleName|String|timer-0800-2100|伸缩策略名称。 |

## 示例

请求示例

```
GET /pop/v1/sam/scale/applicationScalingRules?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
<TraceId>0a98a02315955564772843261e****</TraceId>
<Data>
    <CurrentPage>1</CurrentPage>
    <TotalSize>1</TotalSize>
    <PageSize>10</PageSize>
    <ApplicationScalingRules>
        <Timer>
            <EndDate>2021-04-25</EndDate>
            <BeginDate>2021-03-25</BeginDate>
            <Schedules>
                <AtTime>08:00</AtTime>
                <TargetReplicas>3</TargetReplicas>
            </Schedules>
            <Period>* * *</Period>
        </Timer>
        <UpdateTime>1616642248938</UpdateTime>
        <AppId>7171a6ca-d1cd-4928-8642-7d5cfe69****</AppId>
        <CreateTime>1616642248938</CreateTime>
        <LastDisableTime>1616642248938</LastDisableTime>
        <ScaleRuleEnabled>true</ScaleRuleEnabled>
        <ScaleRuleType>timing</ScaleRuleType>
        <Metric>
            <Metrics/>
            <MetricsStatus>
                <CurrentMetrics/>
                <NextScaleMetrics/>
            </MetricsStatus>
        </Metric>
        <ScaleRuleName>timer-0800-2100</ScaleRuleName>
    </ApplicationScalingRules>
</Data>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : {
    "CurrentPage" : 1,
    "TotalSize" : 1,
    "PageSize" : 10,
    "ApplicationScalingRules" : [ {
      "Timer" : {
        "Schedules" : [ {
          "AtTime" : "08:00",
          "TargetReplicas" : 3
        }, {
          "AtTime" : "21:00",
          "TargetReplicas" : 1
        } ],
        "Period" : "* * *"
      },
      "UpdateTime" : 1616642248938,
      "AppId" : "7171a6ca-d1cd-4928-8642-7d5cfe69****",
      "CreateTime" : 1616642248938,
      "LastDisableTime" : 1616642248938,
      "ScaleRuleEnabled" : true,
      "ScaleRuleType" : "timing",
      "ScaleRuleName" : "timer-0800-2100"
    } ]
  }
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

