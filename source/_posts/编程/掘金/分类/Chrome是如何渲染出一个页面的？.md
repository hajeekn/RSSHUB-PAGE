
---
title: 'Chrome是如何渲染出一个页面的？'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e940bc19bf084634a0972e7ce3f902d2~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 19:54:22 GMT
thumbnail: 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e940bc19bf084634a0972e7ce3f902d2~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>相信各位前端同学，都碰到过这样一个面试题：<strong>浏览器自输入url开始，到页面展示的过程中，究竟发生了什么？</strong></p>
<p>这个问题在掘金上已经有不少作者，发布了很完整的解答了。从解析 URL 、解析 DNS ，再到浏览器生成 Render Tree 并绘制页面，涵盖了网络层和应用层各方面的知识，属于一个比较开放的题目了。这篇文章将抛开网络协议层面，讲讲 Chrome 在这一过程中的工作。</p>
<h1 data-id="heading-0">Chrome的多进程架构</h1>
<p>当你在使用 Chrome 时，打开系统进程列表，你会发现有很多 Google Chrome 的进程已经在运行中，</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e940bc19bf084634a0972e7ce3f902d2~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>你可能会有点疑惑：为什么我只打开了一个Chrome应用，却有这么多个进程？</p>
<p>不同于普通的单进程应用，Chrome 是基于多进程架构设计而成，每个进程各司其职，它们之间通过 IPC 机制（Inter Process Communication）通信。</p>
<h2 data-id="heading-1">各进程介绍</h2>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/072722a582004ae6b2529db0cfd9f0cd~tplv-k3u1fbpfcp-watermark.image" alt="Chrome Processes.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<ul>
<li>Browser: 控制应用程序的“chrome”部分，包括地址栏、书签、后退和前进按钮。还处理 Web 浏览器的不可见的特权部分，例如网络请求和文件访问。</li>
<li>Renderer: 控制显示标签页内的任何内容，<strong>每个标签页，以及其中的iframe都会被分配一个Renderer进程。</strong></li>
<li>Plugin: 控制网站使用的任何插件，例如 flash。</li>
<li>GPU: 处理独立于其他进程的 GPU 任务。它被拆分成一个单独的进程，因为 GPU 处理来自多个应用程序的请求并将它们绘制在同一个界面上。</li>
<li>Extension: 扩展程序。</li>
<li>Utility: 工具进程。</li>
</ul>
<h2 data-id="heading-2">多进程架构的好处</h2>
<p>Chrome利用多进程架构，保证工作的<strong>稳定性</strong>。假设你打开了3个标签页，每个标签页都由一个独立的渲染进程运行。如果其中一个标签页崩溃了，那么你可以关闭这个标签页，同时保持其他标签页正常运行。但如果所有标签页都运行在一个渲染进程上，那么一个标签页崩溃会连带所有的一起崩溃。</p>
<p>但更多的进程意味着分配更多的内存空间，为了节省内存，Chrome 限制了它可以启动的进程数。该限制取决于设备的内存和 CPU 能力，当 Chrome 达到限制时，它会把运行在同一网站的多个标签页的 Renderer Processes 合并为一个。</p>
<p>Chrome将同样的方法应用于 Browser Process ，将它的每个部分作为服务运行，从而可以轻松地拆分为不同的进程或聚合为一个进程。
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2009e1aca62344ee821a0fc4d4dd449f~tplv-k3u1fbpfcp-watermark.image" alt="Browser Process.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<h1 data-id="heading-3">导航阶段</h1>
<h2 data-id="heading-4">Step 1：处理输入</h2>
<p>用户在浏览器地址栏中输入内容，负责处理用户输入的是 Browser Process 的 UI thread，它需要决定将用户输入的内容导向搜索引擎，或是当做网站地址处理。</p>
<h2 data-id="heading-5">Step 2：建立网络连接</h2>
<p>UI 线程通知网络线程，向对方站点发送网络请求，网络线程通过适当的协议，DNS 查找确定主机地址、建立 TCP 连接、通过 TLS 协商建立 HTTPS 连接。</p>
<h2 data-id="heading-6">Step 3：接收响应</h2>
<p>接收到对方站点返回的响应，网络线程先检查状态码，如果是以4或5开头的错误码，则通知渲染器进程，将渲染错误页面。</p>
<p>如果是重定向的状态码，则请求新的URL地址。</p>
<p>如果是成功的状态码，则判断 Content-Type 响应头，如果是 HTML 格式，会对 HTML 做安全检测，确保其不属于危险网站，以及 CORB（Cross Origin Read Blocking）检测，把敏感的跨站数据剔除掉；如果是其他格式，例如pdf、zip等等，尽可能解析它并在浏览器中展示、播放，或者直接下载到本地。</p>
<h2 data-id="heading-7">Step 4：分配/创建一个渲染进程</h2>
<p>网络线程的工作准备就绪之后，会先通知给 UI 线程，UI 线程再给这个网站分配一个渲染器进程。其实早在第二步中，UI 线程通知网络线程建立网络连接的时候，因为不清楚网络线程预期多久完成工作，为了缩短导航阶段耗费的时间，UI 线程就提前开始创建渲染器进程了。当网络线程完成工作后，渲染器进程就可以立马拿来用了。有一个例外就是，当请求被重定向后，这个提前创建好的渲染器进程就被浪费了，会被清除掉，再重新创建个新的进程。</p>
<h2 data-id="heading-8">Step 5：完成导航</h2>
<p>现在数据和渲染器进程已经准备就绪，浏览器进程发送 IPC 到渲染器进程以提交导航，同时传递 HTML 数据。一旦浏览器进程接收到渲染器进程的确认信息，导航就完成了，并且向浏览器 history 插入一条新纪录，导航栏更新为新的站点地址。</p>
<h2 data-id="heading-9">如果引入Service Worker</h2>
<blockquote>
<p>Service worker是一个注册在指定源和路径下的事件驱动worker。它采用JavaScript控制关联的页面或者网站，拦截并修改访问和资源请求，细粒度地缓存资源。你可以完全控制应用在特定情形（最常见的情形是网络不可用）下的表现。</p>
</blockquote>
<p>当导航发生时，网络线程会去 Service Worker 作用域中检查，当前请求的 URL 是否已在 Service Worker 注册，如果该 URL 已注册，则 UI 线程会查找渲染器进程以执行 Service Worker 代码。Service Worker 可能会从本地缓存中读取页面，从而无需发送网络请求。</p>
<h1 data-id="heading-10">渲染阶段</h1>
<p>该阶段的工作主要由渲染器进程完成，渲染器进程的核心工作是将 HTML、CSS 和 JavaScript 转换为用户可以与之交互的网页。</p>
<p>渲染器进程又包括以下几个线程：
<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/870715394ac44fa9b5f93e2284de137c~tplv-k3u1fbpfcp-watermark.image" alt="Renderer Process.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<ul>
<li>主线程处理大部分代码。</li>
<li>Worker用于分担主线程的计算量，但无法访问DOM。</li>
<li>合成器线程和光栅线程用于高效流畅地渲染页面。</li>
</ul>
<h2 data-id="heading-11">Step 1：解析文档</h2>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2cd2d33ab86b40bc8ee8763f4c547a3d~tplv-k3u1fbpfcp-watermark.image" alt="dom.png" loading="lazy" referrerpolicy="no-referrer">
渲染器进程的主线程自上而下地解析 HTML 文档，生成一个名为 DOM 的树形结构。解析方式是由 HTML 规范决定的，同时在解析过程中为了保证容错率，HTML 规范也提供了更优雅的容错方案：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fhtml.spec.whatwg.org%2Fmultipage%2Fparsing.html%23an-introduction-to-error-handling-and-strange-cases-in-the-parser" target="_blank" rel="nofollow noopener noreferrer" title="https://html.spec.whatwg.org/multipage/parsing.html#an-introduction-to-error-handling-and-strange-cases-in-the-parser" ref="nofollow noopener noreferrer">An introduction to error handling and strange cases in the parser
</a>.</p>
<p>一些外部的非阻塞资源，包括图片、CSS 文件等，主线程会在解析构建DOM的同时请求这些资源；但是对于<code><script></code>标签（特别是没有 async 或者 defer 属性）会阻塞渲染并停止HTML的解析。</p>
<h3 data-id="heading-12">预加载扫描器</h3>
<p>为了加快文档解析速度，“预加载扫描器”会在主线程刚开始解析文档时就扫描所需要的高优先级资源，如 CSS、JavaScript 和 web 字体并报告给网络线程，网络线程开始下载它们。运气好的话，当主线程解析到当前节点时，对应的资源可能已经下载完成了。</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">link</span> <span class="hljs-attr">rel</span>=<span class="hljs-string">"stylesheet"</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"styles.css"</span>/></span>
<span class="hljs-tag"><<span class="hljs-name">script</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"myscript.js"</span> <span class="hljs-attr">async</span>></span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>
<span class="hljs-tag"><<span class="hljs-name">img</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"myimage.jpg"</span> <span class="hljs-attr">alt</span>=<span class="hljs-string">"image description"</span>/></span>
<span class="hljs-tag"><<span class="hljs-name">script</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"anotherscript.js"</span> <span class="hljs-attr">async</span>></span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-13">script的加载方式</h3>
<p>当解析到<code><script></code>标签的位置时，主线程会停止继续解析 HTML 文档，开始下载、执行脚本，直到脚本执行结束。换句话说，<strong><code><script></code>标签的下载、执行会阻塞 HTML 文档的解析</strong>。现在可以通过设置<code>async</code>和<code>defer</code>属性，保证浏览器下载脚本的同时继续解析 HTML 文档：</p>
<ul>
<li><code>async</code> 表示脚本下载完成后立即执行</li>
<li><code>defer</code>表示脚本下载完成并且文档解析完成后立即执行，执行完成后触发 <code>DOMContentLoaded</code> 事件</li>
<li>但<strong>两者都不能在执行脚本的同时解析文档</strong></li>
</ul>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/db43b2f270ca4e43ae59c02126b50083~tplv-k3u1fbpfcp-watermark.image" alt="284aec5bb7f16b3ef4e7482110c5ddbb_fix732.jpeg" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-14">rel="preload"</h3>
<p>通过给<code><link></code>标签设置<code>rel="preload"</code>属性，可以使得资源尽早的得到加载并可用，且更不易阻塞页面的初步渲染，进而提升性能。用<code>as</code>属性可以声明它的资源类型，比方说<code>script</code>、<code>style</code>、<code>audio</code>、<code>image</code>等。
MDN对于这方面的解释：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2Forphaned%2FWeb%2FHTML%2FPreloading_content" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/orphaned/Web/HTML/Preloading_content" ref="nofollow noopener noreferrer">developer.mozilla.org/zh-CN/docs/…</a></p>
<h2 data-id="heading-15">Step 2：计算样式</h2>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fda539450708428a92afa27691fb3fb9~tplv-k3u1fbpfcp-watermark.image" alt="computedstyle.png" loading="lazy" referrerpolicy="no-referrer">
主线程解析 CSS ，基于 CSS 选择器决定将哪种样式应用于哪个节点，计算每个 DOM 节点的样式，并与浏览器默认的 CSS 样式合并，生成 Style Rules。</p>
<h2 data-id="heading-16">Step 3：布局</h2>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0561e6ba3d934d1aa29f8842a904d7ad~tplv-k3u1fbpfcp-watermark.image" alt="layout.png" loading="lazy" referrerpolicy="no-referrer">
这一步骤的目的是根据 DOM 结构和 Style Rules ，计算出节点的几何信息。</p>
<p>主线程遍历 DOM 树和 Style Rules，生成 Layout Tree，这个 Layout Tree 包含了节点的x、y轴坐标和盒子大小等信息。</p>
<p>Layout Tree 的结构和 DOM Tree 很像，但它只包括页面上可见的节点。例如，Layout Tree 不包括<code>display: none</code>的节点，但包括<code>visibility: hidden</code>的节点，这两者 DOM Tree 都包含。那有没有 Layout Tree 包含，但 DOM Tree 不包含的节点呢？有，那就是<code>::after</code>、<code>::before</code>这种伪元素。</p>
<blockquote>
<p>确定页面的布局是一项具有挑战性的任务。即使是最简单的页面布局，比如从上到下的块流，也必须考虑字体有多大以及在哪里换行，因为这些会影响段落的大小和形状；这会影响下一段需要放在的位置。CSS 可以使元素浮动到一侧，屏蔽溢出项，并改变书写方向。可想而知，这个布局阶段任务艰巨。</p>
</blockquote>
<h2 data-id="heading-17">Step 4：绘制</h2>
<p>进入到绘制阶段，浏览器已经拥有了 DOM、Style Rules、Layout Tree，也就确定了节点的大小、形状、位置，现在需要根据以上数据确定绘制记录（Paint Records），即绘制它们的顺序。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c301b40300714d22b6310371e108b7eb~tplv-k3u1fbpfcp-watermark.image" alt="paint.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>如果是直接按照 HTML 标签顺序来绘制，那么对于某些设置了<code>z-index</code>属性的元素的安排很可能是错误的。</p>
<h3 data-id="heading-18">更新渲染流水线的成本很高</h3>
<p>渲染流水线中最重要的一点是，在每一步都使用前一操作的结果来创建新数据。例如，脚本修改了 DOM 结构，新增了一个节点，渲染流水线被启动，为 Layout Tree 和 Paint Records 中受影响的部分重新生成。
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/85a48906487542b281cb12f7e0b5bcd8~tplv-k3u1fbpfcp-watermark.image" alt="rendering pipeline.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-19">把脚本拆分成小块执行</h3>
<p>我们的大多数显示器每秒刷新屏幕 60 次 (60 fps)，浏览器的刷新频率一般与其匹配，因为就算超出屏幕的刷新频率也没什么实际意义。两次刷新之间称为一帧，如果你给元素设置了动画，保证在每一帧之间移动元素，那么从视觉上来看这个动画就显得非常流畅。</p>
<p>但如果在这个过程中执行了一段耗时较长的脚本将主线程阻塞了（页面渲染和脚本都由主线程执行），那么时间轴上的动画就<strong>丢帧</strong>了，视觉上看会比较卡顿。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/453ed401b46845e28d4685703bf95e91~tplv-k3u1fbpfcp-watermark.image" alt="pagejank2.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>为了保证页面流畅运行，建议把 JavaScript 脚本拆分成小块，并使用<code>requestAnimationFrame()</code>让脚本运行在每一帧之间。</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a1df4fe11adf45aa851485468338fb9d~tplv-k3u1fbpfcp-watermark.image" alt="raf.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>对于运算量特别大的一段脚本，尽量放在 Web Worker 中执行，避免抢占主线程资源。</p>
<h2 data-id="heading-20">Step 5：合成</h2>
<p>浏览器获得了文档结构，每个元素的样式、几何形状以及绘制顺序，最后把以上信息转化为屏幕上的像素，这一过程称为<strong>光栅化</strong>（rasterizing）。</p>
<p>Chrome 最初版本的光栅化方式是这样的，先光栅化当前视口部分，即当前可见部分；在页面滚动时，移动光栅框架，光栅化更多的内容补足视口内缺失的部分。可想而知，这种方式会在页面滚动时造成比较差的用户体验。
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ad156f7133694601aec38ccc81bde647~tplv-k3u1fbpfcp-zoom-1.image" alt="简单的光栅化" loading="lazy" referrerpolicy="no-referrer"></p>
<p>后面 Chrome 实现了一种更复杂、体验更好的光栅化方式，叫做<strong>合成</strong>（compositing）。合成是一种将页面的各个部分分成多个层、单独光栅化它们，并在合成器线程中合成为一个页面的技术。如果发生滚动，因为图层已经被光栅化，它所要做的就是合成一个新的帧。动画可以通过移动图层并合成新帧以相同的方式实现。你可以在 F12 的 Layers 面板查看页面是如何分层的。
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7081dcd9e93e44b7b6e0d90ad3450fc9~tplv-k3u1fbpfcp-zoom-1.image" alt="合成" loading="lazy" referrerpolicy="no-referrer"></p>
<p>有一些特定的属性和元素可以实例化一个层，包括<code><video></code>和<code><canvas></code>，还有一些CSS属性例如<code>opacity</code>、<code>transform</code>、<code>will-change</code>。</p>
<h3 data-id="heading-21">合成的具体步骤</h3>
<ol>
<li>为了找出哪些元素需要在哪些层中，主线程遍历 Layout Tree 以创建/更新 Layer Tree，将该信息提供给合成器线程</li>
<li>合成器线程会将一个大的图层分割成较小的图块，交由光栅线程</li>
<li>光栅线程对小图块进行光栅化，光栅化后的信息称为绘制四边形（draw quads），并将其存储在 GPU 内存中</li>
<li>合成器线程收集绘制四边形并创建一个合成帧</li>
<li>通过 IPC 将合成帧发送给浏览器进程，浏览器进程再将它发送给 GPU 以显示在屏幕上</li>
</ol>
<p>整个合成的过程还是挺绕的，搞出这么复杂的过程究竟为了什么？</p>
<h3 data-id="heading-22">合成的好处</h3>
<p>首先是把大型图层碎片化，交由多个光栅线程并行计算，在页面仅有部分重新渲染的情况下及其有用，因为这样渲染器进程就可以只对需要重新渲染的图块做光栅化，其他不变的图块从 GPU 内存中取用。</p>
<p>其次，合成这个过程是独立于主线程的。上面有提到过渲染流水线，它运行在主线程并且更新成本比较高，将合成过程独立出来有利于浏览器获得更流畅的性能。现在给元素通过animation修改某些 CSS 属性，例如<code>transform</code>、<code>opacity</code>，是可以被 GPU 加速的，不需要经过渲染流水线，直接步入合成步骤。</p>
<h1 data-id="heading-23">总结</h1>
<p>Chrome 线程间数据流：
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d625fc068f3f4f46968b670805d86259~tplv-k3u1fbpfcp-watermark.image" alt="浏览器线程间数据流.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>这篇文章介绍了 Chrome 浏览器在页面渲染时的具体工作。其中大量参考了官方文档，为了简单清晰地讲明这个过程我简化了一些步骤。有些地方如果讲的不明白可以留言告诉我，或者直接去看原文档。</p>
<h2 data-id="heading-24">参考链接</h2>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fdevelopers.google.com%2Fweb%2Fupdates%2F2018%2F09%2Finside-browser-part1" target="_blank" rel="nofollow noopener noreferrer" title="https://developers.google.com/web/updates/2018/09/inside-browser-part1" ref="nofollow noopener noreferrer">Inside look at modern web browser</a></p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FPerformance%2FHow_browsers_work" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/Performance/How_browsers_work" ref="nofollow noopener noreferrer">渲染页面：浏览器的工作原理</a></p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.html5rocks.com%2Fen%2Ftutorials%2Fspeed%2Fhigh-performance-animations%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/" ref="nofollow noopener noreferrer">High Performance Animations</a></p></div>  
</div>
            