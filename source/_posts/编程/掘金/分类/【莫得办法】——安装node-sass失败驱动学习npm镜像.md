
---
title: '【莫得办法】——安装node-sass失败驱动学习npm镜像'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/274c9c2e0bbb44bb9cd32fba45a8ea28~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Sat, 17 Jul 2021 01:36:20 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/274c9c2e0bbb44bb9cd32fba45a8ea28~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">前言</h2>
<p>不知道大家在接触一个新项目时是怎么去快速理解其中的业务的,我的方式就是先让它可以运行。运行起来的后面是事情才有的谈。</p>
<p>启动项目第一步</p>
<pre><code class="copyable">npm install
<span class="copy-code-btn">复制代码</span></code></pre>
<p>可就在今天,它失败了,本想着快速在谷歌上搜索一下解决方案就完事了没想到自己一步步陷入了一个深不见底的巨坑。</p>
<p>就在今天，我在拉取公司项目之后准确下载相关依赖时,控制台给我报了这样一个错
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/274c9c2e0bbb44bb9cd32fba45a8ea28~tplv-k3u1fbpfcp-zoom-1.image" alt loading="lazy" referrerpolicy="no-referrer">
然后我切换源之后又报了这个错</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d765949a0869422db544c6380c2eaf87~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>然后我带着错误信息到百度谷歌去搜索时发现了和我一样的大量受害者,他们也给出了许多回答,可是大部分回答知识浅尝辄止,既不说出现错误原因,也不谈解决方案的原理。</p>
<p>在翻阅大量文章之后,终于让我找到了一篇系统的相对具有说服力的文章来解决安装node-saa失败这个问题。
链接我会放在文章末尾。</p>
<h2 data-id="heading-1">一.是否是因为没有切换源而导致的?</h2>
<p>众说周知,因为国内网络环境的因素,当我们使用npm去下载一些包的时候,往往会出现下载过慢甚至下载失败的情况。因此有些经验的程序员会在安装完Node之后立马切换npm的镜像,比如切换成淘宝源。</p>
<pre><code class="copyable">npm config set registry https://registry.npm.taobao.org/
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这样我们可以使用npm下载包的时候大幅度速度从而避免下载失败。</p>
<p>这是我刚开始以为下载失败的原因,所以我立马切换成了淘宝源,可是事情没那么简单。切换成淘宝源之后,之前的错误消失了,可有出现了新的错误。</p>
<h2 data-id="heading-2">二.切换源没错,错的是依赖包</h2>
<p>显然,在切换源之后,下载速度提高了,可是安装的模块如果有依赖c++模块的,安装过程中会隐式的安装node-gyp,node-gyp用来编译这些依赖c++模块的模块。</p>
<p>这还不要紧,致命的是<code>node-gyp</code>在首次编译时会依赖<code>Node源码</code>，所以又悄悄去下载<code>Node</code>。虽然在前面已设置了<code>淘宝镜像</code>，但是在这里一点卵用都没有。这样又因为国内网络环境的原因，再次遇上<code>安装过慢</code>或<code>安装失败</code>的情况。</p>
<p>王德发?太搞人心态了吧。</p>
<p>还好<code>npm config</code>提供了一个参数<code>disturl</code>，它可设置Node镜像地址，当然还是将其指向国内的淘宝镜像。这样又能爽歪歪安装这些依赖<code>C++模块</code>的模块了。</p>
<pre><code class="copyable">npm config set disturl https://npm.taobao.org/mirrors/node/
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-3">三.磨人的小妖精node-sass</h2>
<p>前面这两部操作面对一般的模块安装是没问题的可是有一些模块,哎,它就是不想让你好受,其中的代表者就是node-sass,这玩意靠前两步的操作还解决不了。</p>
<p>你要是强行安装的话,极有可能报这样的错
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/98084b6720c0470d914a31717ce9fc86~tplv-k3u1fbpfcp-zoom-1.image" alt loading="lazy" referrerpolicy="no-referrer"></p>
<p>原因是什么呢？</p>
<p>安装<code>node-sass</code>时，在<code>install阶段</code>会从Github上下载一个叫<code>binding.node</code>的文件，而「GitHub Releases」里的文件都托管在<code>s3.amazonaws.com</code>上，这个网址被Q了，所以又安装不了。</p>
<p>那是不是就没办法解决了呢?肯定不是啊,不然我写这篇文章干嘛,闲的蛋疼吗？</p>
<p>我们从<code>node-sass</code>的官方文档中可找到一个叫<code>sass_binary_site</code>的参数，它可设置Sass镜像地址，毫无疑问还是将其指向国内的淘宝镜像。这样又能爽歪歪安装<code>node-sass</code>了。</p>
<pre><code class="copyable">npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/
<span class="copy-code-btn">复制代码</span></code></pre>
<p>嘻嘻,问题到这就差不多要解决了。</p>
<p>为什么我要说差不多呢?</p>
<p>😭</p>
<p>因为我遇到的问题除了前面的哪些还有就是<strong>node版本与node-sass版本不兼容</strong></p>
<p>mmp</p>
<p>最后我的解决方法是在我电脑中找到存放node-sass的文件夹，一般是<code>C:\Users\AppData\Roaming\npm-cache\node-sass</code>这里,然后将网上下载的<a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fsass%2Fnode-sass%2Freleases%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/sass/node-sass/releases/" ref="nofollow noopener noreferrer">win32-x64-46_binding.node</a>文件直接放到这个文件夹里面问题就解决了。但显然这并不是一个好的解决方案。</p>
<p>正确的解决方法,应该是切换到正确的node版本重新下载对应的node-sass模块。对应关系如图所示</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2690249a98e4431fb4afa690ad515428~tplv-k3u1fbpfcp-watermark.image" alt="111.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-4">四.懒人必备的最终解决方案</h2>
<p>如果你觉得前面这些知识你不想知道,也觉得不重要的话。ok,没关系,你可以直接这样做。</p>
<h3 data-id="heading-5">第一步:查看自己的node版本与项目中package.json的node-sass版本是否如下表对应。</h3>
<p>如果对应,进行第二步,如果不对应,请使用切换node或node-sass版本。</p>
<h3 data-id="heading-6">第二步:切换镜像</h3>
<p>使用下列命令切换镜像，我这里使用的是淘宝镜像</p>
<pre><code class="copyable">npm config set registry https://registry.npm.taobao.org/
<span class="copy-code-btn">复制代码</span></code></pre>
<p>你也可以使用nrm切换镜像,具体使用可以看彩蛋</p>
<h3 data-id="heading-7">第三步：设置Sass镜像地址</h3>
<pre><code class="copyable">npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这里可以举一反三,对于另外一些有着同样问题的包,也可以这样解决。</p>
<pre><code class="copyable">npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/
npm config set sharp_dist_base_url https://npm.taobao.org/mirrors/sharp-libvips/
npm config set electron_mirror https://npm.taobao.org/mirrors/electron/
npm config set puppeteer_download_host https://npm.taobao.org/mirrors/
npm config set phantomjs_cdnurl https://npm.taobao.org/mirrors/phantomjs/
npm config set sentrycli_cdnurl https://npm.taobao.org/mirrors/sentry-cli/
npm config set sqlite3_binary_site https://npm.taobao.org/mirrors/sqlite3/
npm config set python_mirror https://npm.taobao.org/mirrors/python/
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-8">第四步:暴力解决</h3>
<p>直接从网上下载<a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fsass%2Fnode-sass%2Freleases%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/sass/node-sass/releases/" ref="nofollow noopener noreferrer">win32-x64-46_binding.node</a>,然后复制粘贴到node-sass所在的文件夹中。当然,不到万不得已,不要这样去做。</p>
<h2 data-id="heading-9">【彩蛋一——npm镜像管理nrm】</h2>
<p>npm包有很多的镜像源，有的源有的时候访问失败，有的源可能没有最新的包等等，所以有时需要切换npm的源，nrm包就是解决快速切换问题的。
nrm可以帮助您在不同的npm源地址之间轻松快速地切换。</p>
<p>nrm内置了如下源：</p>
<p>推荐使用淘宝镜像或cnpm</p>
<h3 data-id="heading-10">1.安装</h3>
<pre><code class="copyable">npm i -g nrm
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-11">2.查看是否安装成功:<code>nrm --version</code></h3>
<pre><code class="copyable">~ nrm --version

