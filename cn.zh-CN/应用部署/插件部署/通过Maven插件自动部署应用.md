# 通过Maven插件自动部署应用

您可以通过Maven的toolkit-maven-plugin插件完成SAE应用的自动化部署。本文介绍通过Maven自动化部署应用的操作步骤及典型场景示例。

-   已下载并安装Maven。更多信息，请参见[Maven](http://maven.apache.org/download.cgi)。
-   已在[SAE控制台](https://sae.console.aliyun.com)上部署应用。更多信息，请参见以下文档：
    -   [在SAE控制台使用WAR包部署Java Web应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用WAR包部署Java Web应用.md)
    -   [在SAE控制台使用JAR包部署微服务应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用JAR文件部署微服务应用.md)
    -   [在SAE控制台使用镜像部署PHP应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用镜像部署PHP应用.md)

Cloud Toolkit的更多信息，请参见[什么是Alibaba Cloud Toolkit]()。

## 典型场景示例

本章节介绍通过Maven插件自动部署应用的典型部署场景及相关配置文件示例。关于自动部署应用的操作步骤，请参见[操作步骤](#section_hyw_lyq_yrn)。

-   场景一：本地构建WAR或FatJAR包并部署

    例如您在北京环境有WAR类型的应用，期望在本地使用WAR包部署应用。文件打包和部署配置如下。

    -   打包文件

        ```
        apiVersion: V1
        kind: AppPackage
        spec:
          packageType: War                                    
        ```

    -   部署文件

        ```
        apiVersion: V1
        kind: AppDeployment
        spec:
          type: serverless
          target:
            appId:        #部署应用的ID。如果配置了该参数则无需配置namespaceId和appName。
            namespaceId:  #应用所属命名空间ID。如果您不清楚应用ID，可使用应用所属命名空间及应用名称进行部署。
            appName:      #应用名称。如果您不清楚应用ID，可使用应用名称及命名空间进行部署。                                      
        ```

-   场景二：使用已有镜像地址部署镜像类型应用

    例如您在北京环境有一个镜像类型应用，期望使用已有的镜像部署应用。文件打包和部署配置如下。

    -   打包文件

        ```
        apiVersion: V1
        kind: AppPackage
        spec:
          packageType: Image
          imageUrl: registry.cn-beijing.aliyuncs.com/test/gateway:latest  #镜像地址。                                    
        ```

    -   部署文件

        ```
        apiVersion: V1
        kind: AppDeployment
        spec:
          type: serverless
          target:
            appId:        #部署应用的ID。如果配置了该参数则无需配置namespaceId和appName。
            namespaceId:  #应用所属命名空间ID。如果您不清楚应用ID，可使用应用所属命名空间及应用名称进行部署。
            appName:      #应用名称。如果您不清楚应用ID，可使用应用名称及命名空间进行部署。                                  
        ```

-   场景三：本地构建镜像上传至仓库并部署应用

    例如您在北京环境有镜像类型应用，期望在本地编译并构建为镜像，然后上传到阿里云镜像仓库部署应用。文件打包和部署配置如下。

    -   打包文件

        ```
        apiVersion: V1
        kind: AppPackage
        spec:
          packageType: Image
          build:
            docker:
               dockerfile: Dockerfile #指定Dockerfile。
               imageRepoAddress:      #镜像仓库地址。
               imageTag:              #镜像Tag。
               imageRepoUser:         #镜像仓库用户名。
               imageRepoPassword:     #镜像仓库密码。                                  
        ```

    -   部署文件

        ```
        apiVersion: V1
        kind: AppDeployment
        spec:
          type: serverless
          target:
            appId:        #部署应用的ID。如果配置了该参数则无需配置namespaceId和appName。
            namespaceId:  #应用所属命名空间ID。如果您不清楚应用ID，可使用应用所属命名空间及应用名称进行部署。
            appName:      #应用名称。如果您不清楚应用ID，可使用应用名称及命名空间进行部署。                                      
        ```


## 操作步骤

1.  在您的打包工程的pom.xml文件中添加插件依赖。

    ```
    <build>
        <plugins>
            <plugin>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>toolkit-maven-plugin</artifactId>
                <version>1.1.2</version>
            </plugin>
        </plugins>
    </build>                            
    ```

    **说明：** 建议您使用1.1.2及以上版本的toolkit-maven-plugin。

2.  配置插件信息。

    配置插件信息主要包括配置账号、打包和部署信息。更多信息，请参见[更多配置项](#section_cr2_4vo_awr)。

    1.  配置账号信息。

        在打包工程的根目录下创建文件格式为`YAML`的账号配置文件，命名为`toolkit_profile.yaml`并输入以下信息。

        ```
        regionId:        #应用所在地域。
        accessKeyId:     #访问阿里云资源的AccessKey ID，建议您使用子账号的AccessKey ID降低安全风险。
        accessKeySecret: #访问阿里云资源的AccessKey Secret，建议您使用子账号的AccessKey Secret降低安全风险。                                    
        ```

    2.  配置打包信息。

        在打包工程的根目录下创建文件格式为`YAML`的打包配置文件。如果打包工程为Maven的子模块，则需要在子模块的目录下创建该文件，并命名为`toolkit_package.yaml`，输入以下信息。

        ```
        apiVersion: V1
        kind: AppPackage
        spec:
         packageType: #应用部署包类型，支持**War**、**FatJar**、**Image**、**url**。您只有在该处配置了url，那么packageUrl才能生效。
         packageUrl:  #部署包地址，**War**、**FatJar**类型应用可配置。不填则使用当前Maven构建的包进行部署。
         imageUrl:    #如果部署包类型为**Image**，可配置此字段。**Image**类型也可以在本地构建Docker镜像进行部署，更多信息，请参见[更多配置项](#section_cr2_4vo_awr)。                                   
        ```

    3.  配置部署信息。

        在打包工程的根目录下创建文件格式为`YAML`的部署文件，命名为`toolkit_deploy.yaml`，并输入以下信息。

        ```
        apiVersion: V1
        kind: AppDeployment
        spec:
         type: serverless
         target:
           appId:        #部署应用的ID。如果配置了该参数则无需配置namespaceId和appName。
           namespaceId:  #应用所属命名空间ID。如果您不清楚应用ID，可使用应用所属命名空间及应用名称进行部署。
           appName:      #应用名称。如果您不清楚应用ID，可使用应用名称及命名空间进行部署。                                   
        ```

3.  进入pom.xml所在的目录，执行以下命令构建部署工程。

    **说明：** 如果部署的是Maven子模块，则需要进入子模块pom.xml文件所在的目录执行部署工程。

    ```
    mvn clean package toolkit:deploy -Dtoolkit_profile=toolkit_profile.yaml -Dtoolkit_package=toolkit_package.yaml -Dtoolkit_deploy=toolkit_deploy.yaml                           
    ```

    命令参数说明如下。

    |参数|说明|
    |--|--|
    |toolkit:deploy|打包完成后进行应用部署。|
    |-Dtoolkit\_profile|指定账号配置文件。如果账号文件与pom.xml在同一个目录下，且名字为`.toolkit_profile.yaml`，可不填写该参数，插件会自动获取。**说明：** 插件自动获取的`.toolkit_profile.yaml`文件名最前面包含英文句号。 |
    |-Dtoolkit\_package|指定打包文件。如果打包文件与pom.xml在同一个目录下，且名字为`.toolkit_package.yaml`，可不填写该参数，插件会自动获取。**说明：** 插件自动获取的`.toolkit_package.yaml`文件名最前面包含英文句号。 |
    |-Dtoolkit\_deploy|指定部署文件。如果部署文件与pom.xml在同一个目录下，且名字为`.toolkit_deploy.yaml`，可不填写该参数，插件会自动获取。**说明：** 插件自动获取的`.toolkit_deploy.yaml`文件名最前面包含英文句号。 |
    |-Ddeploy version|指定部署的版本号，优先级高于`toolkit_deploy.yaml`文件中的**Version**配置。**说明：** toolkit-maven-plugin插件1.1.2及以上版本支持该配置参数。 |

    执行该打包命令后，系统显示如下结果，当返回信息中显示`BUILD SUCCESS`表示部署成功。

    ![通过Maven上部署SAE成功打包信息](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/110639/cn_zh/1552453792195/1537957243390-51f79f1a-b03f-4d7e-b0bb-4fa242ceb003.jpeg)


## 更多配置项

-   打包参数

    打包文件支持的参数如下所示。

    ```
    apiVersion: V1
    kind: AppPackage
    spec:
      packageType:  #应用部署包类型，支持**War**、**FatJar**、**Image**、**url**。您只有在该处配置了url，那么packageUrl才能生效。
      imageUrl:     #镜像地址，**Image**包类型应用可设置。如果设置了spec.build.docker，使用本地构建的镜像部署，则不需要设置该参数。
      packageUrl:   #部署包地址，**War**、**FatJar**类型应用可填入。
      build:
        docker:
           dockerfile:        #Docker镜像构建文件。如果您希望在本地构建镜像部署，需填入此字段，例如：Dockerfile。
           imageRepoAddress:  #阿里云镜像仓库地址。如果您希望在本地构建镜像部署，需填入此字段，例如：registry.cn-beijing.aliyuncs.com/edas_demo/demo。
           imageTag:          #镜像Tag。如果您希望在本地构建镜像部署，需填入此字段，例如：test。
           imageRepoUser:     #阿里云镜像仓库用户名。如果您希望在本地构建镜像部署，需填入此字段，例如：***@***。
           imageRepoPassword: #阿里云镜像仓库密码。如果您希望在本地构建镜像部署，需填入此字段，例如：password。
        oss:
           bucket:              #目标存储桶名称。如果您希望使用自定义的OSS仓库存储部署包，需填入此字段，例如：bucket-name01。
           key:                 #OSS自定义路径。如果您希望使用自定义的OSS仓库存储部署包，需填入此字段，例如:test1/test.jpg。
           accessKeyId:         #OSS账号。如果您希望使用自定义的OSS仓库存储包，需填入此字段。
           accessKeySecret:     #OSS密码。如果您希望使用自定义的OSS仓库存储包，可填入此字段。
           useVpcEndpoint: true #是否通过内网上传文件，**true**表示通过内网上传，**false**表示不通过内网上传。
           accessTimeout:30     #部署包临时访问地址的过期时间，单位分钟，默认为30。如果您希望使用自定义的过期时间，可修改该字段。                       
    ```

-   部署参数

    部署文件支持的参数如下所示。

    ```
    apiVersion: V1
    kind: AppDeployment
    spec:
      type: serverless
      target:
        appName:     #应用名称。
        namespaceId: #应用所在命名空间。
        appId:       #应用ID。插件会使用此应用进行部署，如果未填入则使用namespaceId和appname来查找应用进行部署。
      version:     #部署版本号，默认使用日时分秒格式。
      jdk:           #部署的包依赖的JDK版本，JDK支持版本为Open JDK 7和Open JDK 8。镜像不支持。
      webContainer:  #部署的包依赖的Tomcat版本，WebContainer支持apache-tomcat-7.0.91。镜像不支持。
      batchWaitTime: #分批等待时间。
      command:       #镜像启动命令。该命令必须为容器内存在的可执行的对象。例如：sleep。设置该命令将导致镜像原本的启动命令失效。
      commandArgs:   #镜像启动命令参数。上述启动命令所需参数。
      - 1d
      updateStrategy: 
        type: GrayBatchUpdate #部署类型，**BatchUpdate**表示分批部署，**GrayBatchUpdate**表示灰度部署。
        batchUpdate: 
          batch: 2 #分批数，如果是灰度部署，表示灰度批次后的分批数。
          releaseType: manual #分批类型。**manual**表示手动分批，**auto**表示自动分批。
          batchWaitTime: 0 #分批类型为auto时使用，表示分批间间隔时间，单位为分钟。
        grayUpdate: #灰度部署时需要配置。
          gray: 1 #灰度的实例数。
      envs:    #容器环境变量参数。
        - name: envtmp0
          value: '0'
        - name: envtmp1
          value: '1'
      customHostAlias:  #容器内自定义host映射。
        - hostName: 'samplehost1'
          ip: '127.X.X.X'
        - hostName: 'samplehost2'
          ip: '127.X.X.X'
      jarStartOptions:  #JAR包启动应用选项。
      jarStartArgs:     #JAR包启动应用参数。
      liveness:   #容器健康检查，健康检查失败的容器将被重启。
        exec:
          command:
            - sleep
            - 1s
        initialDelaySeconds: 5
        timeoutSeconds: 11
      readiness:  #应用启动状态检查，多次健康检查失败的容器将被重启。不通过健康检查的容器将不会有SLB流量进入。
        exec:
          command:
            - sleep
            - 1s
        initialDelaySeconds: 5
        timeoutSeconds: 11
      minReadyInstances: 1  #最小存活实例数。在滚动升级过程中或者滚动升级失败时，可用实例数都将尽可能不小于该值，为0则没有限制。弹性扩缩容的范围不能小于该值，否则将触发异常。                       
    ```


## 更多信息

-   您在SAE部署完应用后，可以对应用进行更新、扩缩容、启停、删除应用等生命周期管理操作。具体操作，请参见[管理应用生命周期](/cn.zh-CN/应用管理/应用生命周期/管理应用生命周期.md)。
-   您在SAE部署完应用后，可以对应用进行自动弹性伸缩、SLB绑定和批量启停等提升应用性能的操作。具体操作，请参见以下文档：
    -   [绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)
    -   [配置弹性伸缩策略](/cn.zh-CN/应用管理/应用实例/配置弹性伸缩策略.md)
    -   [一键启停应用](/cn.zh-CN/应用管理/应用生命周期/一键启停应用.md)
    -   [配置管理](/cn.zh-CN/应用管理/配置管理/配置管理概述.md)
    -   [变更实例规格](/cn.zh-CN/应用管理/应用实例/变更实例规格.md)
-   您在SAE部署完应用后，还可以对应用进行日志管理、监控管理、应用事件查看和变更记录查看等聚焦应用运行状态的操作。具体操作，请参见以下文档：
    -   [日志管理](/cn.zh-CN/应用管理/日志管理/查看实时日志.md)
    -   [监控管理](/cn.zh-CN/监控管理/基础监控.md)
    -   [应用事件查看](/cn.zh-CN/应用管理/应用变更记录/查看应用事件.md)
    -   [变更记录查看](/cn.zh-CN/应用管理/应用变更记录/查看变更记录.md)
    -   [使用Webshell诊断应用](/cn.zh-CN/应用管理/使用 Webshell 诊断应用.md)

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4279867061/p72048.png)

