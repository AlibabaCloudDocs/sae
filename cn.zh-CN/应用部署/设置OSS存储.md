# 设置OSS存储

相比于NAS，OSS提供了便捷的工具以及控制台，支持可视化地管理Bucket，并在解决应用实例数据持久化和实例间数据分发问题的基础上，进一步降低成本。本文提供设置OSS存储的操作步骤。

-   [开通OSS服务](/cn.zh-CN/控制台用户指南/开通OSS服务.md)
-   [创建存储空间](/cn.zh-CN/控制台用户指南/存储空间管理/创建存储空间.md)
-   [创建AccessKey]()

## 应用部署时配置OSS存储

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击**创建应用**。

3.  在**应用基本信息**页签设置应用相关信息，并单击**下一步：应用部署配置**。

4.  在**应用部署配置**页签，选择**技术栈语言**和**应用部署方式**，设置部署参数。

5.  展开**持久化存储**区域，单击**OSS对象存储**页签。

6.  填写**AccessKey ID**和**AccessKey Secret**。

    **说明：** 强烈建议您遵循阿里云安全最佳实践，使用RAM用户的AccessKey调用OSS接口，并确保授予该RAM用户访问OSS资源的最小权限。例如，您需要该RAM用户只读test-sae Bucket的oss-test/目录，那么您可以授予该RAM用户以下最小权限：

    ```
    {
        "Statement": [
            {
                "Action": "oss:GetBucket",
                "Effect": "Allow",
                "Resource": "test-sae"
            },
            {
                "Action": "oss:GetObject",
                "Effect": "Allow",
                "Resource": "oss-test/"
            }
        ],
        "Version": "1"
    }
    ```

7.  单击**添加**，并配置以下参数。

    |参数|说明|示例值|
    |--|--|---|
    |Bucket|您在OSS创建的Bucket。|bucketname|
    |挂载目录|您在OSS创建的目录或OSS对象，如果OSS挂载目录不存在，会触发异常。|示例如下：    -   tmp/oss-test/
    -   tmp/oss-demo.log |
    |容器路径|您在SAE的容器路径。如果路径已存在，为覆盖关系；如果路径不存在，会新建。|k8s/demo/|
    |权限|容器路径对挂载目录资源的权限，取值如下：    -   只读
    -   读写
|只读|

8.  单击**下一步：确认规格**。

9.  在**确认规格**页签，查看您所创建应用的详细信息以及配置费用情况，并单击**确认创建**。


## 应用部署完成后配置OSS存储

您可以在创建应用过程中配置OSS存储，也可以在应用部署完成后配置。

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击具体应用名称。

3.  在应用详情页面的右上角，单击**部署应用**。

4.  展开**持久化存储**区域，单击**OSS对象存储**页签。

5.  填写**AccessKey ID**和**AccessKey Secret**。

    **说明：** 强烈建议您遵循阿里云安全最佳实践，使用RAM用户的AccessKey调用OSS接口，并确保授予该RAM用户访问OSS资源的最小权限。例如，您需要该RAM用户只读test-sae Bucket的oss-test/目录，那么您可以授予该RAM用户以下最小权限：

    ```
    {
        "Statement": [
            {
                "Action": "oss:GetBucket",
                "Effect": "Allow",
                "Resource": "test-sae"
            },
            {
                "Action": "oss:GetObject",
                "Effect": "Allow",
                "Resource": "oss-test/"
            }
        ],
        "Version": "1"
    }
    ```

6.  单击**添加**，并配置以下参数。

    |参数|说明|示例值|
    |--|--|---|
    |Bucket|您在OSS创建的Bucket。|bucketname|
    |挂载目录|您在OSS创建的目录或OSS对象，如果OSS挂载目录不存在，会触发异常。|示例如下：    -   tmp/oss-test/
    -   tmp/oss-demo.log |
    |容器路径|您在SAE的容器路径。如果路径已存在，为覆盖关系；如果路径不存在，会新建。|k8s/demo/|
    |权限|容器路径对挂载目录资源的权限，取值如下：    -   只读
    -   读写
|只读|

7.  单击**确认**。


## 结果验证

本文介绍不同系统下验证OSS挂载是否成功的方式，您可以根据实际需要选择验证方式：

-   从变更详情判断。

    如果单次创建或部署的变更已经成功，变更生成的新的实例没有出现异常事件，则说明OSS挂载成功。

    ![sae挂载nas成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0510723061/p70176.png)

-   从容器角度判断。

    在Webshell执行以下命令查询应用中是否存在OSS挂载信息。

    ```
    cat /proc/mounts | grep ossfs
    ```

    当显示如下信息时，表示OSS挂载成功。

    ![oss_success](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8721549161/p268614.png)

-   从业务角度判断。

    在Webshell中，对挂载OSS文件系统路径进行操作，如果可以从OSS控制台同步看到，则说明OSS挂载成功。


## 取消挂载OSS

挂载OSS后，如果您不再使用OSS存储，可以取消挂载OSS。您可以执行[应用部署时配置OSS存储](#section_8dz_nai_u49)的[步骤1](#step_r4x_jti_nuo)~[步骤4](#step_x8f_k42_ydl)，找到需要取消挂载的OSS配置，在其**操作**列，单击![oss-mount-delete-icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5430549161/p268612.png)图标。

**说明：**

-   取消挂载OSS后，SAE会重新部署应用，请在业务较少的时间段配置。
-   在SAE控制台取消挂载OSS后，您在OSS中所存储的数据仍然存在，不会被删除。

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索钉钉群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1176199061/p72048.png)

