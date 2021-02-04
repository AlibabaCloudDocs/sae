# 为Spring Boot应用设置健康检查

对于Spring Boot的应用，除了使用HTTP或TCP端口检测来进行应用健康检查之外，您也可以使用Actuator组件实现定制化健康检查。

Actuator组件是Spring Boot提供的用来对应用系统进行自省和监控的功能模块，借助于Actuator，您可以很方便地查看并统计应用系统的某些监控指标。您也可以通过Actuator组件自定义您的健康检查程序。更多信息，请参见[Spring Boot Actuator官方文档](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html)。

## 操作步骤

1.  在Maven中添加所需依赖。

    ```
    <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    ```

2.  设置application.properties配置文件，显示健康检查详细信息。

    ```
    management.endpoints.web.base-path= /  #Actuator 2.0之前默认基础访问路径是"/"（则健康检查为“/heath”）,2.0之后默认访问路径是"/actuator" （则健康检查为“/actuator/heath”）。
    management.endpoint.health.show-details=always  #显示健康检查详细信息，默认为never，即不显示。
    ```

3.  您可以通过Actuator组件提供的自动配置的健康指示器或者自定义检查程序对应用进行检查。

    -   通过自动配置的健康检查器。

        Actuator有些自动配置加载的健康检查指示器（HealthIndicator），例如若应用中使用了Redis、MongoDB，那么RedisHealthIndicator以及MongoHealthIndicator就会被作为健康检查的一部分。更多关于自动加载的配置信息，请参见[自动配置加载](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-health-indicators)。

        您也可以禁用所有自动配置的健康指示器，或者禁用某个指示器的健康检查。

        ```
        management.health.defaults.enable=false  #禁用所有默认健康检查指示器。  
        management.health.mongo.enable=false  #禁用MongoDB健康检查指示器。
        ```

        **说明：** 请您根据应用，选择需要开启的健康检查指示器。如果您开启了全部的指示器，可能会导致健康检查持续失败。

    -   通过自定义检查程序。此时您可以通过/health/custom路径来单独获取这个健康指示器的结果。

        新建CustomHealthIndicator.java文件，输入代码，实现您业务中特定的检查内容。例如检查数据库连接是否正常，线程池状态等。示例代码如下所示：

        ```
        @Component
        public class CustomHealthIndicator extends AbstractHealthIndicator {
            @Override
            protected void doHealthCheck(Health.Builder builder) throws Exception {
               # 实现您业务中特定的检查内容。
               if (checkSomething()) {  
                   builder.up().withDetail("Item", "xxx").withDetail("error", "null");
               } else {
                   builder.down().withDetail("Item", "xxx").withDetail("error", "xxxErrorCode");
                }
            }
        }
        ```

4.  设置完成后，运行应用，进行健康检查。

    -   通过直接访问默认端口进行健康检查。示例命令如下：

        ```
        curl 127.0.0.21:8080/health/custom #custom为健康检查指示器类名前缀，请以您定义的类名为准。
        ```

        **说明：**

        -   Actuator 2.0版本之前默认基础访问路径是/，则健康检查路径为/health。
        -   Actuator 2.0版本之后默认访问路径是/actuator， 则健康检查路径为/actuator/heath。
        返回示例如下：

        ```
        {"status":"UP","details":{"custom":{"status":"UP","details":{"Item","xxx","error","null"}}}}
        ```

        状态说明如下：

        -   **UP**：HTTP状态码为200，说明健康检查成功。
        -   **DOWN**：HTTP状态码为503，说明健康检查失败。
        **说明：** 如果这个检查路径中包含了多个健康指示器的结果（例如检查的路径是/health），只要有一个指示器的结果为DOWN，HTTP状态码就会是503，即健康检查失败。

    -   在[SAE控制台](https://sae.console.aliyun.com)配置健康检查。具体步骤，请参见[设置健康检查](/cn.zh-CN/应用部署/设置健康检查.md)。

        ![健康检查最佳实践](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0993442161/p235846.png)


