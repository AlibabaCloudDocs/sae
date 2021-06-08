# ListGreyTagRoute

调用ListGreyTagRoute接口根据应用ID查询灰度规则详情。

**说明：** 目前一个应用只能配置一条灰度规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListGreyTagRoute&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/tagroute/greyTagRouteList HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|7171a6ca-d1cd-4928-8642-7d5cfe69\*\*\*\*|应用ID。 |

-   **ScRule参数说明**

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

|Spring Cloud应用灰度规则对应的path。 |
|items

|Array of items

| |条件列表。 |

**Item参数说明**

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

-   **DubboRule参数说明**

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

**Item参数说明**

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

|参数值获取表达式。语法遵循SpEL（link）表达式，取值说明如下：

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
|CurrentPage|Integer|1|当前页码。 |
|PageSize|Integer|1|每页显示的数量。目前只能为**1**。 |
|TotalSize|Long|1|总个数。目前只能为**1**。 |
|Result|Array of result| |返回结果。 |
|GreyTagRouteId|Long|1|规则ID。 |
|Name|String|rule-name|规则名称。 |
|Description|String|test|规则描述。 |
|ScRules|Array of scRule| |Spring Cloud灰度规则。 |
|path|String|/path|Spring Cloud应用灰度规则对应的路径。 |
|condition|String|OR|灰度规则的条件模式，取值说明如下：

 -   **AND**：表示与，即同时满足条件列表中的所有条件。
-   **OR**：表示或，即满足条件列表中的任一条件。 |
|items|Array of item| |条件列表。 |
|type|String|cookie|比较类型，取值说明如下：

 -   **param**：表示Parameter。
-   **cookie**：表示Cookie。
-   **header**：表示Header。 |
|name|String|test|参数名。 |
|operator|String|rawvalue|运算符，取值说明如下：

 -   **rawvalue**：表示直接比较。
-   **list**：表示白名单。
-   **mod**：表示对100取模。
-   **deterministic\_proportional\_steaming\_division**：表示百分比。 |
|value|String|test|参数取值，根据**type**和**name**得到的值跟这个值进行比较。 |
|cond|String|==|比较操作符。可取值：**\>**、**<**、**\>=**、**<=**、**==**以及**!=**。 |
|index|Integer|N/A|Spring Cloud应用不涉及。 |
|expr|String|N/A|Spring Cloud应用不涉及。 |
|DubboRules|Array of dubboRule| |Dubbo服务灰度规则。 |
|serviceName|String|com.alibaba.edas.boot.EchoService|Dubbo服务名称。 |
|group|String|DUBBO|灰度规则对应的Dubbo服务的分组。 |
|version|String|1.0.0|Dubbo服务版本。 |
|methodName|String|echo|Dubbo服务的方法名。 |
|condition|String|OR|灰度规则的条件模式，取值说明如下：

 -   **AND**：表示与，即同时满足条件列表中的所有条件。
-   **OR**：表示或，即满足条件列表中的任一条件。 |
|items|Array of item| |条件列表。 |
|index|Integer|0|参数编号，0表示第一个参数。 |
|expr|String|.name|参数值获取表达式。语法遵循SpEL（link）表达式，取值说明如下：

 -   **留空**：表示直接取当前参数的值。
-   **.name**：表示取参数的name属性，相当于args0.getName\(\)。
-   **.isEnabled\(\)**：表示取参数的enabled属性，相当于args0.isEnabled\(\)。
-   **\[0\]**：表示当前参数应是一个数组，取数组的第一个值，相当于args0\[0\]，注意开始没有英文句点（.）。
-   **.get\(0\)**：表示当前参数应是一个List，取List的第一个值，相当于args0.get\(0\)。
-   **.get\("key"\)**：表示当前参数是一个Map，获取key对应的值，相当于args0.get\("key"\)。

**说明：** 关于参数值获取表达式的更多信息，请参见[Spring Expression Language \(SpEL\)](https://docs.spring.io/spring-integration/docs/current/reference/html/spel.html)。 |
|operator|String|rawvalue|运算符，取值说明如下：

 -   **rawvalue**：表示直接比较。
-   **list**：表示白名单。
-   **mod**：表示对100取模。
-   **deterministic\_proportional\_steaming\_division**：表示百分比。 |
|value|String|test|参数取值，根据**expr**和**index**得到的值跟这个值进行比较。 |
|cond|String|==|比较操作符。可取值：**\>**、**<**、**\>=**、**<=**、**==**以及**!=**。 |
|type|String|N/A|Dubbo服务不涉及。 |
|name|String|N/A|Dubbo服务不涉及。 |
|CreateTime|Long|1619007592013|规则被创建的时间戳。单位：毫秒。 |
|UpdateTime|Long|1609434061000|规则被更新的时间戳。单位：毫秒。 |
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
GET /pop/v1/sam/tagroute/greyTagRouteList?AppId=7171a6ca-d1cd-4928-8642-7d5cfe69**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListGreyTagRouteResponse>
    <RequestId>9D29CBD0-45D3-410B-9826-52F86F90****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <CurrentPage>1</CurrentPage>
        <PageSize>1</PageSize>
        <TotalSize>1</TotalSize>
        <Result>
            <GreyTagRouteId>1</GreyTagRouteId>
            <Name>rule-name</Name>
            <Description>test</Description>
            <ScRules>
                <path>/path</path>
                <condition>OR</condition>
                <items>
                    <type>cookie</type>
                    <name>test</name>
                    <operator>rawvalue</operator>
                    <value>test</value>
                    <cond>==</cond>
                </items>
            </ScRules>
            <DubboRules>
                <serviceName>com.alibaba.edas.boot.EchoService</serviceName>
                <group>DUBBO</group>
                <version>1.0.0</version>
                <methodName>echo</methodName>
                <condition>OR</condition>
                <items>
                    <index>0</index>
                    <expr>.name</expr>
                    <operator>rawvalue</operator>
                    <value>test</value>
                    <cond>==</cond>
                </items>
            </DubboRules>
            <CreateTime>1619007592013</CreateTime>
            <UpdateTime>1609434061000</UpdateTime>
        </Result>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListGreyTagRouteResponse>
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
    "CurrentPage" : 1,
    "PageSize" : 1,
    "TotalSize" : 1,
    "Result" : [ {
      "GreyTagRouteId" : 1,
      "Name" : "rule-name",
      "Description" : "test",
      "ScRules" : [ {
        "path" : "/path",
        "condition" : "OR",
        "items" : [ {
          "type" : "cookie",
          "name" : "test",
          "operator" : "rawvalue",
          "value" : "test",
          "cond" : "=="
        } ]
      } ],
      "DubboRules" : [ {
        "serviceName" : "com.alibaba.edas.boot.EchoService",
        "group" : "DUBBO",
        "version" : "1.0.0",
        "methodName" : "echo",
        "condition" : "OR",
        "items" : [ {
          "index" : 0,
          "expr" : ".name",
          "operator" : "rawvalue",
          "value" : "test",
          "cond" : "=="
        } ]
      } ],
      "CreateTime" : 1619007592013,
      "UpdateTime" : 1609434061000
    } ]
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

