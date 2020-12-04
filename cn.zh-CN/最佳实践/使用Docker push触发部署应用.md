# 使用Docker push触发部署应用

如果您没有持续交付流程，您可以参考本文快速搭建用于测试的持续交付环境，只需要执行docker push \{image\}命令就能免费将镜像部署到SAE。如果您正在建设持续交付流程，也可以参考本文，自定义自动触发部署镜像到SAE的方案。

-   [开通SAE产品](/cn.zh-CN/快速入门/准备工作.md)，并部署一个镜像类型的应用。目前SAE支持部署所有技术栈的镜像，其中Java与PHP技术栈，SAE做了比较深度的增强。如果您有兴趣体验SAE产品，您可以在[SAE控制台](https://sae.console.aliyun.com/)创建SAE应用。具体操作，请参见[在SAE控制台创建应用](/cn.zh-CN/快速入门/普通应用入门/将Demo应用部署到SAE.md)。
-   [开通容器镜像服务](https://cr.console.aliyun.com/)，并创建一个命名空间以及镜像仓库。命名空间以及镜像仓库建议是私有的，尤其是生产环境，保证你的代码不会泄露。阿里云容器镜像服务提供免费的默认实例，可以免费创建命名空间以及镜像仓库，储存镜像。具体操作，请参见[构建仓库与镜像]()。
-   [开通函数计算](https://fc.console.aliyun.com/)，阿里云函数计算产品是一个收费产品，但每月有100万次的免费调用额度，您可以使用免费额度触发部署应用，无需支付其他费用。

本文以搭建一个简单的事件驱动的持续交付函数为例，全程不需要编写一行代码，实现捕获镜像提交事件，并触发云函数，将镜像部署到SAE等操作，耗时不到10分钟。

Java函数的下载地址，请参见[函数](http://sae-public.oss-cn-hangzhou.aliyuncs.com/demo/fc-deploy-trigger/deploy-trigger-1.0-SNAPSHOT.jar)；源代码的下载地址，请参见[源代码](https://github.com/AndyManastorm/sae-deploy-trigger)。

## 步骤一：创建部署应用的云函数DeployTrigger

1.  创建函数。

    1.  登录[函数计算控制台](https://fc.console.aliyun.com)。

    2.  在顶部菜单栏，选择地域。

    3.  在左侧导航栏中，单击**服务/函数**。在**服务/函数**页面左上角单击**新增函数**。

    4.  在**新增函数**页面，单击**HTTP函数**，然后单击**下一步**。

        ![新建HTTP函数](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2559026061/p184859.png)

    5.  在**配置函数**区域，填写函数相关信息。

        ![新建函数 ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2559026061/p184662.png)

        |参数|操作|
        |--|--|
        |所在服务|        -   如果您已经创建了一个用于测试的服务，且不介意将DeployTrigger加入到这个服务，您可以在列表中选择已创建的服务。
        -   如果您没有创建服务，您可以直接输入服务名称，函数计算将自动为您创建该服务。 |
        |函数名称|填写**DeployTrigger**。|
        |运行环境|选择**java8**。|
        |代码上传方式|选择**代码包上传**，单击**选择文件**，上传函数文件。Java函数的下载地址，请参见[函数](http://sae-public.oss-cn-hangzhou.aliyuncs.com/demo/fc-deploy-trigger/deploy-trigger-1.0-SNAPSHOT.jar)。|
        |函数实例类型|选择**弹性实例**。|
        |函数入口|填写**com.aliyun.serverless.DeployTrigger::handleRequest**。|
        |函数执行内存|设置函数执行内存。|
        |超时时间|设置超时时间。默认超时时间为60秒，最长为600秒。超过设置的超时时间，函数将以执行失败结束。 |
        |实例并发度|设置为**10**。|

    6.  在**配置触发器**区域，设置触发器信息，单击**完成**。

        ![设置触发器](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2559026061/p184877.png)

        |参数|操作|
        |--|--|
        |触发器名称|填写**AnonymousTriggerForRegistry**。|
        |认证方式|选择**anonymous**。|
        |请求方式|选择**POST**。|

2.  修改服务配置，添加调用SAE产品的权限。

    1.  在**服务/函数**页面找到目标服务，单击**服务配置**，在**服务配置**页签单击**修改**。

        ![修改服务](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8758126061/p184895.png)

    2.  在**配置服务**页面的**权限配置**区域，添加SAE产品的调用权限**AliyunSAEFullAccess**。具体操作，请参见[配置服务权限]()。

        如果您需要进一步精细化授权，您可以给角色授予部分需要部署的应用的修改权限。更多信息，请参见[应用权限管理](/cn.zh-CN/应用管理/应用权限管理.md)。

        -   添加权限时，如果您已经创建了SAE读写权限的角色，您可以直接添加服务权限。具体操作，请参见[配置服务权限]()。
        -   如果您没有搜索到SAE读写权限的角色，您需要先登录[RAM控制台](https://ram.console.aliyun.com/overview)创建角色并授权。具体操作，请参见以下文档：
            1.  [创建可信实体为阿里云服务的RAM角色](/cn.zh-CN/角色管理/创建RAM角色/创建可信实体为阿里云服务的RAM角色.md)

                创建RAM角色时，**受信服务**选择**函数计算**。

                ![创建RAM角色](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2559026061/p184914.png)

            2.  [为RAM角色授权](/cn.zh-CN/角色管理/为RAM角色授权.md)

                为RAM角色授予**AliyunSAEFullAccess**权限。

                ![RAM角色授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2559026061/p184915.png)

3.  修改函数配置，添加环境变量。

    1.  在**服务/函数**页面找到目标函数，单击**操作**列的**配置**。

        ![修改函数](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8758126061/p184916.png)

    2.  在**配置函数**页面的**环境变量**区域，添加**ACCESS\_TOKEN**环境变量，输入函数访问鉴权的自定义Token，单击**提交**。

        您可以使用uuidgen命令（oxs系统）或在互联网上寻找生成UUID的网页生成Token。

        ![添加环境变量](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8758126061/p184919.png)

4.  获取函数的访问地址。

    1.  在**服务/函数**页面找到目标函数，单击函数名称。

    2.  单击**代码执行**页签，在**调试TTP触发器**区域复制函数的访问地址。

        ![获取域名](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8758126061/p184964.png)

    **说明：** 为了节约成本，您可以直接使用函数计算提供的域名。函数计算每天提供1000次的域名额度，能够满足您测试环境部署场景的需求。


## 步骤二：创建镜像推送触发器

1.  登录[容器镜像服务控制台](https://cr.console.aliyun.com)。

2.  在左侧导航栏选择**默认实例** \> **镜像仓库**，在**镜像仓库**页面单击目标镜像仓库。

3.  在仓库详情页面的左侧导航栏单击**触发器**，在触发器页面右上角单击**创建**。

4.  在**创建触发器**对话框中输入**名称**及**触发器URL**，选择**触发方式**为**全部触发**，单击**确认**。

    ![创建触发器](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8758126061/p184971.png)

    **说明：** **触发器URL**中要包含鉴权的Token以及要部署的SAE应用ID。


## 步骤三：验证部署结果

在本地执行推送镜像后，您可以观察到SAE应用会产生一条变更记录，推送的镜像被重新部署到了SAE。

![镜像推送](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2559026061/p184927.png)

![SAE应用记录](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3559026061/p184928.png)

