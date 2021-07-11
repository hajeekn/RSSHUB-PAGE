
---
title: 'vue的生命周期-从出生到销毁的过程'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e06a5ec0d21f4907ba780ae03da4d548~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 01:00:46 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e06a5ec0d21f4907ba780ae03da4d548~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">一. Vue生命周期介绍</h2>
<blockquote>
<p>生命周期的含义： 从Vue实例创建，运行，到销毁期间，总是伴随着各种各样的事件，这些时间统称为生命周期</p>
</blockquote>
<p>常见叫法： 生命周期钩子 == 生命周期函数 == 生命周期事件</p>
<h2 data-id="heading-1">二、创建阶段</h2>
<ul>
<li>
<p>beforeCreate：实例在内存中创建出来，但未初始化 data和 methods</p>
</li>
<li>
<p>created： 实例已经在内存中创建完成，此时data和methods已初始化</p>
</li>
<li>
<p>beforeMount： 此时已经完成了模版的编译，只是还没有渲染到界面中去</p>
</li>
<li>
<p>mounted： 模版已经渲染到了浏览器，创建阶段结束，即将进入运行阶段（最新的dom）</p>
</li>
</ul>
<h2 data-id="heading-2">三、运行阶段</h2>
<ul>
<li>
<p>beforeUpadte：界面中的数据还是旧的，但是data数据已经更新，页面中和data不会保持同步</p>
</li>
<li>
<p>updated： 页面重新渲染完毕，页面中的数据和data保持一致</p>
</li>
</ul>
<h2 data-id="heading-3">三、销毁阶段</h2>
<ul>
<li>
<p>beforeDestroy：执行该方法的时候，Vue的生命周期已经进入销毁阶段，但是实例上的各种数据和方法还处于可用状态</p>
</li>
<li>
<p>destroyed： 组件已经全部销毁，Vue实例已经被销毁，Vue中的任何数据都不可用</p>
</li>
</ul>
<h2 data-id="heading-4">四、生命周期解析图</h2>
<pre><code class="copyable">这张图对官网的图做出更加详细地解释，我是在其他倔友那下载下来的，手机端可以保存。
vue生命周期非常重要，明白各阶段做了什么事情可以更好地进行项目开发。
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e06a5ec0d21f4907ba780ae03da4d548~tplv-k3u1fbpfcp-watermark.image" alt="4bc6539a019a48279716eb67f58e9bc.jpg" loading="lazy" referrerpolicy="no-referrer"></p></div>  
</div>
            