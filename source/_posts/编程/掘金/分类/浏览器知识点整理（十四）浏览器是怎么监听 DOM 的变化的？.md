
---
title: '浏览器知识点整理（十四）浏览器是怎么监听 DOM 的变化的？'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9076d679f0943898ce2a82a0f9c5ad1~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 17:40:58 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9076d679f0943898ce2a82a0f9c5ad1~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>@charset "UTF-8";.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:14px;overflow-x:hidden;color:#353535&#125;.markdown-body h1&#123;padding-bottom:4px;font-size:30px&#125;.markdown-body h1,.markdown-body h2&#123;margin-top:36px;margin-bottom:10px;line-height:1.5;color:#005bb7&#125;.markdown-body h2&#123;position:relative;padding-left:16px;padding-right:10px;padding-bottom:10px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h2:before&#123;content:"「";position:absolute;top:-6px;left:-10px&#125;.markdown-body h2:after&#123;content:"」";position:absolute;top:6px;right:auto&#125;.markdown-body h3&#123;position:relative;padding-bottom:0;margin-top:30px;margin-bottom:10px;font-size:20px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body h3:before&#123;content:"»";padding-right:6px;color:#2196f3&#125;.markdown-body h4&#123;margin-top:24px;font-size:16px&#125;.markdown-body h4,.markdown-body h5&#123;padding-bottom:0;margin-bottom:10px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body h5&#123;margin-top:18px;font-size:14px&#125;.markdown-body h6&#123;padding-bottom:0;margin-top:12px;margin-bottom:10px;font-size:12px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body p&#123;line-height:inherit;margin-top:16px;margin-bottom:16px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;position:relative;width:98%;height:1px;margin-top:32px;margin-bottom:32px;background-image:linear-gradient(90deg,#007fff,rgba(255,0,0,.3),hsla(0,0%,100%,.1),rgba(255,0,0,.3),#007fff);border-width:0;overflow:visible&#125;.markdown-body hr:after&#123;content:"";position:absolute;margin:auto;left:0;right:0;bottom:0;top:0;display:inline-block;width:60px;height:20px;background:#fff;background-image:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAgCAYAAABgrToAAAADoklEQVRYR82XTYgcRRTHf2933Q1RjAa9eFO8JHoJ8RQVBQ2iBwXBET0YEUTXNVmNQtTpmeqaWV0XNRq/o4KoECSCEPSg4CF+BYUkIIiCoCJCPIhC/Ihh2Z0nVV27VnZnenumW9i6ddV7//frV69fVQurfMgq56NawFTPAU6QyomqXrw6wIZeyhCPebA5buNR+akKyGoAjd6BshthnYdSjqNcRVuOlIUsD2j0SuA94IwuMHdh5ZUykOUBXfSGbmKI54EtAeYIHSZoy5dl4JxvNYBOKdW1KE8BQ8AkVk6WhasWsAiN0TX9gveXQaPP+Aytpc4u+bMI06JNohsYYYYOR2lJWtS3OKDRfcAtQfgDoI6Vo4UCGb0OmAEuDvZvYmVbEd/igC3dzDz7gQu8sPA9kJDK27mBmjqBeLjTg90PDFOjWawFFQd06kZHEfaj3LAIpTRpSXsZ5E06zEYP9sDimnAApYaV2SLZG/wjMeqAkijwW4xQJ5Gf/ZzRC8OW3hiBTGGlURRswW55Bh/Ssxljrwew8l1PQaM14GngvGDzBUKdDsMeTtgU5o8B92PFlUf3YXUrHa7Fys6lBqcCGnX15YQ2A18FyPd7Crd1A3M8C1wdbH4DD3hWeP6IEXbQkG97ajR1HPFnuPP5jFFq1OWX7hl8WM9l1AO648uNfwLk7tytMeogty+xeQ4rO3r6bdcx1nuwOGsHmaXGtPzae4uzGnLH1kQkvpdZGrHjssBZJrL+pqS05KWc8tgITAPXRzYvYOXe/C2OV43eDcRBDtIhoS2f9wzc0Cv8Wls+zoFzUC5zF0U241h5uZtPfptp6OUM8wbK+cH5GEpCS17P3fJei0Z3+npTxryJ8CPzbKMtn/ZyWbkPGl0PuFPkmkjkcb4h4R2ZLwRq1H0ALmvjkf2HwK1Y+T1PY2XABe/sHJ6MxN5lnoSpnC/UGbsTaI5phK2R7x6s3Ffk5YoDOrWm3onwJHBmEP86bPmBrsGaenNoIdnxCH+gPEhLXi0Cl1VBvyPVLSh7gEuC62yAfOIUqabWEaaiucMIk6RyqJ+Q/QM69V26jjW86Gvov/EaoyT8zRCn+Xq7PVrbx0nuYUaO9wM3WAbjCE1NEUw09Um4UV+2OKfYfu5/S19gsAzGKqm6LE5FrShbdS0ku465DjDwKA/oQht19ejqbaEVuRbiLhuHByYLjtUAZpDutzP7cYdHsPJXWbjyNVgFwQoa1WXwf4Jd9YD/Ap80+yE7+u9aAAAAAElFTkSuQmCC);background-repeat:no-repeat;background-size:auto 100%;background-position-x:center&#125;.markdown-body code&#123;padding:.065em .4em;font-size:.87em;color:#c2185b;word-break:break-word;overflow-x:auto;background-color:#fff4f4;border-radius:2px&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;display:block;padding:16px 12px;margin:0;font-size:12px;color:#333;word-break:normal;overflow-x:auto;background:#f8f8f8&#125;.markdown-body pre>code::-webkit-scrollbar&#123;width:4px;height:4px&#125;.markdown-body pre>code::-webkit-scrollbar-track&#123;background-color:#bedcff&#125;.markdown-body pre>code::-webkit-scrollbar-thumb&#123;background-color:#2196f3;border-radius:10px&#125;.markdown-body a&#123;position:relative;text-decoration:none;color:#3da8f5;border-bottom:1px solid #bedcff&#125;.markdown-body a:hover&#123;color:#007fff;border-bottom-color:#007fff&#125;.markdown-body a:active&#123;color:#007fff&#125;.markdown-body a:after&#123;position:absolute;content:"";top:100%;left:0;width:100%;opacity:0;border-bottom:1px solid #bedcff;transition:top .3s,opacity .3s;transform:translateZ(0)&#125;.markdown-body a:hover:after&#123;top:0;opacity:1;border-bottom-color:#007fff&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #c3e0fd;border-spacing:0;border-collapse:collapse&#125;.markdown-body table thead&#123;color:#000;text-align:left;font-size:14px;background:#f6f6f6&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f7fbff&#125;.markdown-body table tr:hover&#123;background-color:#e0edf7&#125;.markdown-body table td,.markdown-body table th&#123;padding:12px 8px;line-height:24px;border:1px solid #c3e0fd&#125;.markdown-body table th&#123;color:#005bb7;background-color:#dff0ff&#125;.markdown-body table td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#8c8c8c;border-left:4px solid #2196f3;background-color:#f0fdff;padding:1px 20px;margin:22px 0&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body b,.markdown-body blockquote>b,.markdown-body blockquote>strong,.markdown-body strong&#123;color:#2196f3&#125;.markdown-body em,.markdown-body i&#123;color:#4fc3f7&#125;.markdown-body del&#123;color:#ccc&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:4px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body details>summary&#123;outline:none;color:#005bb7;font-size:20px;font-weight:bolder;border-bottom:1px solid #bedcff;cursor:pointer&#125;.markdown-body details>p&#123;padding:10px 20px;margin:10px 0 0;color:#666;background-color:#f0fdff;border:2px dashed #2196f3&#125;.markdown-body h1::selection,.markdown-body h2::selection,.markdown-body h3::selection,.markdown-body h4::selection,.markdown-body h5::selection,.markdown-body h6::selection&#123;color:#005bb7;background-color:rgba(160,200,255,.15)&#125;.markdown-body p::selection&#123;color:#c80000&#125;.markdown-body a::selection,.markdown-body b::selection,.markdown-body del::selection,.markdown-body em::selection,.markdown-body i::selection,.markdown-body strong::selection&#123;background-color:transparent&#125;.markdown-body code::selection&#123;background-color:#ffeaeb&#125;.markdown-body pre>code::selection&#123;background-color:rgba(160,200,255,.25)&#125;.markdown-body ol ::selection,.markdown-body ul ::selection&#123;background-color:rgba(160,200,255,.15)&#125;.markdown-body .contains-task-list&#123;padding-left:14px;list-style:none&#125;.markdown-body .contains-task-list input[type=checkbox]&#123;position:relative&#125;.markdown-body .contains-task-list input[type=checkbox]:before&#123;content:"";position:absolute;top:0;left:0;right:0;bottom:0;width:inherit;height:inherit;background:#f0f8ff;border:1px solid #add6ff;border-radius:2px;box-sizing:border-box;z-index:1&#125;.markdown-body .contains-task-list input[type=checkbox]:checked:after&#123;content:"✓";position:absolute;top:-12px;left:0;right:0;bottom:0;width:0;height:0;color:#f55;font-size:20px;font-weight:700;z-index:2&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><blockquote>
<p>本文已参与好文召集令活动，点击查看：<a href="https://juejin.cn/post/6978685539985653767" target="_blank" title="https://juejin.cn/post/6978685539985653767">后端、大前端双赛道投稿，2万元奖池等你挑战！</a></p>
</blockquote>
<h3 data-id="heading-0">前言</h3>
<p>浏览器通过事件循环机制使页面“活”起来，在事件循环中宏任务和微任务有不同的执行时机，而浏览器基于微任务的技术有 <code>MutationObserver</code>、<code>Promise</code> 以及以 <code>Promise</code> 为基础开发出来的很多其他的技术。</p>
<p>前面的文章也花了很大的篇幅介绍 <code>Promise</code>，那么这篇文章就带大家了解一下 <code>MutationObserver</code> 这个微任务是什么？用来做什么的吧！</p>
<p><strong><code>MutationObserver</code> 是用来监听 DOM 变化的一套方法</strong>，而监听 DOM 变化一直是前端工程师一项非常核心的需求。比如很多 Web 应用都利用 HTML 与 JavaScript 构建其自定义控件，与一些内置控件不同，这些控件不是固有的。为了与内置控件一起良好地工作，这些控件必须能够适应内容更改、响应事件和用户交互。因此，<strong>Web 应用需要监视 DOM 变化并及时地做出响应</strong>。</p>
<p><code>MutationObserver</code> 是现在监听 DOM 变化的方法，那么在开始的时候是怎么监听的呢，了解监听 DOM 方法的演变有助于我们更加深入地理解浏览器是怎样运行的。</p>
<h3 data-id="heading-1">早期轮询检测</h3>
<p>在早期，浏览器并没有提供对监听 DOM 的支持，所以那个时候要观察 DOM 是否变化，唯一能做的便是 <strong>轮询检测</strong>，比如使用 <code>setTimeout</code> 或者 <code>setInterval</code> 来定时检测 DOM 是否有改变。</p>
<p>这种方式简单粗暴，但是会遇到两个问题：</p>
<ul>
<li>如果时间间隔设置过长，DOM 变化 <strong>响应不够及时</strong>；</li>
<li>反过来如果时间间隔设置过短，又会 <strong>浪费很多无用的工作量</strong> 去检查 DOM，会让页面变得低效。</li>
</ul>
<h3 data-id="heading-2">Mutation Event</h3>
<p>在 2000 年的时候引入了 <code>Mutation Event</code>，它是在 DOM3 中定义的用于监听 DOM 树结构变化的事件，不过由于该事件存在兼容性以及性能上的问题已经被弃用。</p>
<p><code>Mutation Event</code> 总共有7种事件：<code>DOMNodeInserted</code>、<code>DOMNodeRemoved</code>、<code>DOMSubtreeModified</code>、<code>DOMAttrModified</code>、<code>DOMCharacterDataModified</code>、<code>DOMNodeInsertedIntoDocument</code> 和<code>DOMNodeRemovedFromDocument</code>。</p>
<p>简单用法如下：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">let</span> box = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'box'</span>)
box.addEventListener(<span class="hljs-string">"DOMSubtreeModified"</span>, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'box 元素被修改'</span>);
&#125;, <span class="hljs-literal">false</span>);
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>Mutation Event</code> 采用了 <strong>观察者的设计模式</strong>，当 DOM 有变动时就会立刻触发相应的事件，这种方式属于 <strong>同步回调</strong>。</p>
<p>采用 <code>Mutation Event</code> 解决了 <strong>实时性</strong> 的问题，因为 DOM 一旦发生变化，就会立即调用 JavaScript 接口。但是 <strong>这种实时性造成了严重的性能问题</strong>，因为每次 DOM 变动，渲染引擎都会去调用 JS，这样会产生较大的性能开销。</p>
<p>比如利用 JS 动态创建或动态修改 <code>50</code> 个节点内容，就会触发 <code>50</code> 次回调，而且每个回调函数都需要一定的执行时间，这里我们假设每次回调的执行时间是 <code>4ms</code> ，那么 <code>50</code> 次回调的执行时间就是 <code>200ms</code>，若此时浏览器正在执行一个动画效果，由于 <code>Mutation Event</code> 触发回调事件，就会导致动画的卡顿。</p>
<p>也正是因为使用 <code>Mutation Event</code> 会导致页面性能问题，所以 <code>Mutation Event</code> 被反对使用，并逐步从 Web 标准事件中删除了。</p>
<h3 data-id="heading-3">MutationObserver</h3>
<p><code>MutationObserver</code> API 可以用来监视 DOM 的变化，包括属性的变化、节点的增减、内容的变化等。</p>
<h4 data-id="heading-4"><code>MutationObserver</code> 的使用</h4>
<p>参考 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FAPI%2FMutationObserver" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/API/MutationObserver" ref="nofollow noopener noreferrer"><code>MutationObserver</code> 的 MDN 官方文档资料</a></p>
<p><code>MutationObserver</code> 是一个构造器，用来实例化一个 <code>Mutation</code> 观察者对象，参数是一个回调函数，这个回调函数会在指定的 DOM 节点发送变化后执行，回调函数有两个参数：</p>
<ul>
<li><code>mutations</code>：节点变化记录数组（<code>MutationRecord</code>）</li>
<li><code>observer</code>：观察者对象本身</li>
</ul>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">let</span> observe = <span class="hljs-keyword">new</span> MutationObserver(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">mutations, observer</span>) </span>&#123;&#125;);
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>MutationObserver</code> 实例对象有三个方法，如下：</p>
<ul>
<li><code>observe</code>：配置 <code>MutationObserver</code> 在 DOM 更改匹配给定选项时，通过其回调函数开始接收通知。即设置观察目标，接受两个参数：
<ul>
<li><code>target</code>：观察目标；</li>
<li><code>options</code>：通过对象成员来设置观察选项</li>
</ul>
</li>
<li><code>disconnect</code>：阻止 <code>MutationObserver</code> 实例继续接收的通知，直到再次调用其 <code>observe()</code> 方法，该观察者对象包含的回调函数都不会再被调用。</li>
<li><code>takeRecords</code>：从 <code>MutationObserver</code> 的通知队列中删除所有待处理的通知，并将它们返回到<code>MutationRecord</code> 对象的新 <code>Array</code> 中。即清空记录队列并返回里面的内容。</li>
</ul>
<p>使用实例：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// 选择需要观察变动的节点</span>
<span class="hljs-keyword">const</span> targetNode = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'box'</span>);
<span class="hljs-comment">// 观察器的配置（需要观察什么变动）</span>
<span class="hljs-keyword">const</span> config = &#123;
  <span class="hljs-attr">attributes</span>: <span class="hljs-literal">true</span>,
  <span class="hljs-attr">childList</span>: <span class="hljs-literal">true</span>,
  <span class="hljs-attr">subtree</span>: <span class="hljs-literal">true</span>
