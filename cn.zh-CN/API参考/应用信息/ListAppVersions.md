# ListAppVersions

调用ListAppVersions接口查看应用的历史版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListAppVersions&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/listAppVersions HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|否|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|01CF26C7-00A3-4AA6-BA76-7E95F2A3\*\*\*\*|请求ID。 |
|Data|Array of PackageVersionEntity| |版本信息。 |
|Type|String|image|应用类型。取值说明如下：

 -   **image**：镜像。
-   **upload**：上传的WAR包或JAR包文件。
-   **url**：填写的WAR包或JAR包的URL。 |
|CreateTime|String|1590124643553|创建时间。 |
|BuildPackageUrl|String|https://edas-hz.oss-cn-hangzhou.aliyuncs.com/apps/K8s\_APP\_ID/1d0e7884-60f0-41d2-89dd-ec1f3c69\*\*\*\*/hello-sae.war|当**Type**为**url**时，表示WAR包或JAR包的下载地址。 |
|WarUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/\*\*\*\*/1362469756373809\_shared\_repo:42646692-66e7-4a21-b629-897752975cdf\_159012464\*\*\*\*|-   当**Type**为**image**时，表示镜像地址。
-   当**Type**为**upload**时，表示WAR包或JAR包的下载地址。 |
|Id|String|a0ce266c-d354-423a-9bd6-4083405a\*\*\*\*|版本ID。 |
|ErrorCode|String|InvalidApplication.NotFound|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|查看应用的历史版本是否成功。取值说明如下：

 -   **true**：表示查看历史版本成功。
-   **false**：表示查看历史版本失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/listAppVersions?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListAppVersionsResponse>
    <Message>success</Message>
    <RequestId>01CF26C7-00A3-4AA6-BA76-7E95F2A3****</RequestId>
    <Data>
        <Type>image</Type>
        <CreateTime>1590124643553</CreateTime>
        <BuildPackageUrl>https://edas-hz.oss-cn-hangzhou.aliyuncs.com/apps/K8s_APP_ID/1d0e7884-60f0-41d2-89dd-ec1f3c69****/hello-sae.war</BuildPackageUrl>
        <WarUrl>registry-vpc.cn-hangzhou.aliyuncs.com/****/1362469756373809_shared_repo:42646692-66e7-4a21-b629-897752975cdf_159012464****</WarUrl>
        <Id>a0ce266c-d354-423a-9bd6-4083405a****</Id>
    </Data>
    <ErrorCode>InvalidApplication.NotFound</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListAppVersionsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "success",
  "RequestId" : "01CF26C7-00A3-4AA6-BA76-7E95F2A3****",
  "Data" : [ {
    "Type" : "image",
    "CreateTime" : "1590124643553",
    "BuildPackageUrl" : "https://edas-hz.oss-cn-hangzhou.aliyuncs.com/apps/K8s_APP_ID/1d0e7884-60f0-41d2-89dd-ec1f3c69****/hello-sae.war",
    "WarUrl" : "registry-vpc.cn-hangzhou.aliyuncs.com/****/1362469756373809_shared_repo:42646692-66e7-4a21-b629-897752975cdf_159012464****",
    "Id" : "a0ce266c-d354-423a-9bd6-4083405a****"
  } ],
  "ErrorCode" : "InvalidApplication.NotFound",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

