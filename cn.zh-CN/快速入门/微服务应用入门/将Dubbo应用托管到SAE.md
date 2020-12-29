# 将Dubbo应用托管到SAE

本文以包含服务提供者Provider和服务消费者Consumer的Dubbo微服务应用为例，介绍如何在本地通过XML配置的方式，开发Dubbo微服务示例应用，并部署到SAE。

## 为什么托管到SAE

将Dubbo应用托管到SAE，您仅需关注Dubbo应用自身的逻辑，无需再关注注册中心和配置中心搭建和维护，托管后还可以使用SAE提供的弹性伸缩、一键启停、监控等功能，大大降低开发和运维成本。

**说明：** 如果您坚持使用自建Nacos为服务注册中心，Nacos注册中心的搭建步骤，请参见[如何搭建Nacos为服务注册中心（不推荐）](https://help.aliyun.com/document_detail/142100.html)。

## 准备工作

在开始开发前，请确保您已经完成以下工作：

-   下载[Maven](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/App-develop/apache-maven-3.6.0-bin.tar.gz)并设置环境变量。
-   下载最新版本的[Nacos Server](https://github.com/alibaba/nacos/releases)。
-   按以下步骤启动Nacos Server。
    1.  解压下载的Nacos Server压缩包
    2.  进入`nacos/bin`目录，启动Nacos Server。
        -   Linux/Unix/Mac系统：执行命令`sh startup.sh -m standalone`。
        -   Windows系统：双击执行`startup.cmd`文件。

## 创建服务提供者

在本地创建一个提供者应用工程，添加依赖，配置服务注册与发现，并将注册中心指定为Nacos。

1.  创建Maven项目并引入依赖。

    1.  使用IDE（如IntelliJ IDEA或Eclipse）创建一个Maven项目。

    2.  在`pom.xml`文件中添加dubbo、dubbo-registry-nacos和nacos-client依赖。

        ```
        <dependencies>
        
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo</artifactId>
                <version>2.7.3</version>
            </dependency>
        
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-registry-nacos</artifactId>
                <version>2.7.3</version>
            </dependency>
        
            <dependency>
                <groupId>com.alibaba.nacos</groupId>
                <artifactId>nacos-client</artifactId>
                <version>1.1.1</version>
            </dependency>
        </dependencies>            
        ```

2.  开发Dubbo服务提供者。

    Dubbo中服务都是以接口的形式提供的。

    1.  在`src/main/java`路径下创建一个package`com.alibaba.edas`。

    2.  在`com.alibaba.edas`下创建一个接口（interface）`IHelloService`，里面包含一个`SayHello`方法。

        ```
          package com.alibaba.edas;
        
          public interface IHelloService {
              String sayHello(String str);
          }                                
        ```

    3.  在`com.alibaba.edas`下创建一个类`IHelloServiceImpl`，实现此接口。

        ```
          package com.alibaba.edas;
        
          public class IHelloServiceImpl implements IHelloService {
              public String sayHello(String str) {
                  return "hello " + str;
              }
          }                          
        ```

3.  配置Dubbo服务。

    1.  在`src/main/resources`路径下创建`provider.xml`文件并打开。

    2.  在`provider.xml`中，添加Spring相关的XML Namespace（xmlns）和XML Schema Instance（xmlns:xsi），以及Dubbo相关的Namespace（xmlns:dubbo）和Scheme Instance（xsi:schemaLocation）。

        ```
        <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
        xmlns="http://www.springframework.org/schema/beans"
        xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
        http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
                                        
        ```

    3.  在`provider.xml`中将接口和实现类暴露成Dubbo服务。

        ```
          <dubbo:application name="demo-provider"/>
        
          <dubbo:protocol name="dubbo" port="28082"/>
        
          <dubbo:service interface="com.alibaba.edas.IHelloService" ref="helloService"/>
        
          <bean id="helloService" class="com.alibaba.edas.IHelloServiceImpl"/>                                
        ```

    4.  在`provider.xml`中将注册中心指定为本地启动的Nacos Server。

        ```
        <dubbo:registry address="nacos://127.0.0.1:8848" />                                
        ```

        -   `127.0.0.1`为Nacos Server的地址。如果您的Nacos Server部署在另外一台机器，则需要修改成对应的IP地址。当将应用部署到SAE后，无需做任何修改，注册中心会替换成SAE上的注册中心的地址。
        -   `8848`为Nacos Server的端口号，不可修改。
4.  启动服务。

    1.  在`com.alibaba.edas`中创建类Provider，并按下面的代码在Provider的main函数中加载Spring Context，将配置好的Dubbo服务暴露。

        ```
        package com.alibaba.edas;
        
        import org.springframework.context.support.ClassPathXmlApplicationContext;
        
        public class Provider {
            public static void main(String[] args) throws Exception {
                ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[] {"provider.xml"});
                context.start();
                System.in.read();
            }
        }                
        ```

    2.  执行Provider的main函数，启动服务。

5.  登录Nacos控制台`http://127.0.0.1:8848`，在左侧导航栏中单击**服务列表**，查看提供者列表。可以看到服务提供者里已经包含了`com.alibaba.edas.IHelloService`，且可以查询该服务的**服务分组**和**提供者IP**。


## 创建服务消费者

在本地创建一个消费者应用工程，添加依赖，添加订阅服务的配置。

1.  创建Maven项目并引入依赖。

    1.  使用IDE（如IntelliJ IDEA或Eclipse）创建一个Maven项目。

    2.  在`pom.xml`文件中添加dubbo、dubbo-registry-nacos和nacos-client依赖。

        ```
        <dependencies>
        
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo</artifactId>
                <version>2.7.3</version>
            </dependency>
        
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-registry-nacos</artifactId>
                <version>2.7.3</version>
            </dependency>
        
            <dependency>
                <groupId>com.alibaba.nacos</groupId>
                <artifactId>nacos-client</artifactId>
                <version>1.1.1</version>
            </dependency>
        </dependencies>            
        ```

2.  开发Dubbo服务提供者。

    Dubbo中服务都是以接口的形式提供的。

    1.  在`src/main/java`路径下创建Package，命名为`com.alibaba.edas`。

    2.  在`com.alibaba.edas`下创建一个接口（interface）`IHelloService`，里面包含一个`SayHello`方法。

        **说明：** 通常是在一个单独的模块中定义接口，服务提供者和服务消费者都通过Maven依赖来引用此模块。本文档为了简便，服务提供者和服务消费者分别创建两个完全一模一样的接口，实际使用中不推荐这样使用。

        ```
          package com.alibaba.edas;
        
          public interface IHelloService {
              String sayHello(String str);
          }                                
        ```

3.  配置Dubbo服务。

    1.  在`src/main/resources`路径下创建`consumer.xml`文件并打开。

    2.  在`consumer.xml`中，添加Spring相关的XML Namespace（xmlns）和XML Schema Instance（xmlns:xsi），以及Dubbo相关的Namespace（xmlns:dubbo）和Scheme Instance（xsi:schemaLocation）。

        ```
        <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
        xmlns="http://www.springframework.org/schema/beans"
        xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
        http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">                              
        ```

    3.  在`consumer.xml`中添加如下配置，订阅Dubbo服务。

        ```
          <dubbo:application name="demo-consumer"/>
        
          <dubbo:registry address="nacos://127.0.0.1:8848"/>
        
          <dubbo:reference id="helloService" interface="com.alibaba.edas.IHelloService"/>
        ```

4.  启动、验证服务。

    1.  在`com.alibaba.edas`下创建类Consumer，并按下面的代码在Consumer的main函数中加载Spring Context，订阅并消费Dubbo服务。

        ```
            package com.alibaba.edas;
        
            import org.springframework.context.support.ClassPathXmlApplicationContext;
        
            import java.util.concurrent.TimeUnit;
        
            public class Consumer {
                public static void main(String[] args) throws Exception {
                    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[] {"consumer.xml"});
                    context.start();
                    while (true) {
                        try {
                            TimeUnit.SECONDS.sleep(5);
                            IHelloService demoService = (IHelloService)context.getBean("helloService");
                            String result = demoService.sayHello("world");
                            System.out.println(result);
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                }
            }               
        ```

    2.  执行Consumer的main函数，启动服务。

5.  验证创建结果。

    启动后，可以看到控制台不断地输出`hello world`，表明服务消费成功。

    登录Nacos控制台`http://127.0.0.1:8848`，在左侧导航栏中单击**服务列表**，再在**服务列表**页面选择**调用者列表**。

    可以看到包含了`com.alibaba.edas.IHelloService`，且可以查看该服务的**服务分组**和**调用者IP**。


## 部署到SAE

1.  在pom.xml文件中添加应用编译配置，并执行mvn clean package将本地的程序打成可执行的JAR包。

    -   Provider

        ```
        <build>
         <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
                   <executions>
                       <execution>
                           <goals>
                               <goal>repackage</goal>
                           </goals>
                           <configuration>
                               <classifier>spring-boot</classifier>
                               <mainClass>com.alibaba.edas.Provider</mainClass>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
         </plugins>
        </build>
                                        
        ```

    -   Consumer

        ```
        <build>
         <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
                   <executions>
                       <execution>
                           <goals>
                               <goal>repackage</goal>
                           </goals>
                           <configuration>
                               <classifier>spring-boot</classifier>
                               <mainClass>com.alibaba.edas.Consumer</mainClass>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
         </plugins>
        </build>
                                        
        ```

2.  将编译好的Provider和Consumer应用包部署至SAE。具体操作，请参见[部署微服务应用到SAE](https://help.aliyun.com/document_detail/97761.html)。

    **说明：**

    -   使用自建Nacos时请确保SAE的网络与自建Nacos的网络互通。
    -   使用自建Nacos为服务注册中心，在部署应用时建议使用镜像方式或者JAR包方式，并配置启动参数`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`。
        -   如采用镜像方式，请将`-Dnacos.use.endpoint.parsing.rule=false`和`-Dnacos.use.cloud.namespace.parsing=false`配置在镜像文件中。关于Docker镜像制作方法，请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。
        -   如采用JAR包方式，请在控制台**启动命令设置**区域的**options设置**文本框输入`-Dnacos.use.endpoint.parsing.rule=false -Dnacos.use.cloud.namespace.parsing=false`。

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

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![问题反馈](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