1.0.2
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-12">3.列出可选择的源:nrm ls</h3>
<pre><code class="copyable">~ nrm ls

  npm ---- https://registry.npmjs.org/
  cnpm --- http://r.cnpmjs.org/
* taobao - https://registry.npm.taobao.org/
  nj ----- https://registry.nodejitsu.com/
  rednpm - http://registry.mirror.cqupt.edu.cn/
  npmMirror  https://skimdb.npmjs.com/registry/
  edunpm - http://registry.enpmjs.org/
<span class="copy-code-btn">复制代码</span></code></pre>
<p><em><strong>注：</strong></em> 前面带 * 号的表示正在使用的源</p>
<h3 data-id="heading-13">4.切换使用的源:nrm use npm</h3>
<p><code>nrm use npm</code></p>
<pre><code class="copyable">~ nrm use npm
                        
   Registry has been set to: https://registry.npmjs.org/
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-14">5.添加一个源:nrm add  registry    url</h3>
<p>如果你想添加一个源，终端执行命令<code>nrm add <registry> <url> [home]</code>，reigstry为源名，url为源的路径， home为源的主页(可不写)。</p>
<pre><code class="copyable">~ nrm add company http://npm.company.com/   

    add registry company success
<span class="copy-code-btn">复制代码</span></code></pre>
<p><em><strong>注：</strong></em></p>
<ol>
<li>URL最后的/也可以不带，下面两个URL都是可以的：
<code>http://npm.company.com/</code>
<code>http://npm.company.com</code></li>
<li>[home]参数用于<code>nrm home</code>命令，用来查看源的主页。</li>
</ol>
<h3 data-id="heading-15">6.删除一个源:nrm del registry</h3>
<p>想要删除一个源，终端执行命令<code>nrm del <registry></code>，reigstry为源名.</p>
<pre><code class="copyable">~ nrm del company

    delete registry company success
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>注</strong>：nrm del 命令不能删除nrm自己内置的源。</p>
<h3 data-id="heading-16">7.测试源速度:nrm test</h3>
<p>测试一个源的响应时间：<code>nrm test npm</code></p>
<pre><code class="copyable">~ nrm test npm

