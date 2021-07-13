
---
title: 'Bus消息总线'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ce18a39b44754b7db176c49ad4d810a2~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 19:00:58 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ce18a39b44754b7db176c49ad4d810a2~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">学习目标</h2>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ce18a39b44754b7db176c49ad4d810a2~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-1">什么是消息总线</h2>
<p>　　文章摘自乐字节</p>
<p>　　消息代理中间件构建一个共用的消息主题让所有微服务实例订阅，当该消息主题产生消息时会被所有微服务实例监听和消费。</p>
<p>　　消息代理又是什么？消息代理是一个消息验证、传输、路由的架构模式，主要用来实现接收和分发消息，并根据设定好的消息处理流来转发给正确的应用。它在微服务之间起到通信调度作用，减少了服务之间的依赖。</p>
<p>　　</p>
<h2 data-id="heading-2">什么是 Spring Cloud Bus</h2>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7203c89ff4cc46329de061514950056b~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer">
　　Spring Cloud Bus 是 Spring Cloud 体系内的消息总线，用来连接分布式系统的所有节点。</p>
<p>　　Spring Cloud Bus 将分布式的节点用轻量的消息代理（RibbitMQ、Kafka）连接起来。可以通过消息代理广播配置文件的更改，或服务之间的通讯，也可以用于监控。解决了微服务数据变更，及时同步的问题。</p>
<p>　</p>
<h2 data-id="heading-3">什么时候使用 Spring Cloud Bus</h2>
<p>　　微服务一般都采用集群方式部署，而且在高并发下经常需要对服务进行扩容、缩容、上线、下线的操作。比如我们需要更新配置，又或者需要同时失效所有服务器上的某个缓存，需要向所有相关的服务器发送命令，此时就可以选择使用 Spring Cloud Bus 了。</p>
<p>　　总的来说，就是在我们需要把一个操作散发到所有后端相关服务器的时候，就可以选择使用 Spring Cloud Bus 了。</p>
<p>　　接下来我们通过 Spring Cloud Bus 实现微服务架构的配置刷新。</p>
<p>　　</p>
<h2 data-id="heading-4">环境准备</h2>
<p>　　</p>
<p>　　<code>RibbitMQ v3.8.2</code> 地址：<code>192.168.10.101</code></p>
<p>　　</p>
<p>　　<code>bus-demo</code> 聚合工程 <code>SpringBoot 2.2.4.RELEASE</code>、<code>Spring Cloud Hoxton.SR1</code>。</p>
<ul>
<li><code>eureka-server</code>：注册中心</li>
<li><code>eureka-server02</code>：注册中心</li>
<li><code>config-server</code>：配置中心服务端</li>
<li><code>config-server02</code>：配置中心服务端</li>
<li><code>order-service</code>：订单服务（配置中心客户端）</li>
<li><code>order-service02</code>：订单服务（配置中心客户端）</li>
</ul>
<p>　　</p>
<p>　　配置文件 <code>order-service-prod.yml</code></p>
<pre><code class="hljs language-yml copyable" lang="yml"><span class="hljs-attr">spring:</span>
  <span class="hljs-attr">application:</span>
    <span class="hljs-attr">name:</span> <span class="hljs-string">order-service</span> <span class="hljs-comment"># 应用名称</span>

<span class="hljs-comment"># 配置 Eureka Server 注册中心</span>
<span class="hljs-attr">eureka:</span>
  <span class="hljs-attr">instance:</span>
    <span class="hljs-attr">prefer-ip-address:</span> <span class="hljs-literal">true</span>       <span class="hljs-comment"># 是否使用 ip 地址注册</span>
    <span class="hljs-attr">instance-id:</span> <span class="hljs-string">$&#123;spring.cloud.client.ip-address&#125;:$&#123;server.port&#125;</span> <span class="hljs-comment"># ip:port</span>
  <span class="hljs-attr">client:</span>
    <span class="hljs-attr">service-url:</span>                  <span class="hljs-comment"># 设置服务注册中心地址</span>
      <span class="hljs-attr">defaultZone:</span> <span class="hljs-string">http://localhost:8761/eureka/,http://localhost:8762/eureka/</span>

