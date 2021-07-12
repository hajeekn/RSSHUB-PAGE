
---
title: '自己动手从0开始实现一个分布式RPC框架'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f5cdcfc0582441159e55355aba33ec66~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 18:36:14 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f5cdcfc0582441159e55355aba33ec66~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p><strong>简介：</strong> 如果一个程序员能清楚的了解RPC框架所具备的要素，掌握RPC框架中涉及的服务注册发现、负载均衡、序列化协议、RPC通信协议、Socket通信、异步调用、熔断降级等技术，可以全方位的提升基本素质。虽然也有相关源码，但是只看源码容易眼高手低，动手写一个才是自己真正掌握这门技术的最优路径。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f5cdcfc0582441159e55355aba33ec66~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>作者 | 麓行<br>
来源 | 阿里技术公众号</p>
<h3 data-id="heading-0">前言</h3>
<p>为什么要自己写一个RPC框架，我觉得从个人成长上说，如果一个程序员能清楚的了解RPC框架所具备的要素，掌握RPC框架中涉及的服务注册发现、负载均衡、序列化协议、RPC通信协议、Socket通信、异步调用、熔断降级等技术，可以全方位的提升基本素质。虽然也有相关源码，但是只看源码容易眼高手低，动手写一个才是自己真正掌握这门技术的最优路径。</p>
<h3 data-id="heading-1">一 什么是RPC</h3>
<p>RPC（Remote Procedure Call）远程过程调用，简言之就是像调用本地方法一样调用远程服务。目前外界使用较多的有gRPC、Dubbo、Spring Cloud等。相信大家对RPC的概念都已经很熟悉了，这里不做过多介绍。</p>
<h3 data-id="heading-2">二 分布式RPC框架要素</h3>
<p>一款分布式RPC框架离不开三个基本要素：</p>
<ul>
<li>服务提供方 Serivce Provider</li>
<li>服务消费方 Servce Consumer</li>
<li>注册中心 Registery</li>
</ul>
<p>围绕上面三个基本要素可以进一步扩展服务路由、负载均衡、服务熔断降级、序列化协议、通信协议等等。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a8cc6f89c89a4b14901bdad2ba667c57~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h4 data-id="heading-3">1 注册中心</h4>
<p>主要是用来完成服务注册和发现的工作。虽然服务调用是服务消费方直接发向服务提供方的，但是现在服务都是集群部署，服务的提供者数量也是动态变化的，所以服务的地址也就无法预先确定。因此如何发现这些服务就需要一个统一注册中心来承载。</p>
<h4 data-id="heading-4">2 服务提供方（RPC服务端）</h4>
<p>其需要对外提供服务接口，它需要在应用启动时连接注册中心，将服务名及其服务元数据发往注册中心。同时需要提供服务服务下线的机制。需要维护服务名和真正服务地址映射。服务端还需要启动Socket服务监听客户端请求。</p>
<h4 data-id="heading-5">3 服务消费方（RPC客户端）</h4>
<p>客户端需要有从注册中心获取服务的基本能力，它需要在应用启动时，扫描依赖的RPC服务，并为其生成代理调用对象，同时从注册中心拉取服务元数据存入本地缓存，然后发起监听各服务的变动做到及时更新缓存。在发起服务调用时，通过代理调用对象，从本地缓存中获取服务地址列表，然后选择一种负载均衡策略筛选出一个目标地址发起调用。调用时会对请求数据进行序列化，并采用一种约定的通信协议进行socket通信。</p>
<h3 data-id="heading-6">三 技术选型</h3>
<h4 data-id="heading-7">1 注册中心</h4>
<p>目前成熟的注册中心有Zookeeper，Nacos，Consul，Eureka，它们的主要比较如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2929908c572a4b1789f303f3c5331746~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>本实现中支持了两种注册中心Nacos和Zookeeper，可根据配置进行切换。</p>
<h4 data-id="heading-8">2 IO通信框架</h4>
<p>本实现采用Netty作为底层通信框架，Netty是一个高性能事件驱动型的非阻塞的IO(NIO)框架。</p>
<h4 data-id="heading-9">3 通信协议</h4>
<p>TCP通信过程中会根据TCP缓冲区的实际情况进行包的划分，所以在业务上认为一个完整的包可能会被TCP拆分成多个包进行发送，也有可能把多个小的包封装成一个大的数据包发送，这就是所谓的TCP粘包和拆包问题。所以需要对发送的数据包封装到一种通信协议里。</p>
<p>业界的主流协议的解决方案可以归纳如下：</p>
<ol>
<li>消息定长，例如每个报文的大小为固定长度100字节，如果不够用空格补足。</li>
<li>在包尾特殊结束符进行分割。</li>
<li>将消息分为消息头和消息体，消息头中包含表示消息总长度（或者消息体长度）的字段。</li>
</ol>
<p>很明显1，2都有些局限性，本实现采用方案3，具体协议设计如下：</p>
<pre><code class="copyable">+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+ 
|  BYTE  |        |        |        |        |        |        |             ........ 
+--------------------------------------------+--------+-----------------+--------+--------+--------+--------+--------+--------+-----------------+ 
|  magic | version|  type  |           content lenth           |                   content byte[]                                        |        | 
+--------+-----------------------------------------------------------------------------------------+--------------------------------------------+
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>第一个字节是魔法数，比如我定义为0X35。</li>
<li>第二个字节代表协议版本号，以便对协议进行扩展，使用不同的协议解析器。</li>
<li>第三个字节是请求类型，如0代表请求1代表响应。</li>
<li>第四个字节表示消息长度，即此四个字节后面此长度的内容是消息content。</li>
</ul>
<h4 data-id="heading-10">4 序列化协议</h4>
<p>本实现支持3种序列化协议，JavaSerializer、Protobuf及Hessian可以根据配置灵活选择。建议选用Protobuf，其序列化后码流小性能高，非常适合RPC调用，Google自家的gRPC也是用其作为通信协议。</p>
<h4 data-id="heading-11">5 负载均衡</h4>
<p>本实现支持两种主要负载均衡策略，随机和轮询，其中他们都支持带权重的随机和轮询，其实也就是四种策略。</p>
<h3 data-id="heading-12">四 整体架构</h3>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/66899d45769a4692924e399de0e3fbae~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-13">五 实现</h3>
<p>项目总体结构：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ac6a2f812f57411faaec1de9e8e1e8f6~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h4 data-id="heading-14">1 服务注册发现</h4>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/78507923a3574019825b88df8b3ad8b0~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>Zookeeper</strong></p>
<p>Zookeeper采用节点树的数据模型，类似linux文件系统，/，/node1，/node2 比较简单。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/209528aafb384114943668eb57f9772b~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>Zookeeper节点类型是Zookeeper实现很多功能的核心原理，分为持久节点临时节点、顺序节点三种类型的节点。</p>
<p>我们采用的是对每个服务名创建一个持久节点，服务注册时实际上就是在zookeeper中该持久节点下创建了一个临时节点，该临时节点存储了服务的IP、端口、序列化方式等。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/79956662a7e8420c8b28c4a3bdfed9c2~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>客户端获取服务时通过获取持久节点下的临时节点列表，解析服务地址数据：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dc4d330bf1f64d01bd9ad069270b17fd~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>客户端监听服务变化：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a11cf8fe8e654127b0fc47c935d8babb~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>Nacos</strong></p>
<p>Nacos是阿里开源的微服务管理中间件，用来完成服务之间的注册发现和配置中心，相当于Spring Cloud的Eureka+Config。</p>
<p>不像Zookeeper需要利用提供的创建节点特性来实现注册发现，Nacos专门提供了注册发现功能，所以其使用更加方便简单。主要关注NamingService接口提供的三个方法registerInstance、getAllInstances、subscribe；registerInstance用来完成服务端服务注册，getAllInstances用来完成客户端服务获取，subscribe用来完成客户端服务变动监听，这里就不多做介绍，具体可参照实现源码。</p>
<h4 data-id="heading-15">2 服务提供方 Serivce Provider</h4>
<p>在自动配置类OrcRpcAutoConfiguration完成注册中心和RPC启动类（RpcBootStarter）的初始化：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5f6abcc50d5e4451948c70baa8cb991e~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>服务端的启动流程如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/efe819264cc4470a859c6ac4322b7046~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>RPC启动（RpcBootStarter）：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9710e0fc7d784d1cadc3e0d55e0f1568~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>上面监听Spring容器初始化事件时注意，由于Spring包含多个容器，如web容器和核心容器，他们还有父子关系，为了避免重复执行注册，只处理顶层的容器即可。</p>
<h4 data-id="heading-16">3 服务消费方 Servce Consumer</h4>
<p>服务消费方需要在应用启动完成前为依赖的服务创建好代理对象，这里有很多种方法，常见的有两种：</p>
<ul>
<li>一是在应用的Spring Context初始化完成事件时触发，扫描所有的Bean，将Bean中带有OrcRpcConsumer注解的field获取到，然后创建field类型的代理对象，创建完成后，将代理对象set给此field。后续就通过该代理对象创建服务端连接，并发起调用。</li>
<li>二是通过Spring的BeanFactoryPostProcessor，其可以对bean的定义BeanDefinition(配置元数据)进行处理；Spring IOC会在容器实例化任何其他bean之前运行BeanFactoryPostProcessor读取BeanDefinition，可以修改这些BeanDefinition，也可以新增一些BeanDefinition。</li>
</ul>
<p>本实现也采用第二种方式，处理流程如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ad1dd381f1744b04b22abb8a971e8982~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>BeanFactoryPostProcessor的主要实现：</p>
<pre><code class="copyable">    @Override
    public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory)
        throws BeansException &#123;
        this.beanFactory = beanFactory;
        postProcessRpcConsumerBeanFactory(beanFactory, (BeanDefinitionRegistry)beanFactory);
    &#125;

    private void postProcessRpcConsumerBeanFactory(ConfigurableListableBeanFactory beanFactory, BeanDefinitionRegistry beanDefinitionRegistry) &#123;
        String[] beanDefinitionNames = beanFactory.getBeanDefinitionNames();
        int len = beanDefinitionNames.length;
        for (int i = 0; i < len; i++) &#123;
            String beanDefinitionName = beanDefinitionNames[i];
            BeanDefinition beanDefinition = beanFactory.getBeanDefinition(beanDefinitionName);
            String beanClassName = beanDefinition.getBeanClassName();
            if (beanClassName != null) &#123;
                Class<?> clazz = ClassUtils.resolveClassName(beanClassName, classLoader);
                ReflectionUtils.doWithFields(clazz, new FieldCallback() &#123;
                    @Override
                    public void doWith(Field field) throws IllegalArgumentException, IllegalAccessException &#123;
                        parseField(field);
                    &#125;
                &#125;);
            &#125;

        &#125;

        Iterator<Entry<String, BeanDefinition>> it = beanDefinitions.entrySet().iterator();
        while (it.hasNext()) &#123;
            Entry<String, BeanDefinition> entry = it.next();
            if (context.containsBean(entry.getKey())) &#123;
                throw new IllegalArgumentException("Spring context already has a bean named " + entry.getKey());
            &#125;
            beanDefinitionRegistry.registerBeanDefinition(entry.getKey(), entry.getValue());
            log.info("register OrcRpcConsumerBean definition: &#123;&#125;", entry.getKey());
        &#125;

    &#125;

    private void parseField(Field field) &#123;
        // 获取所有OrcRpcConsumer注解
        OrcRpcConsumer orcRpcConsumer = field.getAnnotation(OrcRpcConsumer.class);
        if (orcRpcConsumer != null) &#123;
            // 使用field的类型和OrcRpcConsumer注解一起生成BeanDefinition
            OrcRpcConsumerBeanDefinitionBuilder beanDefinitionBuilder = new OrcRpcConsumerBeanDefinitionBuilder(field.getType(), orcRpcConsumer);
            BeanDefinition beanDefinition = beanDefinitionBuilder.build();
            beanDefinitions.put(field.getName(), beanDefinition);
        &#125;
    &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>ProxyFactory的主要实现：</p>
<pre><code class="copyable">public class JdkProxyFactory implements ProxyFactory&#123;

    @Override
    public Object getProxy(ServiceMetadata serviceMetadata) &#123;
        return Proxy
            .newProxyInstance(serviceMetadata.getClazz().getClassLoader(), new Class[] &#123;serviceMetadata.getClazz()&#125;,
                new ClientInvocationHandler(serviceMetadata));
    &#125;

    private class ClientInvocationHandler implements InvocationHandler &#123;

        private ServiceMetadata serviceMetadata;

        public ClientInvocationHandler(ServiceMetadata serviceMetadata) &#123;
            this.serviceMetadata = serviceMetadata;
        &#125;

        @Override
        public Object invoke(Object proxy, Method method, Object[] args) throws Throwable &#123;
            String serviceId = ServiceUtils.getServiceId(serviceMetadata);
            // 通过负载均衡器选取一个服务提供方地址
            ServiceURL service = InvocationServiceSelector.select(serviceMetadata);

            OrcRpcRequest request = new OrcRpcRequest();
            request.setMethod(method.getName());
            request.setParameterTypes(method.getParameterTypes());
            request.setParameters(args);
            request.setRequestId(UUID.randomUUID().toString());
            request.setServiceId(serviceId);

            OrcRpcResponse response = InvocationClientContainer.getInvocationClient(service.getServerNet()).invoke(request, service);
            if (response.getStatus() == RpcStatusEnum.SUCCESS) &#123;
                return response.getData();
            &#125; else if (response.getException() != null) &#123;
                throw new OrcRpcException(response.getException().getMessage());
            &#125; else &#123;
                throw new OrcRpcException(response.getStatus().name());
            &#125;
        &#125;
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>本实现只使用JDK动态代理，也可以使用cglib或Javassist实现以获得更好的性能，JdkProxyFactory中。</p>
<h4 data-id="heading-17">4 IO模块</h4>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d6de758ceeeb45ccb92a5836c17a9322~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>UML图如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e75ce354b03548cc9c3bf34017adc113~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>结构比较清晰，分三大模块：客户端调用适配模块、服务端请求响应适配模块和Netty IO服务模块。</p>
<p><strong>客户端调用适配模块</strong></p>
<p>此模块比较简单，主要是为客户端调用时建立服务端接，并将连接存入缓存，避免后续同服务调用重复建立连接，连接建立成功后发起调用。下面是DefaultInvocationClient的实现：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c39c9d8bc61542a2aeff95d592f18ba0~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>服务端请求响应适配模块</strong></p>
<p>服务请求响应模块也比较简单，是根据请求中的服务名，从缓存中获取服务元数据，然后从请求中获取调用的方法和参数类型信息，反射获取调用方法信息。然后从spring context中获取bean进行反射调用。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c64d899f20ec4608a5ef4da31b94c724~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>Netty IO服务模块</strong></p>
<p>Netty IO服务模块是核心，稍复杂一些，客户端和服务端主要处理流程如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d6b0cf403b4c415fbcd3aa9ddfd174d3~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>其中，重点是这四个类的实现：NettyNetClient、NettyNetServer、NettyClientChannelRequestHandler和NettyServerChannelRequestHandler，上面的UML图和下面流程图基本上讲清楚了它们的关系和一次请求的处理流程，这里就不再展开了。</p>
<p>下面重点讲一下编码解码器。</p>
<p>在技术选型章节中，提及了采用的通信协议，定义了私有的RPC协议：</p>
<pre><code class="copyable">+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+ 
|  BYTE  |        |        |        |        |        |        |             ........ 
+--------------------------------------------+--------+-----------------+--------+--------+--------+--------+--------+--------+-----------------+ 
|  magic | version|  type  |           content lenth           |                   content byte[]                                        |        | 
+--------+-----------------------------------------------------------------------------------------+--------------------------------------------+
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>第一个字节是魔法数定义为0X35。</li>
<li>第二个字节代表协议版本号。</li>
<li>第三个字节是请求类型，0代表请求1代表响应。</li>
<li>第四个字节表示消息长度，即此四个字节后面此长度的内容是消息content。</li>
</ul>
<p>编码器的实现如下：</p>
<pre><code class="copyable">@Override
protected void encode(ChannelHandlerContext channelHandlerContext, ProtocolMsg protocolMsg, ByteBuf byteBuf)
    throws Exception &#123;
    // 写入协议头
    byteBuf.writeByte(ProtocolConstant.MAGIC);
    // 写入版本
    byteBuf.writeByte(ProtocolConstant.DEFAULT_VERSION);
    // 写入请求类型
    byteBuf.writeByte(protocolMsg.getMsgType());
    // 写入消息长度
    byteBuf.writeInt(protocolMsg.getContent().length);
    // 写入消息内容
    byteBuf.writeBytes(protocolMsg.getContent());
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>解码器的实现如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eddf61430b044d709e2ccfe19a3b247b~tplv-k3u1fbpfcp-zoom-1.image" alt="1_副本.png" title="1_副本.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-18">六 测试</h3>
<p>在本人MacBook Pro 13寸，4核I5，16g内存，使用Nacos注册中心，启动一个服务器，一个客户端情况下，采用轮询负载均衡策略的情况下，使用Apache ab测试。</p>
<p>在启用8个线程发起10000个请求的情况下，可以做到 18秒完成所有请求，qps550：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b3e4e612bfef42c592b5d92cc404d0a3~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>在启用100个线程发起10000个请求的情况下，可以做到 13.8秒完成所有请求，qps724：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a27a8f8b2c604a95828a0cec2c6753e5~tplv-k3u1fbpfcp-zoom-1.image" alt="image.png" title="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-19">七 总结</h3>
<p>在实现这个RPC框架的过程中，我也重新学习了很多知识，比如通信协议、IO框架等。也横向学习了当前最热的gRPC，借此又看了很多相关的源码，收获很大。后续我也会继续维护升级这个框架，比如引入熔断降级等机制，做到持续学习持续进步。</p>
<p><a href="https://link.juejin.cn/?target=http%3A%2F%2Fclick.aliyun.com%2Fm%2F1000282907%2F" target="_blank" rel="nofollow noopener noreferrer" title="http://click.aliyun.com/m/1000282907/" ref="nofollow noopener noreferrer">原文链接</a></p>
<p>本文为阿里云原创内容，未经允许不得转载。</p></div>  
</div>
            