# CreateApplicationScalingRule

调用CreateApplicationScalingRule接口创建应用弹性伸缩策略。

## 使用须知

-   您最多可以为1个应用创建5条弹性策略。
-   您最多可以为1条定时弹性策略，创建20条单天内触发时间点。
-   弹性策略启用时，请勿手动执行应用生命周期管理操作，例如应用扩缩、部署应用、更改规格、重启应用或停止应用。如果您需要对应用执行该类操作，那么请停用弹性策略后，再手动执行操作。
-   如果当前应用处于扩容、缩容、部署（单批、分批或灰度）、更改规格、重启或停止等过程中，那么该应用暂时无法添加或者启动弹性策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateApplicationScalingRule&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
POST /pop/v1/sam/scale/applicationScalingRule HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|ScalingRuleName|String|Query|是|timer-0800-2100|自定义的弹性伸缩策略名。应用内，策略名称不可重复，必须以小写字母开头，仅可包含小写字母、数字及短划线（-），不超过32个字符。

**说明：** 伸缩策略创建成功后，不可修改策略名。 |
|ScalingRuleType|String|Query|是|timing|弹性策略类型。取值说明如下：

-   **timing**：定时弹性 |
|ScalingRuleTimer|String|Query|否|\{"beginDate":null,"endDate":null,"period":"\* \* \*","schedules":\[\{"atTime":"08:00","targetReplicas":10\},\{"atTime":"20:00","targetReplicas":3\}\]\}|定时弹性策略的配置。参数说明如下：

-   **beginDate**：长期，适用于不需要指定执行定时弹性伸缩策略的结束日期时的场景。取值：**null**。
-   **endDate**：短期，适用于需要指定执行定时弹性伸缩策略的起止日期时的场景。取值示例：**2021-03-25**。
-   **period**：执行定时弹性伸缩策略的周期。取值说明如下：
    -   **\* \* \***：每天指定时间执行定时策略。
    -   **\* \* Fri,Mon**：每周指定天数的指定时间执行定时策略，支持选择多星期几，GMT+8时区。取值说明如下：
        -   **Sun**：星期日
        -   **Mon**：星期一
        -   **Tue**：星期二
        -   **Wed**：星期三
        -   **Thu**：星期四
        -   **Fri**：星期五
        -   **Sat**：星期六
    -   **1,2,3,28,31 \* \***：每月指定日期的指定时间执行定时策略。取值范围\[1, 31\]。若当月无31日，则跳过该日期执行定时策略。
-   **schedules**：弹性伸缩策略触发的时间，以及该时间段内需要保持的应用实例数。最多支持20个时间点。参数说明如下:
    -   **atTime**：触发时间点。支持格式**时:分**，例如**08:00**。
    -   **targetReplicas**：该参数可以指定应用的实例数，也可以是每次部署最小存活的实例数。取值范围\[1, 50\]。

**说明：** 每次滚动部署最小存活的实例数建议大于等于**1**，保证业务不中断。如果设置为**0**，应用在升级过程中将会中断业务。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|object| |返回结果。 |
|Timer|object| |定时弹性伸缩。 |
|EndDate|String|2021-04-25|短期结束日期。若为**null**，则为长期。 |
|BeginDate|String|2021-03-25|短期开始日期。若为**null**，则为长期。 |
|Schedules|Array of Schedule| |单天内触发时间点。 |
|AtTime|String|08:00|时间点。格式：**时:分**。 |
|TargetReplicas|Integer|3|目标实例数。 |
|Period|String|\* \* \*|周期。 |
|UpdateTime|Long|1616642248938|伸缩策略的更新时间。单位：毫秒。 |
|AppId|String|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |
|CreateTime|Long|1616642248938|伸缩策略的创建时间。单位：毫秒。 |
|ScaleRuleEnabled|Boolean|true|是否启用伸缩策略。取值说明如下：

-   **true**：启用状态
-   **false**：禁用状态 |
|ScaleRuleType|String|timing|弹性伸缩策略的类型。取值说明如下：

-   **timing**：定时弹性 |
|ScaleRuleName|String|timer-0800-2100|弹性伸缩策略的名称。 |

## 示例

请求示例

```
POST /pop/v1/sam/scale/applicationScalingRule?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69****&ScalingRuleName=timer-0800-2100&ScalingRuleType=timing&ScalingRuleTimer={"beginDate":null,"endDate":null,"period":"* * *","schedules":[{"atTime":"08:00","targetReplicas":10},{"atTime":"20:00","targetReplicas":3}]} HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
<TraceId>0a98a02315955564772843261e****</TraceId>
<Data>
    <Timer>
        <EndDate>2021-04-25</EndDate>
        <BeginDate>2021-03-25</BeginDate>
        <Schedules>
            <AtTime>08:00</AtTime>
            <TargetReplicas>3</TargetReplicas>
        </Schedules>
        <Schedules>
            <AtTime>21:00</AtTime>
            <TargetReplicas>1</TargetReplicas>
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
    </Metric>
    <ScaleRuleName>timer-0800-2100</ScaleRuleName>
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
    "Metric" : {
      "Metrics" : [ { } ]
    },
    "ScaleRuleName" : "timer-0800-2100"
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InstanceExist.ScalingRuleName|The specified ScalingRuleName already exists.|指定的弹性策略名称已存在。|
|400|InvalidScalingRuleDate.BeginAfterEnd|The specified beginning time is later than the ending time.|指定的开始时间晚于结束时间。|
|400|InvalidScalingRuleDate.Format|The specified date is invalid.|指定的日期不合法。正确的格式为yyyy-MM-dd。|
|400|InvalidScalingRuleName.NotFound|The specified ScalingRuleName does not exist.|指定的ScalingRuleName不存在。|
|400|InvalidScalingRuleTime.Conflict|The specified scaling rule time is invalid. Another schedule has been set for the specified time range. Please set a different time.|指定的弹性策略时间无效。该时间段已设置过定时策略，请重新选择时间设置。|
|400|InvalidScalingRuleTime.Format|The specified time is invalid.|指定的时间不合法。正确的格式为HH:mm。|
|400|QuotaExceeded.ScalingRule|The maximum number of application scaling rules is exceeded.|应用弹性策略数量到达上限。|
|400|QuotaExceeded.ScalingRuleTime|The maximum number of scaling policy trigger time is exceeded.|弹性策略触发时间到达上限。|
|400|NoComputeResourceQuota.App.Exceed|You can create %s instances for each application. Please submit a ticket to raise the quota.|每个应用只允许创建%s个实例，请提交工单增加计算资源额度。|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|
|400|NoComputeResourceQuota.User.Exceed|Your account is limited to create %s instances. Please submit a ticket to raise the quota.|您的账户限额%s个实例，请提交工单增加计算资源额度。|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|OperationDenied.SDKNotSupported|Metrics is not supported in SDK|SDK 未开放指标弹性规则|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

