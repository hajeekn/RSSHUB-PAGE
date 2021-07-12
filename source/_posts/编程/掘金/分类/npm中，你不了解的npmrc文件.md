
---
title: 'npm中，你不了解的.npmrc文件'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=7423'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 20:38:25 GMT
thumbnail: 'https://picsum.photos/400/300?random=7423'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">写在前面</h3>
<p>对于写JS的程序员来说，可能没有人不知道npm，但是有些同学对他的配置文件(即.npmrc文件)并不了解。结合我的学习心得，写一篇博客跟大家分享一些该配置文件的知识。</p>
<h3 data-id="heading-1">.npmrc的作用</h3>
<p>.npmrc，可以理解成npm running cnfiguration, 即npm运行时配置文件。我们知道，npm最大的作用就是帮助开发者安装需要的依赖包，但是要从哪里下载？下载哪一个版本的包，把包下载到电脑的哪个路径下？</p>
<p>这些都可以在.npmrc中进行配置。</p>
<p>在设置.npmrc之前，我们需要知道：在你的电脑上，不止存在一个.npmrc文件，而是有多个。在我们安装包的时候，npm按照如下顺序读取这些配置文件：</p>
<ol>
<li>项目配置文件：你可以在项目的根目录下创建一个.npmrc文件，只用于管理这个项目的npm安装。</li>
<li>用户配置文件：在你使用一个账号登陆的电脑的时候，可以为当前用户创建一个.npmrc文件，之后用该用户登录电脑，就可以使用该配置文件。可以通过 <strong>npm config get userconfig</strong> 来获取该文件的位置。</li>
<li>全局配置文件： 一台电脑可能有多个用户，在这些用户之上，你可以设置一个公共的.npmrc文件，供所有用户使用。该文件的路径为：<strong>$PREFIX/etc/npmrc</strong>，使用 <strong>npm config get prefix</strong> 获取$PREFIX。如果你不曾配置过全局文件，该文件不存在。</li>
<li>npm内嵌配置文件：最后还有npm内置配置文件，基本上用不到，不用过度关注。</li>
</ol>
<h3 data-id="heading-2">如何设置.npmrc</h3>
<h4 data-id="heading-3">1. <strong>设置项目配置文件</strong></h4>
<p>在项目的根目录下新建 .npmrc 文件，在里面以 <strong>key=value</strong> 的格式进行配置。比如要把npm的源配置为淘宝源，可以参考一下代码：</p>
<pre><code class="hljs language-bash copyable" lang="bash">registry=https://registry.npm.taobao.org
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如果你想删除一些配置，可以直接把对应的代码行给删除。</p>
<h4 data-id="heading-4">2. <strong>设置用户配置文件</strong></h4>
<p>你可以直接通过 <strong>npm config get userconfig</strong> 命令找到该文件的路径，然后直接仿照上述方法该文件，也可以通过 <strong>npm config set  </strong> 命令继续设置，命令如下：</p>
<pre><code class="hljs language-bash copyable" lang="bash">config <span class="hljs-built_in">set</span> registry https://registry.npm.taobao.org
<span class="copy-code-btn">复制代码</span></code></pre>
<p>最终，命令行会帮助我们修改对应的配置文件。只不过使用命令行更加快捷。</p>
<p>如果想要删除一些配置，可以直接编辑.npmrc文件，也可以使用命令进行删除，比如：</p>
<pre><code class="hljs language-bash copyable" lang="bash">npm config delete registry
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-5">3. <strong>设置全局配置文件</strong></h4>
<p>方法和设置用户配置文件如出一辙，只不过在使用命令行时需要加上 <strong>-g</strong> 参数。</p>
<pre><code class="hljs language-bash copyable" lang="bash">npm config <span class="hljs-built_in">set</span> registry https://registry.npm.taobao.org -g
<span class="copy-code-btn">复制代码</span></code></pre>
<p>除此之外，这里列出一些常用的npm设置命令，有兴趣的话，可以了解一下，挺好玩的：</p>
<pre><code class="hljs language-bash copyable" lang="bash">npm config <span class="hljs-built_in">set</span> <key> <value> [-g|--global]  //给配置参数key设置值为value；
npm config get <key>          //获取配置参数key的值；
npm config delete <key>       //删除置参数key及其值；
npm config list [-l]      //显示npm的所有配置参数的信息；
npm config edit     //编辑配置文件
npm get <key>     //获取配置参数key的值；
npm <span class="hljs-built_in">set</span> <key> <value> [-g|--global]    //给配置参数key设置值为value；
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-6">写在最后</h3>
<p>以上就是关于.npmrc的一些常识，其实你在开发过程中，很少会继续配置该文件。不过在你安装依赖包出错的时候，可以思考一下：是不是npm的配置参数有问题，这样就多一种解决问题的思路了。</p>
<p>比如这篇博客中的内容：</p>
<p>node-sass 安装失败的解决办法： <a href="https://juejin.cn/post/6982169952325222414" target="_blank" title="https://juejin.cn/post/6982169952325222414">juejin.cn/post/698216…</a></p></div>  
</div>
            