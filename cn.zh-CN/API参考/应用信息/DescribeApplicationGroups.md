# DescribeApplicationGroups

调用DescribeApplicationGroups接口获取应用实例分组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationGroups&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/app/describeApplicationGroups HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|d700e680-aa4d-4ec1-afc2-6566b5ff\*\*\*\*|应用ID。 |
|CurrentPage|Integer|Query|否|1|页码。 |
|PageSize|Integer|Query|否|10|页面大小。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Array of ApplicationGroup| |应用分组信息。 |
|EdasContainerVersion|String|3.5.3|部署时所使用的EdasContainer版本。 |
|GroupId|String|b2a8a925-477a-eswa-b823-d5e22500\*\*\*\*|分组ID。 |
|GroupName|String|\_DEFAULT\_GROUP|分组名称。 |
|GroupType|Integer|0|分组类型。 |
|ImageUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest|部署时设置的ImageUrl。 |
|Jdk|String|Open JDK 8|部署时设置的JDK。 |
|PackageType|String|Image|部署类型。 |
|PackageUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest|部署时设置的WAR或JAR包地址。 |
|PackageVersion|String|1.0.0|部署时设置的软件版本。若为**ImageUrl**部署，则自动生成。 |
|Replicas|Integer|10|所有实例数。 |
|RunningInstances|Integer|1|运行中的实例数。 |
|WebContainer|String|Apache Tomcat 7|部署时设置的WebContainer。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用实例分是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/describeApplicationGroups?RegionId=cn-beijing&AppId=d700e680-aa4d-4ec1-afc2-6566b5ff****
```

正常返回示例

`XML` 格式

```
<DescribeApplicationGroupsResponse>
	  <Data>
		    <GroupType>0</GroupType>
		    <RunningInstances>2</RunningInstances>
		    <PackageType>Image</PackageType>
		    <GroupName>_DEFAULT_GROUP</GroupName>
		    <PackageVersion>2019-04-26 15:56:34.115</PackageVersion>
		    <ImageUrl>registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest</ImageUrl>
		    <Replicas>2</Replicas>
		    <GroupId>b2a8a925-477a-eswa-b823-d5e22500****</GroupId>
	  </Data>
	  <Message>success</Message>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Success>true</Success>
	  <Code>200</Code>
</DescribeApplicationGroupsResponse>
```

`JSON` 格式

```
{
  "Data": [
    {
      "GroupType": 0,
      "RunningInstances": 2,
      "PackageType": "Image",
      "GroupName": "_DEFAULT_GROUP",
      "PackageVersion": "2019-04-26 15:56:34.115",
      "ImageUrl": "registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest",
      "Replicas": 2,
      "GroupId": "b2a8a925-477a-eswa-b823-d5e22500****"
    }
  ],
  "Message": "success",
  "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "TraceId": "0a98a02315955564772843261e****",
  "Success": true,
  "Code": 200
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

