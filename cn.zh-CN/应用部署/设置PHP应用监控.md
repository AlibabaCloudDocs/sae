# 设置PHP应用监控

如果您想要开启PHP应用的监控功能，您需要将SAE内置的应用监控配置文件挂载到PHP的配置加载目录。

## 在应用创建过程中设置PHP应用监控

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击**创建应用**。

3.  在**应用基本信息**页签设置应用相关信息，并单击**下一步：应用部署配置**。

4.  在**应用部署配置**页签，选择**技术栈语言**和**应用部署方式**，设置部署参数。

5.  在**应用部署配置**页签，展开**PHP应用监控设置**区域，在**挂载目录**区域设置应用监控配置文件的挂载目录。

    ![设置PHP应用监控](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0236760061/p166980.png)

    **说明：** 请确保挂载的应用监控配置文件能被进程加载。

6.  单击**下一步：确认规格**。

7.  在**确认规格**页签，查看您所创建应用的详细信息以及配置费用情况，并单击**确认创建**。


## 应用部署完成后设置PHP应用监控

PHP应用监控可以在创建应用过程中设置，也可以在应用部署完成后进行配置。

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击具体应用名称。

3.  在应用详情页面的右上角，单击**部署应用**。

4.  在**部署应用**页面，展开**PHP应用监控设置**区域，在**挂载目录**区域设置应用监控配置文件的挂载目录。

    ![设置PHP应用监控](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0236760061/p166980.png)

    **说明：** 请确保挂载的应用监控配置文件能被进程加载。

5.  配置完成后单击**确认**。

    **说明：** 单击**确认**后，该应用将会被重启，请在业务较少的时间段进行。


## 结果验证

您可以通过以下方式验证PHP应用监控是否设置成功。

1.  登录[SAE控制台](https://sae.console.aliyun.com)。

2.  在左侧导航栏单击**应用列表**，在**应用列表**页面上方选择**地域**，单击具体应用名称。

3.  在应用**基本信息**页面单击**实例部署信息**，在**实例部署信息**页签，单击具体实例**操作**列的**Webshell**，在命令框中执行以下命令。

    -   执行以下命令获取ARMS信息。

        ```
        cat /usr/local/etc/php/conf.d/arms.ini #  /usr/local/etc/php/conf.d/arms.ini为配置文件挂载目录，请根据实际配置填写。
        ```

        如果返回结果如下，说明PHP应用监控设置成功。

        ```
        extension=/usr/local/arms/arms-php-agent/arms-x.x.so
        [ARMS]
        arms.enable=1
        arms.app_id=<yourAppName>
        arms.license_key=<yourLicenseKey>
        arms.network_type=tcp
        arms.tcp_host=127.0.0.0
        arms.tcp_port=11234
        ```

    -   执行以下命令查看应用是否加载监控配置文件。

        ```
        php -i | grep ini
        ```

        如果返回结果如下，说明PHP应用监控设置成功。

        ```
        Scan this dir for additional .ini files => /usr/local/etc/php/conf.d
        Additional .ini files parsed => /usr/local/etc/php/conf.d/arms.ini
        ```


## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码或搜索群号23198618，加入钉钉群与我们交流。

![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4279867061/p72048.png)

