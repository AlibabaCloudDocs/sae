# DescribeApplicationInstances

调用DescribeApplicationInstances接口获取应用实例列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationInstances&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/app/describeApplicationInstances HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|d700e680-aa4d-4ec1-afc2-6566b5ff\*\*\*\*|应用ID。 |
|GroupId|String|Query|是|b2a8a925-477a-4ed7-b825-d5e22500\*\*\*\*|应用分组ID。需要调用[DescribeApplicationGroups](~~126249~~)接口获取。 |
|CurrentPage|Integer|Query|否|1|当前页数。 |
|PageSize|Integer|Query|否|10|页面大小。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |应用实例信息。 |
|CurrentPage|Integer|1|当前页数。 |
|Instances|Array of Instance| |应用实例列表。 |
|CreateTimeStamp|Long|1558442609000|实例创建时间戳。单位：毫秒。 |
|GroupId|String|b2a8a925-477a-4ed7-b825-d5e22500\*\*\*\*|实例所属分组ID。 |
|InstanceContainerIp|String|192.168.1.1|实例内网IP。 |
|InstanceContainerRestarts|Long|0|实例重启次数。 |
|InstanceContainerStatus|String|Running|实例运行状态。 |
|InstanceId|String|b2a8a925-477a-4ed7-b825-d5e22500\*\*\*\*|实例ID。 |
|VSwitchId|String|vsw-\*\*\*|实例所在可用区。 |
|PageSize|Integer|10|页码大小。 |
|TotalSize|Integer|30|实例总数。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用实例列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/describeApplicationInstances?RegionId=cn-hangzhou&AppId=d700e680-aa4d-4ec1-afc2-6566b5ff****&GroupId=GroupId%22%3A%20%22b2a8a925-477a-4ed7-b825-d5e22500****
```

正常返回示例

`XML` 格式

```
<DescribeApplicationInstancesResponse>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <Message>success</Message>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Data>
    	    <Instances>
        	      <InstanceContainerIp>192.168.1.1</InstanceContainerIp>
        	      <InstanceId>b2a8a925-477a-4ed7-b825-d5e22500****</InstanceId>
        	      <VSwitchId>vsw-***</VSwitchId>
        	      <InstanceContainerRestarts>0</InstanceContainerRestarts>
        	      <InstanceContainerStatus>Running</InstanceContainerStatus>
        	      <CreateTimeStamp>1558442609000</CreateTimeStamp>
        	      <GroupId>b2a8a925-477a-4ed7-b825-d5e22500****</GroupId>
    	    </Instances>
    	    <PageSize>10</PageSize>
    	    <CurrentPage>1</CurrentPage>
    	    <TotalSize>30</TotalSize>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeApplicationInstancesResponse>
```

`JSON` 格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "Instances": {
            "InstanceContainerIp": "192.168.1.1",
            "InstanceId": "b2a8a925-477a-4ed7-b825-d5e22500****",
            "VSwitchId": "vsw-***",
            "InstanceContainerRestarts": 0,
            "InstanceContainerStatus": "Running",
            "CreateTimeStamp": 1558442609000,
            "GroupId": "b2a8a925-477a-4ed7-b825-d5e22500****"
        },
        "PageSize": 10,
        "CurrentPage": 1,
        "TotalSize": 30
    },
    "ErrorCode": "success",
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