<span class="hljs-comment"># 自定义配置</span>
<span class="hljs-attr">name:</span> <span class="hljs-string">order-service-prod</span>
<span class="hljs-attr">password:</span> <span class="hljs-string">root</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>　　</p>
<h2 data-id="heading-5">Spring Cloud Bus 实现配置刷新</h2>
<p>　　</p>
<h3 data-id="heading-6">客户端发起通知</h3>
<p>　　</p>
<p>　　消息总线（Bus）的典型应用场景就是配置中心客户端刷新。</p>
<p>　　我们在学习 Spring Cloud Config 配置中心时给大家讲了基于 <code>Actuator</code> 的配置刷新，当时的案例只有一个 Config Client，我们可以使用 Webhook，设置手动刷新都不算太费事，但是如果客户端比较多的情况下，一个一个去手动刷新未免有点复杂，这种方案就不太适合了。使用 Spring Cloud Bus 可以完美解决这一问题。</p>
<p>　　借助 Spring Cloud Bus 的广播功能，让 Config Client 都订阅配置更新事件，当配置更新时，触发其中一个端的更新事件，Spring Cloud Bus 就把此事件广播到其他订阅客户端，以此来达到批量更新。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/824dd1358cec4f8dadb83a3f9c5c206d~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<ol>
<li>Webhook 监听被触发，给 ConfigClient A 发送 bus-refresh 请求刷新配置</li>
<li>ConfigClient A 读取 ConfigServer 中的配置，并且发送消息给 Bus</li>
<li>Bus 接收消息后广播通知其他 ConfigClient</li>
<li>其他 ConfigClient 收到消息重新读取最新配置</li>
</ol>
<p>　　</p>
<h4 data-id="heading-7">添加依赖</h4>
<p>　　</p>
<p>　　Config Client 添加 <code>spring cloud starter bus amqp</code> 依赖。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eaf17676ef3a44c79ceb80355cb013a5~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<pre><code class="hljs language-xml copyable" lang="xml"><span class="hljs-comment"><!-- spring cloud starter bus amqp 依赖 --></span>
<span class="hljs-tag"><<span class="hljs-name">dependency</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">groupId</span>></span>org.springframework.cloud<span class="hljs-tag"></<span class="hljs-name">groupId</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">artifactId</span>></span>spring-cloud-starter-bus-amqp<span class="hljs-tag"></<span class="hljs-name">artifactId</span>></span>
<span class="hljs-tag"></<span class="hljs-name">dependency</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>　　</p>
<h4 data-id="heading-8">配置文件</h4>
<p>　　</p>
<p>　　配置文件需要配置 <code>消息队列</code> 和 <code>bus-refresh</code> 自动刷新端点。<code>/actuator/bus-refresh</code> 端点会清除 <code>@RefreshScope</code> 缓存重新绑定属性。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/79e95331813c44d2b093d27db077efee~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<p>　　Config Client 的 <code>bootstrap.yml</code> 核心配置。</p>
<pre><code class="hljs language-yml copyable" lang="yml"><span class="hljs-attr">spring:</span>
  <span class="hljs-attr">cloud:</span>
    <span class="hljs-attr">config:</span>
      <span class="hljs-attr">name:</span> <span class="hljs-string">order-service</span> <span class="hljs-comment"># 配置文件名称，对应 git 仓库中配置文件前半部分</span>
      <span class="hljs-attr">label:</span> <span class="hljs-string">master</span> <span class="hljs-comment"># git 分支</span>
      <span class="hljs-attr">profile:</span> <span class="hljs-string">prod</span> <span class="hljs-comment"># 指定环境</span>
      <span class="hljs-attr">discovery:</span>
        <span class="hljs-attr">enabled:</span> <span class="hljs-literal">true</span> <span class="hljs-comment"># 开启</span>
        <span class="hljs-attr">service-id:</span> <span class="hljs-string">config-server</span> <span class="hljs-comment"># 指定配置中心服务端的 service-id</span>
  <span class="hljs-comment"># 消息队列</span>
  <span class="hljs-attr">rabbitmq:</span>
    <span class="hljs-attr">host:</span> <span class="hljs-number">192.168</span><span class="hljs-number">.10</span><span class="hljs-number">.106</span>