* npm ---- 833ms
<span class="copy-code-btn">复制代码</span></code></pre>
<p>测试所有源的速度：<code>nrm test</code></p>
<pre><code class="copyable">~ nrm test

* npm ---- 807ms
  cnpm --- 374ms
  taobao - 209ms
  nj ----- Fetch Error
  rednpm - Fetch Error
  npmMirror  1056ms
  edunpm - Fetch Error
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-17">8.不使用nrm来切换源</h3>
<p>如果不是nrm也能切换源，只不过比较麻烦</p>
<p>查看当前使用的源</p>
<p><code>npm config get registry</code></p>
<pre><code class="copyable">~ npm config get registry
https://registry.npmjs.org/
<span class="copy-code-btn">复制代码</span></code></pre>
<p>设置一个源</p>
<p><code>npm config set registry https://registry.npm.taobao.org/</code></p>
<pre><code class="copyable">~ npm config set registry https://registry.npm.taobao.org/
<span class="copy-code-btn">复制代码</span></code></pre>
<p>设置成功后终端不会有任何输出。</p>
<ul>
<li>
<p>安装包使用特定源</p>
<p>全部使用特定源安装：</p>
<p><code>npm install --registry=https://registry.npm.taobao.org</code></p>
<p>安装一个包使用特定源：</p>
<p><code>npm i logo --registry=https://registry.npm.taobao.org</code></p>
</li>
</ul>
<h2 data-id="heading-18">【彩蛋二——nvm管理node】</h2>
<p>关于nvm的使用菜鸟教程写的不错,<a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.runoob.com%2Fw3cnote%2Fnvm-manager-node-versions.html" target="_blank" rel="nofollow noopener noreferrer" title="https://www.runoob.com/w3cnote/nvm-manager-node-versions.html" ref="nofollow noopener noreferrer">使用 nvm 管理不同版本的 node 与 npm</a></p>
<h2 data-id="heading-19">参看链接</h2>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2Fu4oI_tdYDIFQeTPSifCt7g%23" target="_blank" rel="nofollow noopener noreferrer" title="https://mp.weixin.qq.com/s/u4oI_tdYDIFQeTPSifCt7g#" ref="nofollow noopener noreferrer">聊聊NPM镜像那些险象环生的坑</a></p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000017419993" target="_blank" rel="nofollow noopener noreferrer" title="https://segmentfault.com/a/1190000017419993" ref="nofollow noopener noreferrer">npm源管理器nrm使用教程</a></p></div>  
</div>
            