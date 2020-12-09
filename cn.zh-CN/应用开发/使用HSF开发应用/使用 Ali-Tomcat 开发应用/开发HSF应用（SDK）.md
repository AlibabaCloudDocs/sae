# 开发HSF应用（SDK）

介绍如何使用SDK快速开发HSF应用，完成服务注册与发现。

在开发应用前，您已经完成以下工作：

-   [配置SAE的私服地址和轻量级配置及注册中心]()
-   [启动轻量级配置及注册中心]()

## 下载Demo工程

您可以按照本文的步骤一步步搭建工程，也可以直接下载本文对应的[示例工程](https://github.com/aliyun/alibabacloud-microservice-demo/archive/master.zip)，或者使用Git下载：git clone https://github.com/aliyun/alibabacloud-microservice-demo.git。

该项目包含了众多示例工程，本文对应的示例工程位于alibabacloud-microservice-demo/microservice-doc-demo/hsf-ali-tomcat，包含itemcenter-api，itemcenter和detail三个Maven工程文件夹。

-   itemcenter-api：提供接口定义
-   itemcenter：服务提供者
-   detail：消费者服务

**说明：** 请使用JDK 1.7及以上版本。

## 定义服务接口

HSF服务基于接口实现，当接口定义好之后，生产者将使用该接口实现具体的服务，消费者也基于此接口去订阅服务。

在Demo的itemcenter-api工程中，定义了一个服务接口`com.alibaba.edas.carshop.itemcenter.ItemService`。

```
public interface ItemService {
    public Item getItemById(long id);
    public Item getItemByName(String name);
}
```

该服务接口将提供两个方法：getItemById与getItemByName。

## 开发服务提供者

服务提供者将实现服务接口以提供具体服务。同时，如果使用了Spring框架，还需要在xml文件中配置服务属性。

**说明：** Demo工程中的itemcenter文件夹为服务提供者的示例代码。

1.  实现服务接口。

    请参考ItemServiceImpl.java文件中的示例代码构建服务接口。

    ```
    public class ItemServiceImpl implements ItemService {
    
        @Override
        public Item getItemById( long id ) {
            Item car = new Item();
            car.setItemId( 1l );
            car.setItemName( "Mercedes Benz" );
            return car;
        }
        @Override
        public Item getItemByName( String name ) {
            Item car = new Item();
            car.setItemId( 1l );
            car.setItemName( "Mercedes Benz" );
            return car;
        }
    }
    ```

2.  服务提供者配置。

    [实现服务接口](#step_0tx_pi0_9s4)中实现了com.alibaba.edas.carshop.itemcenter.ItemService，并在两个方法中返回了Item对象。代码开发完成之后，除了在web.xml中进行必要的常规配置，您还需要增加相应的Maven依赖，同时在Spring配置文件使用`<hsf />`标签注册并发布该服务。

    1.  在pom.xml中添加Maven依赖。

        ```
          <dependencies>
              <!-- 添加servlet的依赖 -->
              <dependency>
                  <groupId>javax.servlet</groupId>
                  <artifactId>servlet-api</artifactId>
                  <version>2.5</version>
                  <scope>provided</scope>
              </dependency>
              <!-- 添加服务接口的依赖 -->      
              <dependency>
                  <groupId>com.alibaba.edas.carshop</groupId>
                  <artifactId>itemcenter-api</artifactId>
                  <version>1.0.0-SNAPSHOT</version>
              </dependency>
              <!-- 添加Spring的依赖 -->
              <dependency>
                  <groupId>org.springframework</groupId>
                  <artifactId>spring-web</artifactId>
                  <version>2.5.6(及其以上版本)</version>
              </dependency>
              <!-- 添加edas-sdk的依赖 -->
              <dependency>
                    <groupId>com.alibaba.edas</groupId>
                     <artifactId>edas-sdk</artifactId>
                    <version>1.8.1</version>
              </dependency>
          </dependencies>
        ```

    2.  在hsf-provider-beans.xml文件中增加Spring关于HSF服务的配置。

        ```
          <?xml version="1.0" encoding="UTF-8"?>
          <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xmlns:hsf="http://www.taobao.com/hsf"
              xmlns="http://www.springframework.org/schema/beans"
              xsi:schemaLocation="http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
              http://www.taobao.com/hsf
              http://www.taobao.com/hsf/hsf.xsd" default-autowire="byName">
              <!-- 定义该服务的具体实现 -->
              <bean id="itemService" class="com.alibaba.edas.carshop.itemcenter.ItemServiceImpl" />
              <!-- 用hsf:provider标签表明提供一个服务生产者 -->
              <hsf:provider id=“itemServiceProvider"
                  <!-- 用interface属性说明该服务为此类的一个实现 -->
                  interface=“com.alibaba.edas.carshop.itemcenter.ItemService"
                  <!-- 此服务具体实现的Spring对象 -->
                  ref=“itemService"
                  <!-- 发布该服务的版本号，可任意指定，默认为1.0.0 -->
                  version=“1.0.0"
              </hsf:provider>
          </beans>
        ```

        上面的示例为基本配置，您也可以根据您的实际需求，参考下面的生产者服务属性列表，增加其它配置。

        |属性|描述|
        |--|--|
        |interface|必须配置，类型为 \[String\]，为服务对外提供的接口。|
        |version|可选配置，类型为 \[String\]，含义为服务的版本，默认为1.0.0。|
        |clientTimeout|该配置对接口中的所有方法生效，但是如果客户端通过methodSpecials属性对某方法配置了超时时间，则该方法的超时时间以客户端配置为准。其他方法不受影响，还是以服务端配置为准。|
        |serializeType|可选配置，类型为`[String(hessian｜java)]`，含义为序列化类型，默认为hessian。|
        |corePoolSize|单独针对这个服务设置核心线程池，从公用线程池中划分出来。|
        |maxPoolSize|单独针对这个服务设置线程池，从公用线程池中划分出来。|
        |enableTXC|开启分布式事务GTS。|
        |ref|必须配置，类型为 \[ref\]，为需要发布为HSF服务的Spring Bean ID。|
        |methodSpecials|可选配置，用于为方法单独配置超时时间（单位ms），这样接口中的方法可以采用不同的超时时间。该配置优先级高于上面的clientTimeout的超时配置，低于客户端的methodSpecials配置。|

        服务创建及发布存在以下限制：

        |名称|示例|限制大小|是否可调整|
        |--|--|----|-----|
        |\{服务名\}:\{版本号\}|com.alibaba.edas.testcase.api.TestCase:1.0.0|最大192字节|否|
        |组名|HSF|最大32字节|否|
        |单个Pandora应用实例发布的服务数|N/A|最大800个|可在应用基本信息页面单击**应用设置**部分右侧的设置，在下拉列表中选择**JVM**，在弹出的**应用设置**对话框中进入**自定义** \> **自定义参数**，`-DCC.pubCountMax=1200`属性参数（该参数值可根据应用实际发布的服务数调整）。|

        服务提供者属性配置示例：

        ```
        <bean id="impl" class="com.taobao.edas.service.impl.SimpleServiceImpl" />
        <hsf:provider
                id="simpleService"
                interface="com.taobao.edas.service.SimpleService"
                ref="impl"
                version="1.0.1"
                clientTimeout="3000"
                enableTXC="true"
                serializeType="hessian">
                <hsf:methodSpecials>
                    <hsf:methodSpecial name="sum" timeout="2000" />
                </hsf:methodSpecials>
        </hsf:provider>
        ```


## 开发服务消费者

消费者订阅服务从代码编写的角度分为两个部分。

-   Spring的配置文件使用标签`<hsf:consumer/>`定义好一个Bean。
-   在使用的时候从Spring的context中将Bean取出来。

**说明：** Demo工程中的detail文件夹为消费者服务的示例代码。

1.  与生产者相同，消费者的服务属性配置分为Maven依赖配置与Spring的配置。
2.  配置服务属性。

    1.  在pom.xml文件中添加Maven依赖。

        ```
          <dependencies>
              <!-- 添加 servlet 的依赖 -->
              <dependency>
                  <groupId>javax.servlet</groupId>
                  <artifactId>servlet-api</artifactId>
                  <version>2.5</version>
                  <scope>provided</scope>
              </dependency>
              <!-- 添加 Spring 的依赖 -->
              <dependency>
                  <groupId>com.alibaba.edas.carshop</groupId>
                  <artifactId>itemcenter-api</artifactId>
                  <version>1.0.0-SNAPSHOT</version>
              </dependency>
              <!-- 添加服务接口的依赖 -->
              <dependency>
                  <groupId>org.springframework</groupId>
                  <artifactId>spring-web</artifactId>
                  <version>2.5.6(及其以上版本)</version>
              </dependency>
              <!-- 添加 edas-sdk 的依赖 -->
              <dependency>
                    <groupId>com.alibaba.edas</groupId>
                     <artifactId>edas-sdk</artifactId>
                    <version>1.8.1</version>
              </dependency>
          </dependencies>
        ```

    2.  在hsf-consumer-beans.xml文件中添加Spring关于HSF服务的配置。

        增加消费者的定义，HSF框架将根据该配置文件去服务中心订阅所需的服务。

        ```
        <?xml version="1.0" encoding="UTF-8"?>
        <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xmlns:hsf="http://www.taobao.com/hsf"
                xmlns="http://www.springframework.org/schema/beans"
                xsi:schemaLocation="http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
                http://www.taobao.com/hsf
                http://www.taobao.com/hsf/hsf.xsd" default-autowire="byName">
                <!-- 消费一个服务示例 -->
                <hsf:consumer
                    <!-- Bean ID，在代码中可根据此ID进行注入从而获取consumer对象  -->
                    id="item"
                    <!-- 服务名，与服务提供者的相应配置对应，HSF将根据interface + version查询并订阅所需服务  -->
                    interface="com.alibaba.edas.carshop.itemcenter.ItemService"
                    <!-- 版本号，与服务提供者的相应配置对应，HSF将根据interface + version查询并订阅所需服务  -->
                    version="1.0.0">
                </hsf:consumer>
        </beans>
        ```

3.  服务消费者配置。

    请参考StartListener.java文件中的示例进行。

    ```
    public class StartListener implements ServletContextListener{
    
        @Override
        public void contextInitialized( ServletContextEvent sce ) {
            ApplicationContext ctx = WebApplicationContextUtils.getWebApplicationContext( sce.getServletContext() );
            // 根据Spring配置中的Bean ID“item” 获取订阅到的服务final ItemService itemService = ( ItemService ) ctx.getBean( "item" );
            ……
            // 调用服务ItemService的getItemById方法System.out.println( itemService.getItemById( 1111 ) );
            // 调用服务ItemService的getItemByName方法System.out.println( itemService.getItemByName( "myname is le" ) );
            ……
        }
    }
    ```

    上面的示例中为基本配置，您也可以根据您的实际需求，参考下面的服务属性列表，增加其它配置。

    |属性|描述|
    |--|--|
    |interface|必须配置，类型为 \[String\]，为需要调用的服务的接口。|
    |version|可选配置，类型为 \[String\]，为需要调用的服务的版本，默认为1.0.0。|
    |methodSpecials|可选配置，为方法单独配置超时时间（单位ms）。这样接口中的方法可以采用不同的超时时间，该配置优先级高于服务端的超时配置。|
    |target|主要用于单元测试环境和开发环境中，手动地指定服务提供端的地址。如果不想通过此方式，而是通过配置中心推送的目标服务地址信息来指定服务端地址，可以在消费者端指定 -Dhsf.run.mode=0。|
    |connectionNum|可选配置，为支持设置连接到server连接数，默认为1。在小数据传输，要求低延迟的情况下设置多一些，会提升TPS。|
    |clientTimeout|客户端统一设置接口中所有方法的超时时间（单位ms）。超时时间设置优先级由高到低是：客户端methodSpecials，客户端接口级别，服务端methodSpecials，服务端接口级别 。|
    |asyncallMethods|可选配置，类型为 \[List\]，设置调用此服务时需要采用异步调用的方法名列表以及异步调用的方式。默认为空集合，即所有方法都采用同步调用。|
    |maxWaitTimeForCsAddress|配置该参数，目的是当服务进行订阅时，会在该参数指定时间内，阻塞线程等待地址推送，避免调用该服务时因为地址为空而出现地址找不到的情况。若超过该参数指定时间，地址还是没有推送，线程将不再等待，继续初始化后续内容。注意，在应用初始化时，需要调用某个服务时才使用该参数。如果不需要调用其它服务，请勿使用该参数，会延长启动时间。|

    消费者服务属性配置示例

    ```
    <hsf:consumer
          id="service"
          interface="com.taobao.edas.service.SimpleService"
          version="1.1.0"
          clientTimeout="3000"
          target="10.1.6.57:12200?_TIMEOUT=1000"
          maxWaitTimeForCsAddress="5000">
          <hsf:methodSpecials>
               <hsf:methodSpecial name="sum" timeout="2000" ></hsf:methodSpecial>
          </hsf:methodSpecials>
    </hsf:consumer>
    ```


## 本地运行服务

完成代码、接口开发和服务配置后，在Eclipse或IDEA中，可直接以Ali-Tomcat运行该服务（具体请参见[安装及开发环境配置]()）。

在开发环境配置时，有一些额外JVM启动参数来改变HSF的行为，具体如下：

|属性|描述|
|--|--|
|-Dhsf.server.port|指定HSF的启动服务绑定端口，默认值为12200。|
|-Dhsf.serializer|指定HSF的序列化方式，默认值为hessian。|
|-Dhsf.server.max.poolsize|指定HSF的服务端最大线程池大小，默认值为720。|
|-Dhsf.server.min.poolsize|指定HSF的服务端最小线程池大小。默认值为50。|
|-DHSF\_SERVER\_PUB\_HOST|指定对外暴露的IP，如果不配置，使用 -Dhsf.server.ip的值。|
|-DHSF\_SERVER\_PUB\_PORT|指定对外暴露的端口，该端口必须在本机被监听，并对外开放了访问授权，默认使用 -Dhsf.server.port的配置，如果 -Dhsf.server.port没有配置，默认使用12200。|

## 本地查询HSF服务

在开发调试的过程中，如果您的服务是通过轻量级注册配置中心进行服务注册与发现，就可以通过EDAS控制台查询某个应用提供或调用的服务。

假设您在一台IP为192.168.1.100的机器上启动了EDAS配置中心。

-   进入[http://192.168.1.100:8080/](http://192.168.1.100:8080/)
-   在左侧菜单栏单击**服务列表**，输入服务名、服务组名或者IP地址进行搜索，查看对应的服务提供者以及服务调用者。

    **说明：** 配置中心启动之后默认选择第一块网卡地址做为服务发现的地址，如果开发者所在的机器有多块网卡的情况，可设置启动脚本中的SERVER\_IP变量进行显式的地址绑定。


常见查询案例

-   提供者列表页
    -   在搜索框中输入IP地址，单击**搜索**，即可查询该IP地址的物理机所提供的服务。
    -   在搜索框中输入服务名或服务分组，即可查询提供该服务的IP地址。
-   调用者列表页
    -   在搜索框中输入IP地址，单击**搜索**，即可查询该IP地址的物理机所调用的服务。
    -   在搜索框中输入服务名或服务分组，即可查询调用该服务的IP地址。

## 部署到SAE

本地使用轻量级配置及注册中心的应用可以直接部署到SAE中，无需做任何修改，注册中心会被自动替换为SAE上的注册中心。

正常打包出可供EDAS-Container运行的WAR包，需要添加如下的Maven打包插件

1.  在pom.xml文件中添加以下打包插件的配置。

    ```
       <build>
           <finalName>itemcenter</finalName>
           <plugins>
               <plugin>
                   <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-compiler-plugin</artifactId>
                   <version>3.1</version>
               </plugin>
           </plugins>
       </build>
    ```

2.  执行mvn clean package将本地的程序打成WAR包。


应用运行时环境需要选择EDAS-Container。

具体部署操作请参见[应用部署概述](https://help.aliyun.com/document_detail/113181.htm)。

