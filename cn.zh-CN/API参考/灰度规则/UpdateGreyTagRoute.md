# UpdateGreyTagRoute

调用UpdateGreyTagRoute接口更新灰度规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateGreyTagRoute&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
PUT /pop/v1/sam/tagroute/greyTagRoute HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|Description|String|Query|否|灰度发布-地域灰度|规则描述。 |
|ScRules|String|Query|否|\[\{"condition":"OR","items":\[\{"cond":"==","name":"grey","operator":"rawvalue","type":"param","value":"true"\},\{"cond":"==","name":"grey","operator":"rawvalue","type":"cookie","value":"true"\},\{"cond":"==","name":"grey","operator":"rawvalue","type":"header","value":"true"\}\],"path":"/post-echo/hi"\}\]|Spring Cloud应用的灰度规则。 |
|DubboRules|String|Query|否|\[\{"condition":"OR","group":"DUBBO","items":\[\{"cond":"==","expr":".key1","index":0,"operator":"rawvalue","value":"value1"\},\{"cond":"==","expr":".key2","index":0,"operator":"rawvalue","value":"value2"\}\],"methodName":"echo","serviceName":"com.alibaba.edas.boot.EchoService","version":"1.0.0"\}\]|Dubbo应用的灰度规则。 |
|GreyTagRouteId|Long|Query|是|\[\{"condition":"OR","items":\[\{"cond":"==","name":"grey","operator":"rawvalue","type":"param","value":"true"\},\{"cond":"==","name":"grey","operator":"rawvalue","type":"cookie","value":"true"\},\{"cond":"==","name":"grey","operator":"rawvalue","type":"header","value":"true"\}\],"path":"/post-echo/hi"\}\]|灰度规则ID。 |

-   **ScRules参数说明**

|参数名称

|类型

|示例

|描述 |
|------|----|----|----|
|condition

|String

|OR

|灰度规则的条件模式，取值说明如下：

 -   **AND**：表示与，即同时满足条件列表中的所有条件。
-   **OR**：表示或，即满足条件列表中的任一条件。 |
|path

|String

|/path

|Spring Cloud应用灰度规则对应的路径。 |
|items

|Array of items

| |条件列表。 |

**items参数说明**

|参数名称

|类型

|示例

|描述 |
|------|----|----|----|
|name

|String

|test

|参数名。 |
|cond

|String

|==

|比较操作符。可取值：**\>**、**<**、**\>=**、**<=**、**==**以及**!=**。 |
|type

|String

|cookie

|比较类型，取值说明如下：

 -   **param**：表示Parameter。
-   **cookie**：表示Cookie。
-   **header**：表示Header。 |
|value

|String

|test

|参数取值，根据**type**和**name**得到的值跟这个值进行比较。 |
|operator

|String

|rawvalue

|运算符，取值说明如下：

 -   **rawvalue**：表示直接比较。
-   **list**：表示白名单。
-   **mod**：表示对100取模。
-   **deterministic\_proportional\_steaming\_division**：表示百分比。 |

-   **DubboRules参数说明**

|参数名称

|类型

|示例

|描述 |
|------|----|----|----|
|condition

|String

|OR

|灰度规则的条件模式，取值说明如下：

 -   **AND**：表示与，即同时满足条件列表中的所有条件。
-   **OR**：表示或，即满足条件列表中的任一条件。 |
|methodName

|String

|echo

|Dubbo服务的方法名。 |
|serviceName

|String

|com.alibaba.edas.boot.EchoService

|Dubbo服务名称。 |
|version

|String

|1.0.0

|Dubbo服务版本。 |
|items

|Array of items

| |条件列表。 |
|group

|String

|DUBBO

|灰度规则对应的Dubbo服务的分组。 |

**items参数说明**

|参数名称

|类型

|示例

|描述 |
|------|----|----|----|
|index

|Integer

|0

|参数编号，0表示第一个参数。 |
|expr

|String

|.name

|参数值获取表达式。取值说明如下：

 -   **留空**：表示直接取当前参数的值。
-   **.name**：表示取参数的name属性，相当于args0.getName\(\)。
-   **.isEnabled\(\)** ：表示取参数的enabled属性，相当于args0.isEnabled\(\)。
-   **\[0\]**：表示当前参数应是一个数组，取数组的第一个值，相当于args0\[0\]，注意开始没有英文句点（.）。
-   **.get\(0\)**：表示当前参数应是一个List，取List的第一个值，相当于args0.get\(0\)。
-   **.get\("key"\)**：表示当前参数是一个Map，获取key对应的值，相当于args0.get\("key"\)。 |
|cond

|String

|==

|比较操作符。可取值：**\>**、**<**、**\>=**、**<=**、**==**以及**!=**。 |
|value

|String

|test

|参数取值，根据**expr**和**index**得到的值跟这个值进行比较。 |
|operator

|String

|rawvalue

|运算符，取值说明如下：

 -   **rawvalue**：表示直接比较。
-   **list**：表示白名单。
-   **mod**：表示对100取模。
-   **deterministic\_proportional\_steaming\_division**：表示百分比。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|9D29CBD0-45D3-410B-9826-52F86F90\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |灰度规则信息。 |
|GreyTagRouteId|Long|16|灰度规则ID，全局唯一。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|查询变更单信息是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |

## 示例

请求示例

```
PUT /pop/v1/sam/tagroute/greyTagRoute?Description=灰度发布-地域灰度&ScRules=[{"condition":"OR","items":[{"cond":"==","name":"grey","operator":"rawvalue","type":"param","value":"true"},{"cond":"==","name":"grey","operator":"rawvalue","type":"cookie","value":"true"},{"cond":"==","name":"grey","operator":"rawvalue","type":"header","value":"true"}],"path":"/post-echo/hi"}]&DubboRules=[{"condition":"OR","group":"DUBBO","items":[{"cond":"==","expr":".key1","index":0,"operator":"rawvalue","value":"value1"},{"cond":"==","expr":".key2","index":0,"operator":"rawvalue","value":"value2"}],"methodName":"echo","serviceName":"com.alibaba.edas.boot.EchoService","version":"1.0.0"}] HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UpdateGreyTagRouteResponse>
    <RequestId>9D29CBD0-45D3-410B-9826-52F86F90****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <GreyTagRouteId>16</GreyTagRouteId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</UpdateGreyTagRouteResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "9D29CBD0-45D3-410B-9826-52F86F90****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : {
    "GreyTagRouteId" : 16
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

