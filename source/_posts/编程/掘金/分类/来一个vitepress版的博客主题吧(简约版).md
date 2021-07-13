
---
title: '来一个vitepress版的博客主题吧(简约版)'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0e4e3a1491344c0838cb782fc57604d~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 05:37:30 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0e4e3a1491344c0838cb782fc57604d~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>本主题基于 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fvitepress.vuejs.org%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://vitepress.vuejs.org/" ref="nofollow noopener noreferrer">vitepress</a> 最新版的0.15.6开发</p>
<p>补个侧边栏</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0e4e3a1491344c0838cb782fc57604d~tplv-k3u1fbpfcp-watermark.image" alt="WechatIMG149.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Ffangying.dev" target="_blank" rel="nofollow noopener noreferrer" title="https://fangying.dev" ref="nofollow noopener noreferrer">live demo</a><br>
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fairene%2Fvitepress-blog-pure" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/airene/vitepress-blog-pure" ref="nofollow noopener noreferrer">github repo</a></p>
<h3 data-id="heading-0">已经实现的功能：</h3>
<ul>
<li>按年归档功能</li>
<li>标签功能</li>
<li>不是很优雅的分页功能</li>
<li>非常不优雅但是没办法的评论功能(基于<a href="https://link.juejin.cn/?target=https%3A%2F%2Futteranc.es%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://utteranc.es/" ref="nofollow noopener noreferrer">utteranc.es</a>)</li>
<li><strong>不出意外的话，应该会一直follow <a href="https://link.juejin.cn/?target=https%3A%2F%2Fvitepress.vuejs.org%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://vitepress.vuejs.org/" ref="nofollow noopener noreferrer">vitepress</a> 的版本</strong></li>
</ul>
<h3 data-id="heading-1">动机：</h3>
<p>直想找一个架构足够干净(小、轻量)的ssg程序，hexo,hugo,vuepress,docsify等都试了，总有不满意的地方，包括这些程序的主题也没有直接满意的（编程语言不熟悉的、功能太多，<strong>生成的html的文件还有不少插件的残留</strong>）。</p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fvitepress.vuejs.org%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://vitepress.vuejs.org/" ref="nofollow noopener noreferrer">vitepress</a> 足够轻量，系统干净，启动贼拉快，博客主题这块还没成熟的，所以自己动手做一个满意的博客主题吧，诉求就是功能可以少，但要足够的轻量。</p>
<h3 data-id="heading-2">核心实现思路</h3>
<p>不动官方的默认主题，能继承最好，方便跟着 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fvitepress.vuejs.org%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://vitepress.vuejs.org/" ref="nofollow noopener noreferrer">vitepress</a> 的快速升级，同时还能直接拥有官方皮肤的功能<br>
<strong>重要的事情说三遍！！！除了以学习为目的，其他时候其实折腾远没有沉淀重要，坚持看坚持写，比用什么系统更重要</strong></p>
<h2 data-id="heading-3">使用方法</h2>
<p><strong>貌似目前vitepress主题机制还不成熟，可能是因为没到正式版，先用<code>copy</code>的方式使用</strong></p>
<p>1.复制一下文件到你的项目根目录
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fairene%2Fvitepress-blog-pure" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/airene/vitepress-blog-pure" ref="nofollow noopener noreferrer">下载地址</a></p>
<pre><code class="copyable">├── .vitepress  
├── pages  
│   ├── about.md  
│   ├── archives.md  
│   └── tags.md  
├── posts            //存放博客文章  
├── public           //[可选]    
    └── favicon.ico  
<span class="copy-code-btn">复制代码</span></code></pre>
<p>2.新建一个package.json文件,执行 npm i,包信息自己看着调整</p>
<pre><code class="hljs language-json copyable" lang="json">&#123;
    <span class="hljs-attr">"name"</span>: <span class="hljs-string">"vitepress-blog-pure"</span>,
    <span class="hljs-attr">"version"</span>: <span class="hljs-string">"1.0.0"</span>,
    <span class="hljs-attr">"description"</span>: <span class="hljs-string">""</span>,
    <span class="hljs-attr">"main"</span>: <span class="hljs-string">"index.js"</span>,
    <span class="hljs-attr">"scripts"</span>: &#123;
        <span class="hljs-attr">"dev"</span>: <span class="hljs-string">"vitepress dev --host 0.0.0.0"</span>,
        <span class="hljs-attr">"build"</span>: <span class="hljs-string">"vitepress build"</span>,
        <span class="hljs-attr">"serve"</span>: <span class="hljs-string">"vitepress serve"</span>
    &#125;,
    <span class="hljs-attr">"keywords"</span>: [],
    <span class="hljs-attr">"author"</span>: <span class="hljs-string">""</span>,
    <span class="hljs-attr">"license"</span>: <span class="hljs-string">"ISC"</span>,
    <span class="hljs-attr">"devDependencies"</span>: &#123;
        <span class="hljs-attr">"vitepress"</span>: <span class="hljs-string">"^0.15.6"</span>,
        <span class="hljs-attr">"globby"</span>: <span class="hljs-string">"^11.0.4"</span>,
        <span class="hljs-attr">"gray-matter"</span>: <span class="hljs-string">"^4.0.3"</span>,
        <span class="hljs-attr">"fs-extra"</span>: <span class="hljs-string">"^10.0.0"</span>
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>3.执行 <code>npm run dev</code> 即可查看效果, 其他工具随意pnpm,yarn</p>
<p><strong>ps. 写文章的格式和位置</strong><br>
推荐放到posts目录中(脚本有关联)，格式：</p>
<pre><code class="hljs language-markdown copyable" lang="markdown">---
date: 2021-06-30
title: .zsh<span class="hljs-emphasis">_history历史记录优化
description: 历史重复的命令太多了，不用grep都不太好找
tags:
- macOS
---
#标题
正文
</span><span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-4">感谢</h2>
<p>看到这一篇文章带来的灵感 - <a href="https://juejin.cn/post/6896382276389732359" target="_blank" title="https://juejin.cn/post/6896382276389732359">VitePress极简博客搭建</a></p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2FMoking1997" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/Moking1997" ref="nofollow noopener noreferrer">Moking1997</a> 开发的比较早，vitepress的版本还是0.7.x,现在已经0.15.x了，变化还是挺大的，已经不太能通过提pr的方式维护了。<br>
主要的变化是适配vitepress的新版本，主题这块采用的实现思路不一样，并不改动官方默认主题，这样可以实现极少的代码量和为将来能发布成npm主题包的做准备。</p>
<p>比如：<br>
sidebar使用hackcss的方式实现想要的效果</p></div>  
</div>
            