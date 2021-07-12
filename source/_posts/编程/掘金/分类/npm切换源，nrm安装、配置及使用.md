
---
title: 'npm切换源，nrm安装、配置及使用'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1d7426e0d9ee47e3ba155fd5bf2fcf07~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 17:18:11 GMT
thumbnail: 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1d7426e0d9ee47e3ba155fd5bf2fcf07~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>为什么要切换npm源</p>
<p>1.速度太慢</p>
<p>因为默认的npm源是国外的，速度比较慢。可以选择国内镜像，加快下载安装速度，比如我们可以切换到taobao源或者公司内部的源。</p>
<p>2.手动切换太麻烦</p>
<p>切换源时，往往记不住源链接，百度之后再来执行命令npm config set registry ....</p>
<p>切换npm源推荐使用nrm</p>
<p>nrm 是一个 js 模块，是一个命令行工具，可以用来快速切换 npm 源。</p>
<p>2.1 nrm安装方法</p>
<pre><code class="copyable">npm install -g nrm 
<span class="copy-code-btn">复制代码</span></code></pre>
<p>2.2 查看可选npm源</p>
<pre><code class="copyable">nrm ls
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1d7426e0d9ee47e3ba155fd5bf2fcf07~tplv-k3u1fbpfcp-watermark.image" alt="nrm_1.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>2.3 切换npm源</p>
<pre><code class="copyable">nrm use npm
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/10904130499e40e78ee8069c7def3533~tplv-k3u1fbpfcp-watermark.image" alt="nrm_2.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>2.4 增加npm源</p>
<pre><code class="copyable">nrm add hinpm https://registry.npm.taobao.org
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c99bdccb43a04ff69ddad9d0abcfd22b~tplv-k3u1fbpfcp-watermark.image" alt="nrm_3.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>2.5 删除npm源</p>
<pre><code class="copyable">nrm del hinpm
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2d3326e06614a60b2de16097ab22a56~tplv-k3u1fbpfcp-watermark.image" alt="nrm_4.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>2.6 测试npm源速度</p>
<pre><code class="copyable">nrm test
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dca49fbf7ad44d78b0c54d9faf02ba02~tplv-k3u1fbpfcp-watermark.image" alt="nrm_5.png" loading="lazy" referrerpolicy="no-referrer"></p></div>  
</div>
            