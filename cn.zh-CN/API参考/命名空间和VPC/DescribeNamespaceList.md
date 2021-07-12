# DescribeNamespaceList

调用DescribeNamespaceList接口获取命名空间列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespaceList&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/namespace/describeNamespaceList HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|ContainCustom|Boolean|Query|否|true|是否返回自定义命名空间。取值说明如下：

 -   **true**：表示返回自定义命名空间。
-   **false**：表示不返回自定义命名空间。 |
|HybridCloudExclude|Boolean|Query|否|true|是否排除混合云命名空间。取值说明如下：

 -   **true**：表示排除混合云命名空间。
-   **false**：表示不排除混合云命名空间。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|30375C38-F4ED-4135-A0AE-5C75DC7F\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|ac1a0b2215622920113732501e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Array of RegionList| |命名空间列表。 |
|VpcId|String|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |
|VSwitchId|String|vsw-2ze559r1z1bpwqxwp\*\*\*\*|vSwitch ID。 |
|Custom|Boolean|true|是否返回自定义命名空间。取值说明如下：

 -   **true**：表示返回自定义命名空间。
-   **false**：表示不返回自定义命名空间。 |
|AgentInstall|String|http://edas-bj.oss-cn-beijing-internal.aliyuncs.com/test/install.sh|Agent安装命令。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|HybridCloudEnable|Boolean|false|是否排除混合云命名空间。取值说明如下：

 -   **true**：表示排除混合云命名空间。
-   **false**：表示不排除混合云命名空间。 |
|SecurityGroupId|String|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |
|Current|Boolean|false|废弃参数，无特殊含义。 |
|NamespaceName|String|test|命名空间名称。 |
|RegionId|String|cn-beijing|命名空间所属地域。 |
|ErrorCode|String|error|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取命名空间列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/namespace/describeNamespaceList?ContainCustom=true&HybridCloudExclude=true HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeNamespaceListResponse>
    <RequestId>30375C38-F4ED-4135-A0AE-5C75DC7F****</RequestId>
    <Message>success</Message>
    <TraceId>ac1a0b2215622920113732501e****</TraceId>
    <Data>
        <VpcId>vpc-2ze0i263cnn311nvj****</VpcId>
        <VSwitchId>vsw-2ze559r1z1bpwqxwp****</VSwitchId>
        <Custom>true</Custom>
        <AgentInstall>http://edas-bj.oss-cn-beijing-internal.aliyuncs.com/test/install.sh</AgentInstall>
        <NamespaceId>cn-beijing:test</NamespaceId>
        <HybridCloudEnable>false</HybridCloudEnable>
        <SecurityGroupId>sg-wz969ngg2e49q5i4****</SecurityGroupId>
        <Current>false</Current>
        <NamespaceName>test</NamespaceName>
        <RegionId>cn-beijing</RegionId>
    </Data>
    <ErrorCode>error</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeNamespaceListResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "30375C38-F4ED-4135-A0AE-5C75DC7F****",
  "Message" : "success",
  "TraceId" : "ac1a0b2215622920113732501e****",
  "Data" : [ {
    "VpcId" : "vpc-2ze0i263cnn311nvj****",
    "VSwitchId" : "vsw-2ze559r1z1bpwqxwp****",
    "Custom" : true,
    "AgentInstall" : "http://edas-bj.oss-cn-beijing-internal.aliyuncs.com/test/install.sh",
    "NamespaceId" : "cn-beijing:test",
    "HybridCloudEnable" : false,
    "SecurityGroupId" : "sg-wz969ngg2e49q5i4****",
    "Current" : false,
    "NamespaceName" : "test",
    "RegionId" : "cn-beijing"
  } ],
  "ErrorCode" : "error",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

