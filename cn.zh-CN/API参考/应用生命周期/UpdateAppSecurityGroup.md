# UpdateAppSecurityGroup

调用UpdateAppSecurityGroup接口更新应用安全组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateAppSecurityGroup&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/app/updateAppSecurityGroup HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|017f39b8-dfa4-4e16-a84b-1dcee4b1\*\*\*\*|应用ID。 |
|SecurityGroupId|String|Query|是|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|ErrorCode|String|InvalidParameter.NotEmpty|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D5557|请求ID。 |
|Success|Boolean|true|更新应用安全组是否成功。取值说明如下：

 -   **true**：表示更新成功。
-   **false**：表示更新失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
PUT /pop/v1/sam/app/updateAppSecurityGroup?RegionId=cn-beijing&AppId=017f39b8-dfa4-4e16-a84b-1dcee4b1****&SecurityGroupId=sg-wz969ngg2e49q5i4****
```

正常返回示例

`XML`格式

```
<UpdateAppSecurityGroupResponse>
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D5557</RequestId>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Code>200</Code>
      <Success>true</Success>
</UpdateAppSecurityGroupResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D5557",
    "TraceId": "0a98a02315955564772843261e****",
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

