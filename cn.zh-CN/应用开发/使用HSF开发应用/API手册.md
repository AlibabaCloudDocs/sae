# API手册

在HSF应用的API中，最关键的是创建ProviderBean和ConsumerBean相关的API。

根据用户使用的场景不同，主要分为4个关键的类。

-   com.taobao.hsf.app.api.util.HSFApiProviderBean: 通过API编程的方式创建Provider Bean
-   com.taobao.hsf.app.api.util.HSFApiConsumerBean: 通过API编程的方式创建Consumer Bean
-   com.taobao.hsf.app.spring.util.HSFSpringProviderBean: 通过Spirng配置的方式创建Provider Bean
-   com.taobao.hsf.app.spring.util.HSFSpringConsumerBean: 通过Spirng配置的方式创建Consumer Bean

其中，HSFSpringXxxBean的配置属性与HSFApiXxxBean的setter方法相对应。接下来就分别以ProviderBean和ConsumerBean的视角介绍这4个类的API。

## ProviderBean

-   API编程方式 - HSFApiProviderBean

    通过配置并初始化com.taobao.hsf.app.api.util.HSFApiProviderBean即可完成HSF服务的发布。

    对于一个服务，com.taobao.hsf.app.api.util.HSFApiProviderBean的配置及初始化过程只需配置一次。此外，考虑到HSFApiProviderBean对象比较复杂，建议缓存。

    -   范例代码：

        ```
        // 实例化并配置Provider Bean
        HSFApiProviderBean hsfApiProviderBean = new HSFApiProviderBean();
        hsfApiProviderBean.setServiceInterface("com.taobao.hsf.test.HelloWorldService");
        hsfApiProviderBean.setTarget(target); // target为serviceInterface指定接口的实现对象hsfApiProviderBean.setServiceVersion("1.0.0");
        hsfApiProviderBean.setServiceGroup("HSF");
        
        // 初始化Provider Bean，发布服务hsfApiProviderBean.init();
        ```

    -   可配置属性表：

        除上述范例代码中设置的属性，HSFApiProviderBean还包含许多其他可配置的属性，均可通过对应的setter方法进行设置。

        |属性名|类型|是否必选|默认值|含义|
        |---|--|----|---|--|
        |serviceInterface|String|是|无|设置HSF服务对外提供的业务接口。 客户端通过此属性进行订阅。|
        |target|Object|是|无|设置serviceInterface指定接口的服务实现对象。|
        |serviceVersion|String|否|1.0.0|设置服务的版本号。 客户端通过此属性进行订阅。|
        |serviceGroup|String|否|HSF|设置服务的组别。 客户端通过此属性进行订阅。|
        |serviceDesc|String|否|null|设置服务的描述，从而方便管理。|
        |clientTimeout|int|否|3000|设置响应超时时间（单位：毫秒）。如果服务端在设置的时间内没有返回，则抛出HSFTimeOutException。|
        |methodSpecials|MethodSpecial\[\]|否|空|设置服务中某些方法的响应超时时间。通过设置MethodSpecial.methodName指定方法名，通过设置MethodSpecial.clientTimout指定当前方法的超时时间，优先级高于当前服务端的clientTimeout。|
        |preferSerializeType|String|否|hessian2|针对HSF2，设置服务的请求参数和响应结果的序列化方式。可选值有java、hessian、hessian2、json和kryo。|
        |corePoolSize|值为整型的String|否|0|配置服务单独的线程池，并指定最小活跃线程数量。若不设置该属性，则默认使用HSF服务端的公共线程池。|
        |maxPoolSize|值为整型的String|否|0|配置服务单独的线程池，并指定最大活跃线程数量。若不设置该属性，则默认使用HSF服务端的公共线程池。|

