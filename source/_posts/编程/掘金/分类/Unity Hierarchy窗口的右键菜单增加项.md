
---
title: 'Unity Hierarchy窗口的右键菜单增加项'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/67116387266c4fac9d0deb6cbe84e31f~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 05:13:51 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/67116387266c4fac9d0deb6cbe84e31f~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">目的</h2>
<p>实现在Hierarchy窗口的右键菜单增加项，来快速实现一些功能，比如：自定义的UI创建等等。参照uGUI源码发现并不能添加成功：</p>
<pre><code class="hljs language-csharp copyable" lang="csharp">        [<span class="hljs-meta">MenuItem(<span class="hljs-meta-string">"GameObject/UI/Text"</span>, false, 2000)</span>]
        <span class="hljs-function"><span class="hljs-keyword">static</span> <span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">AddText</span>(<span class="hljs-params">MenuCommand menuCommand</span>)</span>
        &#123;
            GameObject go = DefaultControls.CreateText(GetStandardResources());
            PlaceUIElementRoot(go, menuCommand);
        &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-1">原因</h2>
<p>按照API手册，发现需要将优先级改成10，但是只能设置10的话，是没办法达到想要的顺序是在UI之下，而不是更下面。之后发现有人搜索总结如下：</p>
<p>标题菜单栏优先级：
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/67116387266c4fac9d0deb6cbe84e31f~tplv-k3u1fbpfcp-zoom-1.image" alt loading="lazy" referrerpolicy="no-referrer">
右键菜单优先级：
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b2b7bed565a44b7cafeb277b7c304559~tplv-k3u1fbpfcp-zoom-1.image" alt loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-2">参考</h2>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fanswers.unity.com%2Fquestions%2F22947%2Fadding-to-the-context-menu-of-the-hierarchy-tab.html" target="_blank" rel="nofollow noopener noreferrer" title="https://answers.unity.com/questions/22947/adding-to-the-context-menu-of-the-hierarchy-tab.html" ref="nofollow noopener noreferrer">answers.unity.com/questions/2…</a></p></div>  
</div>
            