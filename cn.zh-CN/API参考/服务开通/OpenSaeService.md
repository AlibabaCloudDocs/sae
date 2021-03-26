# OpenSaeService

调用OpenSaeService免费开通SAE服务。

**说明：** 请确保您的账号余额大于0，否则，无法开通SAE服务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=OpenSaeService&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
POST|GET /service/open HTTP/1.1
```

## 请求参数

无请求参数

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|559B4247-C41C-4D9E-B866-B55D378B\*\*\*\*|请求ID。 |
|OrderId|String|20485646575\*\*\*\*|订单ID。 |

## 示例

请求示例

```
POST /service/open HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<OpenSaeServiceResponse>
<RequestId>559B4247-C41C-4D9E-B866-B55D378B****</RequestId>
<OrderId>20485646575****</OrderId>
</OpenSaeServiceResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "559B4247-C41C-4D9E-B866-B55D378B****",
  "OrderId" : "20485646575****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

