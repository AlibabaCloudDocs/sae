# DescribeRegions

调用DescribeRegions接口查询可用地域。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeRegions&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/paas/regionConfig HTTP/1.1
```

## 请求参数

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|Integer|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Message|String|success|调用结果的附加信息。 |
|Regions|Array of Region| |地域列表。 |
|Region| | | |
|LocalName|String|华东2（上海）|地域名称。 |
|RegionEndpoint|String|sae.cn-shanghai.aliyuncs.com|地域地址。 |
|RegionId|String|cn-shanghai|地域ID。 |
|RequestId|String|DDE85827-B0B3-4E56-86E8-17C42009\*\*\*\*|请求ID。 |

## 示例

请求示例

```
GET /pop/v1/paas/regionConfig HTTP/1.1
公共请求头
```

正常返回示例

`XML`格式

```
<DescribeRegionsResponse>
	  <Message>success</Message>
	  <RequestId>DDE85827-B0B3-4E56-86E8-17C420090D5C</RequestId>
	  <Regions>
		    <Region>
			      <RegionId>cn-shanghai</RegionId>
			      <RegionEndpoint>sae.cn-shanghai.aliyuncs.com</RegionEndpoint>
			      <LocalName>华东2（上海）</LocalName>
		    </Region>
		    <Region>
			      <RegionId>cn-hangzhou</RegionId>
			      <RegionEndpoint>sae.cn-hangzhou.aliyuncs.com</RegionEndpoint>
			      <LocalName>华东1（杭州）</LocalName>
		    </Region>
	  </Regions>
	  <Code>200</Code>
</DescribeRegionsResponse>
```

`JSON`格式

```
{
  "Message": "success",
  "RequestId": "DDE85827-B0B3-4E56-86E8-17C420090D5C",
  "Regions": {
    "Region": [
      {
        "RegionId": "cn-shanghai",
        "RegionEndpoint": "sae.cn-shanghai.aliyuncs.com",
        "LocalName": "华东2（上海）"
      },
      {
        "RegionId": "cn-hangzhou",
        "RegionEndpoint": "sae.cn-hangzhou.aliyuncs.com",
        "LocalName": "华东1（杭州）"
      }
    ]
  },
  "Code": 200
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

