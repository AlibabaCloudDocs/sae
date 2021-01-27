# DescribeApplicationImage

调用DescribeApplicationImage接口描述应用镜像信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationImage&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/container/describeApplicationImage HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|d700e680-aa4d-4ec1-afc2-6566b5ff\*\*\*\*|应用ID。 |
|ImageUrl|String|Query|是|registry-vpc.cn-hangzhou.aliyuncs.com/demo/demo:latest|镜像URL。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |应用镜像信息。 |
|CrUrl|String|保留字段|保留字段，暂无特殊含义。 |
|Logo|String|保留字段|保留字段，暂无特殊含义。 |
|RegionId|String|cn-beijing|地域。 |
|RepoName|String|demo|镜像仓库名称。 |
|RepoNamespace|String|demo|镜像命名空间。 |
|RepoOriginType|String|ALI\_HUB|镜像仓库类型。当前仅支持容器镜像服务。 |
|RepoTag|String|latest|镜像TAG。 |
|RepoType|String|保留字段|保留字段。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用镜像信息是否成功。取值说明如下：

 -   **true**：表示获取信息成功。
-   **false**：表示获取信息失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/container/describeApplicationImage?RegionId=cn-beijing&AppId=d700e680-aa4d-4ec1-afc2-6566b5ff****&ImageUrl=registry-vpc.cn-hangzhou.aliyuncs.com%2Fdemo%2Fdemo%3Alatest
```

正常返回示例

`XML` 格式

```
<DescribeApplicationImageResponse>
	  <Data>
		    <RepoName>nginx</RepoName>
		    <RepoOriginType>ALI_HUB</RepoOriginType>
		    <RepoNamespace>demo</RepoNamespace>
		    <RepoTag>latest</RepoTag>
		    <RegionId>cn-hangzhou</RegionId>
	  </Data>
	  <Message>success</Message>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Success>true</Success>
	  <Code>200</Code>
</DescribeApplicationImageResponse>
```

`JSON` 格式

```
{
  "Data": {
    "RepoName": "nginx",
    "RepoOriginType": "ALI_HUB",
    "RepoNamespace": "demo",
    "RepoTag": "latest",
    "RegionId": "cn-hangzhou"
  },
  "Message": "success",
  "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "TraceId": "0a98a02315955564772843261e****",
  "Success": true,
  "Code": 200
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

