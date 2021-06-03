# 通过RAM角色实现跨云账号授权

本文介绍如何创建可信实体为阿里云账号的RAM角色，来实现跨账号授权访问SAE资源。

## 应用场景

企业A开通了Serverless应用引擎服务，并希望将部分业务授权给企业B。需求如下：

-   企业A希望能专注于业务系统，仅作为Serverless应用引擎的资源所有者；而将部分业务授权给企业B，例如应用发布、应用管理、自动弹性、一键启停应用和应用监控等服务。
-   企业A希望当企业B的员工加入或离职时，无需做任何权限变更。企业B可以进一步将A的资源访问权限分配给企业B的RAM用户，并可以精细控制其员工或应用对资源的访问和操作权限。
-   企业A希望如果双方合同终止，企业A随时可以撤销对企业B的授权。

## 解决方案

企业A需要授予企业B的员工对Serverless应用引擎的资源进行操作。假设企业A和企业B分别有一个阿里云账号A和阿里云账号B，需要完成以下操作来实现企业A和企业B的跨云账号授权及资源访问：

1.  [步骤一：创建RAM角色并授权](#section_nkr_a9e_6qj)

    阿里云账号A创建一个RAM角色并根据业务范围和需求为RAM角色授予对应的权限，并允许阿里云账号B下的RAM用户扮演该角色。

2.  [步骤二：跨云账号访问资源](#section_trg_h5j_uns)

    RAM角色授权完成后，阿里云账号B下的RAM用户通过扮演RAM角色可获取该角色对应的权限。RAM用户可通过以下方式访问阿里云账号A的资源：

    -   通过控制台访问资源
    -   通过SDK访问资源

## 步骤一：创建RAM角色并授权

假设企业A需要为企业B授予只读权限，且企业A和企业B名下分别有一个阿里云账号A和阿里云账号B。

-   企业A的阿里云账号ID为`123456789098****`，账号别名（企业别名）为`company-a`。
-   企业B的阿里云账号ID为`234567890987****`，账号别名（企业别名）为`company-b`。

1.  企业A使用阿里云账号A登录[RAM控制台](https://ram.console.aliyun.com/overview)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  在RAM角色管理页面，单击**创建RAM角色**。

4.  在创建RAM角色面板，选择可信实体类型为**阿里云账号**，然后单击**下一步**。

5.  输入**角色名称**和**备注**，例如设置**角色名称**为sae-admin，选择云账号为**其他云账号**并输入企业B的阿里云账号B。

6.  单击**完成**。

    若界面跳转至创建RAM角色面板的**创建完成**界面，表示RAM角色创建成功。RAM角色创建成功后，您可以在该角色的基本信息页面查看该角色的信息，包括RAM角色名称、创建时间和ARN等。

    -   RAM角色名称：sae-admin
    -   ARN：`acs:ram::123456789098****:role/sae-admin`。
    -   信任策略：

        **说明：** 以下策略表示仅允许阿里云账号B下的RAM用户来扮演该RAM角色。

        ```
        {
          "Statement": [
            {
              "Action": "sts:AssumeRole",
              "Effect": "Allow",
              "Principal": {
                "RAM": [
                  "acs:ram::234567890987****:root"
                ]
              }
            }
          ],
          "Version": "1"
        }
        ```

7.  企业A的阿里云账号A为RAM角色sae-admin添加AliyunSAEReadOnlyAccess权限。具体操作，请参见[为RAM角色授权](/cn.zh-CN/角色管理/为RAM角色授权.md)。


1.  使用企业B的阿里云账号B登录[RAM控制台](https://ram.console.aliyun.com/overview)。

2.  企业B的阿里云账号B创建RAM用户。具体操作，请参见[创建RAM用户](/cn.zh-CN/用户管理/基本操作/创建RAM用户.md)。

3.  企业B为RAM用户添加AliyunSTSAssumeRoleAccess权限，RAM用户就可以扮演企业A创建的RAM角色。具体操作，请参见[为RAM用户授权](/cn.zh-CN/用户管理/授权管理/为RAM用户授权.md)。


企业B的阿里云账户B下的RAM用户在登录后，可以通过切换身份的方式扮演RAM角色，达到访问企业A的阿里云账户A的资源的目的。

1.  使用阿里云账号B的RAM用户登录[RAM控制台](https://signin.aliyun.com/login.htm)。

2.  将鼠标悬停在右上角头像的位置，查看**企业别名**并保存，然后单击**切换身份**。

3.  在**角色切换**页面，输入**企业别名**和**角色名**。

    **说明：** 在**角色切换**页面，除了输入企业别名（账号别名），您也可以输入默认域名或阿里云账号进行角色切换。关于如何查看默认域名，请参见[查看和修改默认域名](/cn.zh-CN/安全设置/高级设置/查看和修改默认域名.md)。本文示例中需要输入的**企业别名**为企业A的阿里云账号A，**角色名**为企业B的阿里云账号B下的RAM角色名称。


若企业A与企业B的合作终止，企业A只需移除为阿里云账号B创建的RAM角色的权限，那么阿里云账号B下的所有RAM用户将失去以RAM角色的身份访问阿里云账号A资源的能力。

1.  使用企业A的阿里云账号A登录[RAM控制台](https://ram.console.aliyun.com/overview)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  在RAM角色管理页面，选择目标RAM角色，在**操作**列单击**删除**。


**说明：** 在删除RAM角色前，需要先为RAM角色移除授权。具体操作，请参见[为RAM角色移除权限](/cn.zh-CN/角色管理/为RAM角色移除权限.md)。

## 步骤二：跨云账号访问资源

阿里云临时安全令牌STS（Security Token Service）是阿里云提供的一种临时访问权限管理服务。通过STS服务，您所授权的身份主体（RAM用户或RAM角色）可以获取一个自定义时效和访问权限的临时访问令牌。STS令牌持有者可以通过以下方式访问阿里云资源：

-   登录阿里云控制台操作被授权的云资源。
-   通过编程方式访问被授权的阿里云服务API。

企业B的RAM用户可按照以下步骤登录控制台，达到访问企业A的Serverless应用引擎资源的目的。

1.  使用阿里云账号B的RAM用户登录[RAM控制台](https://signin.aliyun.com/login.htm)。
2.  在**RAM用户登录**页面上，输入RAM用户登录名称，单击**下一步**，并输入RAM用户密码，然后单击**登录**。

    **说明：** RAM用户登录名称的格式为`<$username>@<$AccountAlias>`或`<$username>@<$AccountAlias>.onaliyun.com`。`<$AccountAlias>`为账号别名，如果没有设置账号别名，则默认值为阿里云账号的ID。更多信息，请参见[RAM用户登录控制台](/cn.zh-CN/用户管理/登录管理/RAM用户登录控制台.md)。

3.  在阿里云控制台登录页面，将鼠标指针移到右上角头像上，并在浮层中单击**切换身份**。
4.  在**阿里云－角色切换**页面，输入企业A的**企业别名**或**默认域名**，以及**角色名**，然后单击**提交**。
5.  对企业A的Serverless应用引擎资源进行操作。

1.  通过Java SDK示例代码获取访问凭证。更多信息，请参见[Java示例](/cn.zh-CN/SDK参考/SDK参考（STS）/Java示例.md)和[AssumeRole](/cn.zh-CN/API参考/API 参考（STS）/操作接口/AssumeRole.md)。

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    import java.util.*;
    import com.aliyuncs.sts.model.v20150401.*;
    
    public class AssumeRole {
    
        public static void main(String[] args) {
            //构建一个阿里云客户端，用于发起请求。
            //构建阿里云客户端时需要设置AccessKey ID和AccessKey Secret。
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            //构造请求，设置参数。关于参数含义和设置方法，请参见API参考。
            AssumeRoleRequest request = new AssumeRoleRequest();
            request.setRegionId("cn-hangzhou");
            request.setRoleArn("<RoleArn>");
            request.setRoleSessionName("<RoleSessionName>");
            
            //发起请求，并得到响应。
            try {
                AssumeRoleResponse response = client.getAcsResponse(request);
                System.out.println(new Gson().toJson(response));
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
    
        }
    }            
    ```

    **说明：** SAE的API支持HTTP调用、SDK调用和OpenAPI开发者门户调用。 更多信息，请参见[API概览](/cn.zh-CN/API参考/API概览.md)和[调用方式](/cn.zh-CN/API参考/调用方式.md)。

2.  预期输出。

    ```
    {
      "RequestId": "964E0EC5-575B-4FF5-8FD0-D4BD8025****",
      "AssumedRoleUser": {
        "Arn": "acs:ram::*************",
        "AssumedRoleId": "*************"
      },
      "Credentials": {
        "SecurityToken": "*************",
        "AccessKeyId": "STS.*************",
        "AccessKeySecret": "*************",
        "Expiration": "2021-05-28T11:23:19Z"
      }
    }
    ```

3.  依据所返回的访问密钥等信息，在阿里云账号B的代码中，生成新的Clinet，使其RAM用户有权限查看阿里云账号A下SAE华东1（杭州）地域的所有命名空间服务。

    ```
    public class CreateNamespace {
        public static void main(String[] args) {
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            CommonRequest request = new CommonRequest();
            //request.setProtocol(ProtocolType.HTTPS);
            request.setMethod(MethodType.POST);
            request.setDomain("sae.cn-shanghai.aliyuncs.com");
            request.setVersion("2019-05-06");
            request.setUriPattern("/pop/v1/paas/namespace");
    
            request.putHeadParameter("Content-Type", "application/json");
            String requestBody = "" + "{}";
            request.setHttpContent(requestBody.getBytes(), "utf-8", FormatType.JSON);
            try {
                CommonResponse response = client.getCommonResponse(request);
                System.out.println(response.getData());
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                e.printStackTrace();
            }
        }
    }
    ```