<span class="hljs-comment"># 度量指标监控与健康检查</span>
<span class="hljs-attr">management:</span>
  <span class="hljs-attr">endpoints:</span>
    <span class="hljs-attr">web:</span>
      <span class="hljs-attr">base-path:</span> <span class="hljs-string">/actuator</span>    <span class="hljs-comment"># 访问端点根路径，默认为 /actuator</span>
      <span class="hljs-attr">exposure:</span>
        <span class="hljs-attr">include:</span> <span class="hljs-string">bus-refresh</span>  <span class="hljs-comment"># 需要开启的端点</span>
        <span class="hljs-comment">#exclude:             # 不需要开启的端点</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>　　</p>
<h4 data-id="heading-9">测试</h4>
<p>　　</p>
<h5 data-id="heading-10">查看端点</h5>
<p>　　</p>
<p>　　可以看到已经开启了 <code>bus-refresh</code> 自动刷新端点。</p>
<p>　　<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/932733ab048e4f518081150373bae9b2~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d602084e249c40d3ba49660e34d9d075~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/356bf531347e48b786978e42847d7ed0~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<p>　　</p>
<h5 data-id="heading-11">修改 Git 仓库配置</h5>
<p>　　</p>
<p>　　修改 Git 仓库配置信息如下：</p>
<pre><code class="hljs language-yml copyable" lang="yml"><span class="hljs-comment"># 自定义配置</span>
<span class="hljs-attr">name:</span> <span class="hljs-string">order-service-prod-1.0</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>　　</p>
<h5 data-id="heading-12">自动刷新</h5>
<p>　　</p>
<p>　　刷新页面发现结果并未改变，没事正常。</p>
<p>　　通过 Post 方式调用<strong>任意客户端</strong>的自动刷新端点：再次访问结果如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ed238427632b42e695626462f35fbdcf~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer">
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2601398ddfe0428bb1ae177b40eb796e~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<h5 data-id="heading-13">查看队列</h5>
<p>　　</p>
<p>　　再来观察一下消息队列的 UI 界面，发现多了一个 <code>springCloudBus</code> 的交换机。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/57a4ac6cc25e4da58335fe54f57bf2af~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<p>　　该交换机下绑定了两个队列对应我们的两个 Config Client。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/09285eccd81e4c039332560cfe0aa6b5~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<h4 data-id="heading-14">客户端发起通知缺陷</h4>
<p>　　</p>
<ul>
<li>打破了微服务的职责单一性。微服务本身是业务模块，它本不应该承担配置刷新的职责。</li>
<li>破坏了微服务各节点的对等性。</li>
<li>存在一定的局限性。例如，微服务在迁移时，它的网络地址常常会发生变化，此时如果想要做到自动刷新，就不得不修改Webhook 的配置。</li>
</ul>
<p>　　</p>
<h3 data-id="heading-15">服务端发起通知</h3>
<p>　　</p>
<p>　　为了解决客户端发起通知缺陷，我们改用服务端发起通知。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d70d64dc063644538a3bd9da2a3e72d5~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<ol>
<li>Webhook监听被触发，给 ConfigServer 发送 bus-refresh 请求刷新配置</li>
<li>ConfigServer 发送消息给 Bus</li>
<li>Bus 接收消息后广播通知所有 ConfigClient</li>
<li>各 ConfigClient 收到消息重新读取最新配置</li>
</ol>
<p>　　</p>
<h4 data-id="heading-16">添加依赖</h4>
<p>　　</p>
<p>　　Config Server 添加 <code>spring cloud starter bus amqp</code> 依赖。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4570b627028d4c2bac00bcd83bdf8c4a~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<pre><code class="hljs language-xml copyable" lang="xml"><span class="hljs-comment"><!-- spring cloud starter bus amqp 依赖 --></span>
<span class="hljs-tag"><<span class="hljs-name">dependency</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">groupId</span>></span>org.springframework.cloud<span class="hljs-tag"></<span class="hljs-name">groupId</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">artifactId</span>></span>spring-cloud-starter-bus-amqp<span class="hljs-tag"></<span class="hljs-name">artifactId</span>></span>
<span class="hljs-tag"></<span class="hljs-name">dependency</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>　　</p>
<h4 data-id="heading-17">配置文件</h4>
<p>　　</p>
<p>　　配置文件需要配置 <code>消息队列</code> 和 <code>bus-refresh</code> 自动刷新端点。<code>/actuator/bus-refresh</code> 端点会清除 <code>@RefreshScope</code> 缓存重新绑定属性。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1639dbb841d4447aaa01b9585189c918~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<p>　　Config Server 的 <code>application.yml</code> 核心配置。</p>
<pre><code class="hljs language-yml copyable" lang="yml"><span class="hljs-attr">spring:</span>
  <span class="hljs-attr">application:</span>
    <span class="hljs-attr">name:</span> <span class="hljs-string">config-server</span> <span class="hljs-comment"># 应用名称</span>
  <span class="hljs-attr">cloud:</span>
    <span class="hljs-attr">config:</span>
      <span class="hljs-attr">server:</span>
        <span class="hljs-attr">git:</span>
          <span class="hljs-attr">uri:</span> <span class="hljs-string">https://github.com/imrhelloworld/config-repo</span> <span class="hljs-comment"># 配置文件所在仓库地址</span>
          <span class="hljs-comment">#username:             # Github 等产品的登录账号</span>
          <span class="hljs-comment">#password:             # Github 等产品的登录密码</span>
          <span class="hljs-comment">#default-label: master # 配置文件分支</span>
          <span class="hljs-comment">#search-paths:         # 配置文件所在根目录</span>
  <span class="hljs-comment"># 消息队列</span>
  <span class="hljs-attr">rabbitmq:</span>
    <span class="hljs-attr">host:</span> <span class="hljs-number">192.168</span><span class="hljs-number">.10</span><span class="hljs-number">.106</span>