&#125;;
<span class="hljs-comment">// 当观察到变动时执行的回调函数</span>
<span class="hljs-keyword">const</span> callback = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">mutationsList, observer</span>) </span>&#123;
  <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> mutation <span class="hljs-keyword">of</span> mutationsList) &#123;
    <span class="hljs-keyword">if</span> (mutation.type === <span class="hljs-string">'childList'</span>) &#123;
      <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'有节点发生改变，当前节点的内容是：'</span> + mutation.target.innerHTML);
    &#125; <span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> (mutation.type === <span class="hljs-string">'attributes'</span>) &#123;
      <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'修改了'</span> + mutation.attributeName + <span class="hljs-string">'属性'</span>);
    &#125;
  &#125;
&#125;;
<span class="hljs-comment">// 创建一个观察器实例并传入回调函数</span>
<span class="hljs-keyword">const</span> observer = <span class="hljs-keyword">new</span> MutationObserver(callback);
<span class="hljs-comment">// 以上述配置开始观察目标节点</span>
observer.observe(targetNode, config);
<span class="hljs-comment">// 之后，可停止观察</span>
<span class="hljs-comment">// observer.disconnect();</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-5"><code>MutationObserver</code> 的改进优化</h4>
<ul>
<li>首先，<strong><code>MutationObserver</code> 将响应函数改成异步调用</strong>，可以不用在每次 DOM 变化都触发异步调用，而是等多次 DOM 变化后，一次触发异步调用，并且还会使用一个数据结构来记录这期间所有的 DOM 变化。这样即使频繁地操纵 DOM，也不会对性能造成太大的影响。</li>
<li>在每次 DOM 节点发生变化的时候，<strong>渲染引擎将变化记录封装成微任务</strong>，并将微任务添加进当前的微任务队列中。这样当执行到检查点的时候，V8 引擎就会按照顺序执行微任务。</li>
</ul>
<p>综上所述，<code>MutationObserver</code> 采用了 <strong>异步 + 微任务</strong> 的策略来实现监听 DOM 的变化。</p>
<ul>
<li><strong>通过异步操作解决了同步操作的性能问题</strong>；</li>
<li><strong>通过微任务解决了实时性的问题</strong>。</li>
</ul>
<h4 data-id="heading-6"><code>MutationObserver</code> 和 Vue 中的 <code>nextTick</code></h4>
<p>Vue 中 <code>nextTick</code> 可以让我们在下次 DOM 更新循环结束之后执行延迟回调，用于获得更新后的 DOM。</p>
<p>那在 Vue 中是怎么实现 <code>nextTick</code> 的呢？</p>
<p><strong>Vue 在更新 DOM 时是异步执行的</strong>。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 <code>watcher</code> 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。</p>
<p>而异步回调我们知道有宏任务（<code>macrotasks</code>）和微任务（<code>microtasks</code>）两种，那为了让 <code>nextTick</code> 更快的执行，那肯定是优先选择微任务（<code>microtasks</code>）的。要创建一个新的微任务（<code>microtask</code>），会优先使用 <code>Promise</code>，如果浏览器不支持，再尝试 <code>MutationObserver</code>。实在不支持，就只能用 <code>setTimeout</code> 这个宏任务了。</p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fcn.vuejs.org%2Fv2%2Fguide%2Freactivity.html%23%25E5%25BC%2582%25E6%25AD%25A5%25E6%259B%25B4%25E6%2596%25B0%25E9%2598%259F%25E5%2588%2597" target="_blank" rel="nofollow noopener noreferrer" title="https://cn.vuejs.org/v2/guide/reactivity.html#%E5%BC%82%E6%AD%A5%E6%9B%B4%E6%96%B0%E9%98%9F%E5%88%97" ref="nofollow noopener noreferrer">Vue 中的异步更新队列</a> 是这样说的：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9076d679f0943898ce2a82a0f9c5ad1~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>至于 <code>MutationObserver</code> 是怎么模拟 <code>nextTick</code> 的，可以看 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fvuejs%2Fvue%2Fblob%2F9cfd63a7d08c1eba029c8bd7463b3047c3347826%2Fsrc%2Fcore%2Futil%2Fenv.js%23L86-L95" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/vuejs/vue/blob/9cfd63a7d08c1eba029c8bd7463b3047c3347826/src/core/util/env.js#L86-L95" ref="nofollow noopener noreferrer">源码</a>，其实就是创建一个 <code>TextNode</code> 并监听内容变化，然后要 <code>nextTick</code> 的时候去改一下这个节点的文本内容：</p>
<pre><code class="hljs language-js copyable" lang="js">    <span class="hljs-keyword">var</span> counter = <span class="hljs-number">1</span>
    <span class="hljs-keyword">var</span> observer = <span class="hljs-keyword">new</span> MutationObserver(nextTickHandler)
    <span class="hljs-keyword">var</span> textNode = <span class="hljs-built_in">document</span>.createTextNode(<span class="hljs-built_in">String</span>(counter))
    observer.observe(textNode, &#123;
      <span class="hljs-attr">characterData</span>: <span class="hljs-literal">true</span>
    &#125;)
    timerFunc = <span class="hljs-function">() =></span> &#123;
      counter = (counter + <span class="hljs-number">1</span>) % <span class="hljs-number">2</span>
      textNode.data = <span class="hljs-built_in">String</span>(counter)
    &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-7">总结</h3>
<p>这篇文章介绍了监听 DOM 变化技术方案的演化史，从轮询到 <code>Mutation Event</code> 再到最新使用的 <code>MutationObserver</code>。<strong><code>MutationObserver</code> 方案的核心就是采用微任务机制，有效地权衡了实时性和执行效率的问题</strong>。</p>
<p>最后还简单介绍了 <code>MutationObserver</code> 和 Vue 中 <code>nextTick</code> 的关系。</p></div>  
</div>
            