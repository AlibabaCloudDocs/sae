# 开发HSF应用（Pandora Boot）

您可以使用Pandora Boot开发HSF应用，实现服务注册发现、异步调用，并完成单元测试。相比使用ali-tomcat部署HSF的WAR包，Pandora Boot部署的是JAR包。直接将HSF应用打包成FatJar，这更加符合微服务的风格，不需要依赖外置的ali-tomcat也使得应用的部署更加灵活。Pandora Boot可以认为是Spring Boot的增强。

在开发应用前，您已经完成以下工作：

-   [配置SAE的私服地址和轻量级配置及注册中心]()
-   [启动轻量级配置及注册中心]()

## 服务注册与发现

下面将介绍如何使用Pandora Boot开发应用（包括服务提供者和服务消费者）并实现服务注册与发现。

**说明：** 严禁在应用启动时调用HSF远程服务，否则会导致启动失败。

下载[Demo源码](https://github.com/aliyun/alibabacloud-microservice-demo/tree/master/microservice-doc-demo/hsf-pandora-boot)。

使用Git克隆整个项目，并在microservice-doc-demo/hsf-pandora-boot文件夹内可以找到本文使用的示例工程。

1.  创建服务提供者。

    1.  创建命名为hsf-pandora-boot-provider的Maven工程。

    2.  在pom.xml中引入需要的依赖。

        ```
        <properties>
              <java.version>1.8</java.version>
              <spring-boot.version>2.1.6.RELEASE</spring-boot.version>
              <pandora-boot.version>2019-06-stable</pandora-boot.version>
          </properties>
        
          <dependencies>
              <dependency>
                  <groupId>com.alibaba.boot</groupId>
                  <artifactId>pandora-hsf-spring-boot-starter</artifactId>
              </dependency>
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
              </dependency>
          </dependencies>
        
          <dependencyManagement>
              <dependencies>
                  <dependency>
                      <groupId>org.springframework.boot</groupId>
                      <artifactId>spring-boot-dependencies</artifactId>
                      <version>${spring-boot.version}</version>
                      <type>pom</type>
                      <scope>import</scope>
                  </dependency>
                  <dependency>
                      <groupId>com.taobao.pandora</groupId>
                      <artifactId>pandora-boot-starter-bom</artifactId>
                      <version>${pandora-boot.version}</version>
                      <type>pom</type>
                      <scope>import</scope>
                  </dependency>
              </dependencies>
          </dependencyManagement>
        
          <build>
              <plugins>
                  <plugin>
                      <groupId>org.apache.maven.plugins</groupId>
                      <artifactId>maven-compiler-plugin</artifactId>
                      <version>3.7.0</version>
                      <configuration>
                          <source>1.8</source>
                          <target>1.8</target>
                      </configuration>
                  </plugin>
                  <plugin>
                      <groupId>com.taobao.pandora</groupId>
                      <artifactId>pandora-boot-maven-plugin</artifactId>
                      <version>2.1.11.8</version>
                      <executions>
                          <execution>
                              <phase>package</phase>
                              <goals>
                                  <goal>repackage</goal>
                              </goals>
                          </execution>
                      </executions>
                  </plugin>
              </plugins>
          </build>
        ```

        虽然HSF服务框架并不依赖于Web环境，但是在应用的生命周期过程中需要使用到Web相关的特性，所以需要添加`spring-boot-starter-web`的依赖。

        `pandora-hsf-spring-boot-starter`实现了HSF配置的自动装配。`pandora-boot-maven-plugin`是Pandora Boot提供的Maven打包插件，可以将Pandora Boot HSF工程编译为可执行的FatJar，并在EDAS Container中部署运行。

        `dependencyManagement`中包含了`spring-boot-dependencies`和`pandora-boot-starter-bom`两个依赖，分别负责Spring Boot和Pandora Boot相关依赖的版本管理，设置之后，您的工程无需将parent设置为`spring-boot-starter-parent`。

    3.  定义服务接口，创建一个接口类`com.alibaba.edas.HelloService`。

        HSF服务框架基于接口进行服务通信，当接口定义好之后，生产者将通过该接口实现具体的服务并发布，消费者也是基于此接口去订阅和消费服务。

        ```
          public interface HelloService {
              String echo(String string);
          }
        ```

        接口com.alibaba.edas.HelloService提供了echo方法。

    4.  添加服务提供者的具体实现类EchoServiceImpl，并通过注解方式发布服务。

        ```
          @HSFProvider(serviceInterface = HelloService.class, serviceVersion = "1.0.0")
          public class HelloServiceImpl implements HelloService {
              @Override
              public String echo(String string) {
                  return string;
              }
          }
        ```

        在HSF应用中，接口名和服务版本才能唯一确定一个服务，所以在注解HSFProvider中的需要添加接口名com.alibaba.edas.HelloService和服务版本`1.0.0`。

        **说明：**

        -   注解中的配置拥有高优先级。
        -   如果在注解中没有配置，服务发布时会优先在resources/application.properties文件中查找这些属性的全局配置。
        -   如果注解和resources/application.properties文件中都没有配置，则会使用注解中的默认值。
    5.  在resources目录下的application.properties文件中配置应用名和监听端口号。

        ```
          spring.application.name=hsf-pandora-boot-provider
          server.port=8081
        
          spring.hsf.version=1.0.0
          spring.hsf.timeout=3000
        ```

        **说明：** 建议将服务版本（`spring.hsf.version`）和服务超时（`spring.hsf.timeout`）都统一配置在application.properties中。

    6.  添加服务启动的main函数入口。

        ```
         @SpringBootApplication
          public class HSFProviderApplication {
        
              public static void main(String[] args) {
                  // 启动Pandora Boot用于加载Pandora容器。PandoraBootstrap.run(args);
                  SpringApplication.run(HSFProviderApplication.class, args);
                  // 标记服务启动完成，并设置线程wait。防止业务代码运行完毕退出后，导致容器退出。PandoraBootstrap.markStartupAndWait();
              }
          }
        ```

        |属性|是否必配|描述|类型|默认值|
        |--|----|--|--|---|
        |serviceInterface|是|服务对外提供的接口|Class|java.lang.Object|
        |serviceVersion|否|服务的版本号|String|1.0.0.DAILY|
        |serviceGroup|否|服务的组名|String|HSF|
        |clientTimeout|否|该配置对接口中的所有方法生效，但是如果客户端通过methodSpecials属性对某方法配置了超时时间，则该方法的超时时间以客户端配置为准。其他方法不受影响，还是以服务端配置为准（单位ms）|int|-1|
        |corePoolSize|否|单独针对这个服务设置最小活跃线程数，从公用线程池中划分出来|int|0|
        |maxPoolSize|否|单独针对这个服务设置最大活跃线程数，从公用线程池中划分出来|int|0|
        |delayedPublish|否|是否延迟发布|boolean|false|
        |includeFilters|否|用户可选的自定义过滤器|String\[\]|空|
        |enableTXC|否|是否开启分布式事务GTS|boolean|false|
        |serializeType|否|服务接口序列化类型，hessian或者java|String|hessian|
        |supportAsynCall|否|是否支持异步调用|String|false|

        |名称|示例|限制大小|是否可调整|
        |--|--|----|-----|
        |\{服务名\}:\{版本号\}|com.alibaba.edas.testcase.api.TestCase:1.0.0|最大192字节|否|
        |组名|aliware|最大32字节|否|
        |一个Pandora应用实例发布的服务数|N/A|最大800个|是，可在左侧导航栏单击**基本信息**在**基本信息**页签内的**应用设置**区域内，单击**JMV参数**右侧的**编辑**，然后在弹出的**应用设置**对话框中选择**自定义** \> **自定义参数**，在输入框中添加`-DCC.pubCountMax=1200`属性参数（该参数值可根据应用实际发布的服务数调整）|

2.  创建服务消费者。

    本示例中，将创建一个服务消费者，通过HSFConsumer所提供的API接口去调用服务提供者。

    1.  创建一个Maven工程，命名为hsf-pandora-boot-consumer。

    2.  在pom.xml中引入需要的依赖内容。

        **说明：** 消费者和提供者的Maven依赖相同。

        ```
          <properties>
              <java.version>1.8</java.version>
              <spring-boot.version>2.1.6.RELEASE</spring-boot.version>
              <pandora-boot.version>2019-06-stable</pandora-boot.version>
          </properties>
        
          <dependencies>
              <dependency>
                  <groupId>com.alibaba.boot</groupId>
                  <artifactId>pandora-hsf-spring-boot-starter</artifactId>
              </dependency>
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
              </dependency>
          </dependencies>
        
          <dependencyManagement>
              <dependencies>
                  <dependency>
                      <groupId>org.springframework.boot</groupId>
                      <artifactId>spring-boot-dependencies</artifactId>
                      <version>${spring-boot.version}</version>
                      <type>pom</type>
                      <scope>import</scope>
                  </dependency>
                  <dependency>
                      <groupId>com.taobao.pandora</groupId>
                      <artifactId>pandora-boot-starter-bom</artifactId>
                      <version>${pandora-boot.version}</version>
                      <type>pom</type>
                      <scope>import</scope>
                  </dependency>
              </dependencies>
          </dependencyManagement>
        
          <build>
              <plugins>
                  <plugin>
                      <groupId>org.apache.maven.plugins</groupId>
                      <artifactId>maven-compiler-plugin</artifactId>
                      <version>3.7.0</version>
                      <configuration>
                          <source>1.8</source>
                          <target>1.8</target>
                      </configuration>
                  </plugin>
                  <plugin>
                      <groupId>com.taobao.pandora</groupId>
                      <artifactId>pandora-boot-maven-plugin</artifactId>
                      <version>2.1.11.8</version>
                      <executions>
                          <execution>
                              <phase>package</phase>
                              <goals>
                                  <goal>repackage</goal>
                              </goals>
                          </execution>
                      </executions>
                  </plugin>
              </plugins>
          </build>
        ```

    3.  将服务提供者所发布的API服务接口（包括包名）拷贝到本地，如com.alibaba.edas.HelloService。

        ```
          public interface HelloService {
              String echo(String string);
          }
        ```

    4.  通过注解的方式将服务消费者的实例注入到Spring的Context中。

        ```
         @Configuration
          public class HsfConfig {
        
              @HSFConsumer(clientTimeout = 3000, serviceVersion = "1.0.0")
              private HelloService helloService;
        
          }
        ```

        **说明：** 在`HsfConfig`类里配置一次`@HSFConsumer`，然后在多处通过`@Autowired`注入使用。通常一个`@HSFConsumer`需要在多个地方使用，但并不需要在每次使用的地方都用`@HSFConsumer`来标记。只需要写一个统一的`HsfConfig`类，然后在其它需要使用的地方，直接通过`@Autowired`注入即可。

    5.  为了便于测试，使用SimpleController来暴露一个/hsf-echo/\*的HTTP接口，/hsf-echo/\*接口内部实现调用了HSF服务提供者。

        ```
          @RestController
          public class SimpleController {
        
              @Autowired
              private HelloService helloService;
        
              @RequestMapping(value = "/hsf-echo/{str}", method = RequestMethod.GET)
              public String echo(@PathVariable String str) {
                  return helloService.echo(str);
              }
          }
        ```

    6.  在resources目录下的application.properties文件中配置应用名与监听端口号。

        ```
          spring.application.name=hsf-pandora-boot-consumer
          server.port=8080
        
          spring.hsf.version=1.0.0
          spring.hsf.timeout=1000
        ```

        **说明：** 建议将服务版本和服务超时都统一配置在application.properties中。

    7.  添加服务启动的main函数入口。

        ```
          @SpringBootApplication
          public class HSFConsumerApplication {
        
              public static void main(String[] args) {
                  PandoraBootstrap.run(args);
                  SpringApplication.run(HSFConsumerApplication.class, args);
                  PandoraBootstrap.markStartupAndWait();
              }
          }
        ```

        |属性|是否必配|描述|类型|默认值|
        |--|----|--|--|---|
        |serviceGroup|否|服务的组名|String|HSF|
        |serviceVersion|否|服务的版本号|String|1.0.0.DAILY|
        |clientTimeout|否|客户端统一设置接口中所有方法的超时时间（单位ms）|int|-1|
        |generic|否|是否支持泛化调用|boolean|false|
        |addressWaitTime|否|同步等待服务注册中心（ ConfigServer ）推送服务提供者地址的时间（单位ms）|int|3000|
        |proxyStyle|否|代理方式（JDK或Javassist）|String|jdk|
        |futureMethods|否|设置调用此服务时需要采用异步调用的方法名列表以及异步调用的方式，默认为空，即所有方法都采用同步调用|String\[\]|空|
        |consistent|否|负载均衡是否使用一致性哈希|String|空|
        |methodSpecials|否|配置方法级的超时时间、重试次数、方法名称|com.alibaba.boot.hsf.annotation.HSFConsumer.ConsumerMethodSpecial\[\]|空|

        |属性|是否必配|描述|类型|默认值|
        |--|----|--|--|---|
        |spring.hsf.version|否|服务的全局版本号，还可以使用`spring.hsf.versions.<完整的服务接口名>=<单独为该服务接口设置的版本号，String类型>`，例如`spring.hsf.versions.com.aliware.edas.EchoService="1.0.0"`为具体某个服务设置版本号。|String|1.0.0.DAILY|
        |spring.hsf.group|否|服务的全局组名，还可以使用`spring.hsf.groups.<完整的服务接口名>=<单独为该服务接口设置的组名，String类型>`为具体某个服务设置组名。|String|HSF|
        |spring.hsf.timeout|否|服务的全局超时时间，还可以使用`spring.hsf.timeouts.<完整的服务接口名>=<超时时间，String类型>`为具体某个服务设置超时时间。|Integer|无|
        |spring.hsf.max-wait-address-time|否|同步等待服务注册中心（ ConfigServer ）推送服务提供者地址的全局时间（单位ms ），还可以使用`spring.hsf.max-wait-address-times.<完整的服务接口名>=<等待时间，String类型>`为具体某个服务设置的等待服务注册中心（ConfigServer）推送服务提供者地址的时间。|Integer|3000|
        |spring.hsf.delay-publish|否|服务延迟发布的全局开关，”true”or“false”，还可以使用`spring.hsf.delay-publishes.<完整的服务接口名>=<是否延迟发布，String类型>`为具体某个服务设置是否延迟。|String|无|
        |spring.hsf.core-pool-size|否|服务的全局最小活跃线程数，还可以使用`spring.hsf.core-pool-sizes.<完整的服务接口名>=<最小活跃线程数，String类型>`单独为某服务设置最小活跃线程数。|int|无|
        |spring.hsf.max-pool-size|否|服务的全局最大活跃线程数，还可以使用`spring.hsf.max-pool-sizes.<完整的服务接口名>=<最大活跃线程数，String类型>`单独为某服务设置最大活跃线程数。|int|无|
        |spring.hsf.serialize-type|否|服务的全局序列化类型，Hessian或者Java，还可以使用`spring.hsf.serialize-types.<完整的服务接口名>=<序列化类型>`单独为某服务设置序列化类型。|String|无|

        **说明：** 全局配置参数可在Pandora Boot应用的application.properties文件中设置。


## 本地开发调试

1.  配置轻量级配置及注册中心。

    本地开发调试时，需要使用轻量级配置及注册中心，轻量级配置及注册中心包含了服务注册发现服务端的轻量版，详情请参见[启动轻量级配置及注册中心]()。

2.  启动应用。

    -   在IDE中启动

        通过VM options配置启动参数-Djmenv.tbsite.net=\{$IP\}，通过main方法直接启动。其中`{$IP}`为轻量配置中心的IP地址。例如本机启动轻量配置中心，则`{$IP}`为`127.0.0.1`。

        您也可以不配置JVM的参数，而是直接通过修改hosts文件将`jmenv.tbsite.net`绑定为轻量配置中心的IP。详情请参见[启动轻量级配置及注册中心]()。

    -   通过FatJar启动
        1.  增加taobao-hsf.sar依赖，这样会下载到我们需要的依赖：/.m2/com/taobao/pandora/taobao-hsf.sar/2019-06-stable/taobao-hsf.sar-2019-06-stable.jar，在后面的启动参数中依赖它。

            ```
               <dependency>
                    <groupId>com.taobao.pandora</groupId>
                    <artifactId>taobao-hsf.sar</artifactId>
                    <version>2019-06-stable</version>
                </dependency>
            ```

        2.  使用Maven将Pandora Boot工程打包成FatJar， 需要在pom.xml中添加如下插件。为避免与其他打包插件发生冲突，请勿在build的plugin中添加其他FatJar插件。

            ```
                <plugin>
                    <groupId>com.taobao.pandora</groupId>
                    <artifactId>pandora-boot-maven-plugin</artifactId>
                    <version>2.1.11.8</version>
                    <executions>
                        <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                        </execution>
                    </executions>
                </plugin>
            ```

        3.  添加完插件后，在工程的主目录下，执行Maven命令`mvn clean package`进行打包，即可在Target目录下找到打包好的FatJar文件。
        4.  通过Java命令启动应用。

            ```
            java -Djmenv.tbsite.net=127.0.0.1 -Dpandora.location=${M2_HOME}/.m2/repository/com/taobao/pandora/taobao-hsf.sar/2019-06-stable/taobao-hsf.sar-2019-06-stable.jar -jar hsf-pandora-boot-provider-1.0.jar
            ```

            **说明：** `-Dpandora.location`指定的路径必须是全路径，使用命令行启动时，必须显示指定taobao-hsf.sar的位置。

    访问consumer所在机器的地址，可以触发consumer远程调用provider。

    ```
    curl localhost:8080/hsf-echo/helloworld
    helloworld
    ```


## 单元测试

Pandora Boot的单元测试可以通过PandoraBootRunner启动，并与SpringJUnit4ClassRunner无缝集成。

我们将演示一下如何在服务提供者中进行单元测试，供大家参考。

1.  在Maven中添加Pandora Boot和Spring Boot测试必要的依赖。

    ```
      <dependency>
          <groupId>com.taobao.pandora</groupId>
          <artifactId>pandora-boot-test</artifactId>
          <scope>test</scope>
      </dependency>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-test</artifactId>
          <scope>test</scope>
      </dependency>
    ```

2.  编写测试类的代码。

    ```
    @RunWith(PandoraBootRunner.class)
      @DelegateTo(SpringJUnit4ClassRunner.class)
      // 加载测试需要的类，一定要加入Spring Boot的启动类，其次需要加入本类。
      @SpringBootTest(classes = {HSFProviderApplication.class, HelloServiceTest.class })
      @Component
      public class HelloServiceTest {
    
          /**
           * 当使用 @HSFConsumer时，一定要在 @SpringBootTest类加载中，加载本类，通过本类来注入对象，否则当做泛化时，会出现类转换异常。
           */
          @HSFConsumer(generic = true)
          HelloService helloService;
    
          //普通的调用。
          @Test
          public void testInvoke() {
              TestCase.assertEquals("hello world", helloService.echo("hello world"));
          }
          //泛化调用。
          @Test
          public void testGenericInvoke() {
              GenericService service = (GenericService) helloService;
              Object result = service.$invoke("echo", new String[] {"java.lang.String"}, new Object[] {"hello world"});
              TestCase.assertEquals("hello world", result);
          }
          //返回值Mock。
          @Test
          public void testMock() {
              HelloService mock = Mockito.mock(HelloService.class, AdditionalAnswers.delegatesTo(helloService));
              Mockito.when(mock.echo("")).thenReturn("beta");
              TestCase.assertEquals("beta", mock.echo(""));
          }
      }
    ```