-   Spring配置方式 - HSFSpringProviderBean

    通过在Spring配置文件中，配置一个class为com.taobao.hsf.app.spring.util.HSFSpringProviderBean的bean，即可完成HSF服务的发布。

    示例代码

    ```
    <bean id="helloWorldService" class="com.taobao.hsf.test.HelloWorldService" />
    
    <bean class="com.taobao.hsf.app.spring.util.HSFSpringProviderBean" init-method="init">
        <!-- [必选] 设置HSF服务对外提供的业务接口 -->
        <property name="serviceInterface" value="com.taobao.hsf.test.HelloWorldService" />
    
        <!-- [必选] 设置serviceInterface指定接口的服务实现对象，即需要发布为HSF服务的spring bean id -->
        <property name="target" ref="helloWorldService" />
    
        <!-- [可选] 设置服务的版本号，默认为1.0.0 -->
        <property name="serviceVersion" value="1.0.0" />
    
        <!-- [可选] 设置服务的组别，默认为HSF -->
        <property name="serviceGroup" value="HSF" />
    
        <!-- [可选] 设置服务的描述，从而方便管理，默认为null -->
        <property name="serviceDesc" value="HelloWorldService providered by HSF" />
    
        <!-- [可选] 设置响应超时时间（单位：毫秒）。如果服务端在设置的时间内没有返回，则抛出HSFTimeOutException -->
        <!-- 默认为3000 ms -->
        <property name="clientTimeout" value="3000"/>
    
        <!-- [可选] 设置服务中某些方法的响应超时时间。优先级高于上面的clientTimeout -->
        <!-- 通过设置MethodSpecial.methodName指定方法名，MethodSpecial.clientTimout指定方法的超时时间 -->
        <property name="methodSpecials">
            <list>
                <bean class="com.taobao.hsf.model.metadata.MethodSpecial">
                    <property name="methodName" value="sum" />
                    <property name="clientTimeout" value="2000" />
                </bean>
            </list>
        </property>
    
        <!-- [可选] 设置服务的请求参数和响应结果的序列化方式。可选值包含java、hessian、hessian2、json和kryo -->
        <!-- 默认为hessian2 -->
        <property name="preferSerializeType" value="hessian2"/>
    
        <!-- [可选] 配置服务单独的线程池，并指定最小活跃线程数量。若不设置该属性，则默认使用HSF服务端的公共线程池 -->
        <property name="corePoolSize" value="10"/>
    
        <!-- [可选] 配置服务单独的线程池，并指定最大活跃线程数量。若不设置该属性，则默认使用HSF服务端的公共线程池 -->
        <property name="maxPoolSize" value="60"/>
    </bean>
    ```


## ConsumerBean

-   API配置方式 - HSFApiConsumerBean

    通过配置并初始化com.taobao.hsf.app.api.util.HSFApiConsumerBean完成HSF服务的订阅。

    对于同一个服务，com.taobao.hsf.app.api.util.HSFApiConsumerBean的配置及初始化过程只需配置一次。

    由于HSFApiConsumerBean对象内容多，建议将该对象以及获取到的HSF代理进行缓存。

    **说明：** 在HSF内部HSFApiConsumerBean对服务的配置是缓存起来的。即如果对某个订阅的服务进行了多次配置，只有第一次的配置生效。

    -   范例代码

        ```
        // 实例化并配置Consumer Bean
        HSFApiConsumerBean hsfApiConsumerBean = new HSFApiConsumerBean();
        hsfApiConsumerBean.setInterfaceName("com.taobao.hsf.test.HelloWorldService");
        hsfApiConsumerBean.setVersion("1.0.0");
        hsfApiConsumerBean.setGroup("HSF");
        
        // 初始化Consumer Bean，订阅服务
        // true表示等待地址推送（超时时间为3000毫秒），默认为false（异步）
        hsfApiConsumerBean.init(true);
        
        // 获取HSF代理HelloWorldService helloWorldService = (HelloWorldService) hsfApiConsumerBean.getObject();
        
        // 发起HSF调用String helloStr = helloWorldService.sayHello("Li Lei");
        ```

    -   可配置属性表

        除上述范例代码中设置的属性，HSFApiConsumerBean还包含许多其他可配置的属性，均可通过对应的setter方法进行设置。

        |属性名|类型|是否必选|默认值|含义|
        |---|--|----|---|--|
        |interfaceName|String|是|无|设置需要订阅服务的接口名。 客户端通过此属性进行订阅。|
        |version|String|是|无|设置需要订阅服务的版本号。 客户端通过此属性进行订阅。|
        |group|String|是|无|设置需要订阅服务的组别。 客户端通过此属性进行订阅。|
        |clientTimeout|int|否|无|设置请求超时时间（单位：毫秒）。如果客户端在设置的时间内没有收到服务端响应，则抛出HSFTimeOutException。 若客户端设置了clientTimeout，则优先级高于服务端设置的clientTimeout。否则，在服务的远程调用过程中，使用服务端设置的clientTimeout。|
        |methodSpecials|MethodSpecial\[\]|否|空|设置服务中某些方法的请求超时时间。通过设置MethodSpecial.methodName指定方法名，通过设置MethodSpecial.clientTimout指定当前方法的超时时间，优先级高于当前客户端的clientTimeout。|
        |maxWaitTimeForCsAddress|int|否|无|设置同步等待ConfigServer推送地址的时间（单位：毫秒），从而避免因地址还未推送到就发起服务调用造成的HSFAddressNotFoundException。一般建议设置为5000毫秒，即可满足推送等待时间。|
        |asyncallMethods|List|否|null|设置需要异步调用的方法列表。List中的每一个字符串的格式为：        -   name：方法名
        -   type：异步调用类型
        -   listener：监听器