<span class="hljs-comment"># 配置 Eureka Server 注册中心</span>
<span class="hljs-attr">eureka:</span>
  <span class="hljs-attr">instance:</span>
    <span class="hljs-attr">prefer-ip-address:</span> <span class="hljs-literal">true</span>       <span class="hljs-comment"># 是否使用 ip 地址注册</span>
    <span class="hljs-attr">instance-id:</span> <span class="hljs-string">$&#123;spring.cloud.client.ip-address&#125;:$&#123;server.port&#125;</span> <span class="hljs-comment"># ip:port</span>
  <span class="hljs-attr">client:</span>
    <span class="hljs-attr">service-url:</span>                  <span class="hljs-comment"># 设置服务注册中心地址</span>
      <span class="hljs-attr">defaultZone:</span> <span class="hljs-string">http://localhost:8761/eureka/,http://localhost:8762/eureka/</span>

<span class="hljs-comment"># 度量指标监控与健康检查</span>
<span class="hljs-attr">management:</span>
  <span class="hljs-attr">endpoints:</span>
    <span class="hljs-attr">web:</span>
      <span class="hljs-attr">base-path:</span> <span class="hljs-string">/actuator</span>    <span class="hljs-comment"># 访问端点根路径，默认为 /actuator</span>
      <span class="hljs-attr">exposure:</span>
        <span class="hljs-attr">include:</span> <span class="hljs-string">bus-refresh</span>  <span class="hljs-comment"># 需要开启的端点</span>
        <span class="hljs-comment">#exclude:             # 不需要开启的端点</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>文章摘自乐字节</p></div>  
</div>
            