其中listener只对callback类型的异步调用生效。type的类型有：        -   future：通过Future的方式去获取请求执行的结果。
        -   callback：当远程服务的调用完成后，HSF会使用响应结果回调此处配置的listener，该listener需要实现HSFResponseCallback接口。 |
        |proxyStyle|String|否|jdk|设置服务的代理模式，一般不用配置。如果要拦截这个consumer bean，需要配置成javassist。|

-   Spring配置方式 - HSFSpringConsumerBean

    通过在Spring配置文件中，配置一个class为com.taobao.hsf.app.api.util.HSFSpringConsumerBean的bean，即可实现服务的订阅。

    示例代码

    ```
    <bean id="helloWorldService" class="com.taobao.hsf.app.spring.util.HSFSpringConsumerBean">
        <!-- [必选] 设置需要订阅服务的接口名 -->
        <property name="interfaceName" value="com.taobao.hsf.test.HelloWorldService" />
    
        <!-- [必选] 设置需要订阅服务的版本号 -->
        <property name="version" value="1.0.0" />
    
        <!-- [必选] 设置需要订阅服务的组别 -->
        <property name="group" value="HSF" />
    
        <!-- [可选] 设置请求超时时间（单位：毫秒）。如果客户端在设置的时间内没有收到服务端响应，则抛出HSFTimeOutException -->
        <!-- 若客户端设置了clientTimeout，则优先级高于服务端设置的clientTimeout。否则，在服务的远程调用过程中，使用服务端设置的clientTimeout。-->
        <property name="clientTimeout" value="3000" />
    
        <!-- [可选] 设置服务中某些方法的请求超时时间，优先级高于当前客户端的clientTimeout -->
        <!-- 通过设置MethodSpecial.methodName指定方法名，通过设置MethodSpecial.clientTimout指定当前方法的超时时间 -->
        <property name="methodSpecials">
            <list>
                <bean class="com.taobao.hsf.model.metadata.MethodSpecial">
                    <property name="methodName" value="sum" />
                    <property name="clientTimeout" value="2000" />
                </bean>
            </list>
        </property>
    
        <!-- [可选] 设置同步等待ConfigServer推送地址的时间（单位：毫秒）-->
        <!-- 从而避免因地址还未推送到就发起服务调用造成的HSFAddressNotFoundException -->
        <!-- 一般建议设置为5000毫秒，即可满足推送等待时间 -->
        <property name="maxWaitTimeForCsAddress"  value="5000"/>
    
        <!-- [可选] 设置需要异步调用的方法列表。List中的每一个字符串的格式为：-->
        <!-- name：方法名 -->
        <!-- type：异步调用类型 -->
        <!-- listener：监听器 -->
        <!-- 其中，listener只对callback类型的异步调用生效-->
        <!-- type的类型有： -->
        <!-- future: 通过Future的方式去获取请求执行的结果 -->
        <!-- callback: 当远程服务的调用完成后，HSF会使用响应结果回调此处配置的listener，该listener需要实现HSFResponseCallback接口 -->
        <property name="asyncallMethods">
            <list>
                <value>name:sayHello;type:callback;listener:com.taobao.hsf.test.service.HelloWorldServiceCallbackHandler</value>
            </list>
        </property>
    
        <!-- [可选] 设置服务的代理模式，一般不用配置。如果要拦截这个consumer bean，需要配置成javassist -->
        <property name="proxyStyle" value="jdk" />
    </bean>
    ```


