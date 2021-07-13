
---
title: 'HTML_CSS_JaveScript 保存自动刷新'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d8dc90e62b514f4e8d30ce7f0980371b~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 05:17:14 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d8dc90e62b514f4e8d30ce7f0980371b~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>在开发静态的 HTML 页面时，屏幕通常是左边浏览器，打开正在测试的页面，右边 VSCode 写代码。如果要修改代码，VSCode 保存好，再手动在浏览器刷新一下页面才能看到效果。这样浏览器和 VSCode 不停地切换，不仅效率低，而且会打断思路。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d8dc90e62b514f4e8d30ce7f0980371b~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712203154346" loading="lazy" referrerpolicy="no-referrer"></p>
<p>所以，我们需要一个功能，只要保存 HTML / CSS / JavaScript 文件，浏览器就会自动刷新，显示最新的效果。</p>
<p>他们来了！他们来了！他们来了！</p>
<p>这个功能可以叫做 <code>实时更新</code>、<code>自动更新</code>、<code>热加载</code>、<code>live reload</code>、<code>hot reload</code>。有很多 <code>npm</code> 包可以实现这样的功能，我推荐两个比较牛逼的插件：</p>
<ul>
<li>live-server</li>
<li>Browser-sync</li>
</ul>
<p>这两个插件都是 <code>npm</code> 包，所以，安装的前提是，首先安装好 <code>Node.js</code>。</p>
<h2 data-id="heading-0">live-server</h2>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ade6d14d4edd48cd99e43aca8cbd3e9c~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712203249677" loading="lazy" referrerpolicy="no-referrer"> <a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Ftapio%2Flive-server" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/tapio/live-server" ref="nofollow noopener noreferrer">github.com/tapio/live-…</a></p>
<h3 data-id="heading-1">1. 安装 live-server</h3>
<pre><code class="hljs language-bash copyable" lang="bash">npm install -g live-server
<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<p>安装好 node.js 后才能使用 npm 命令</p>
</blockquote>
<h3 data-id="heading-2">2. 配置 npm 脚本</h3>
<p>在 HTML 项目的根目录下初始化 npm 配置</p>
<pre><code class="hljs language-bash copyable" lang="bash">npm init -y
<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<p>项目根目录下如果已经有 <code>package.json</code> 文件，表示已经是初始化了，这一步不需要执行。</p>
</blockquote>
<p>打开 <code>package.json</code> 文件，找到 <code>scripts</code> 节点，添加如下命令：</p>
<pre><code class="hljs language-json copyable" lang="json"><span class="hljs-string">"scripts"</span>: &#123;
    <span class="hljs-attr">"dev"</span>: <span class="hljs-string">"live-server"</span>
&#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e76c785df42b478ba5977162ac63c2ea~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712203907320" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-3">3. 启动 live-server</h3>
<p>在根目录下运行：</p>
<pre><code class="hljs language-bash copyable" lang="bash">npm run dev
<span class="copy-code-btn">复制代码</span></code></pre>
<p>看到 <code>serving .....</code> 表示服务器已经启动成功，打开 <code>http://127.0.0.1:8080</code>（会自动打开），即可看到首页。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e89e48da194a496eb264b871c7bedb35~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712204026002" loading="lazy" referrerpolicy="no-referrer"></p>
<p>见证奇迹的时刻到了，只要编辑项目下的任何文件，一按保存，页面马上会自动刷新。</p>
<blockquote>
<p>更多配置，可查看 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Ftapio%2Flive-server" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/tapio/live-server" ref="nofollow noopener noreferrer">github</a> 页面说明文档。</p>
</blockquote>
<h2 data-id="heading-4">Browser-sync</h2>
<p>官网：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fbrowsersync.io%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://browsersync.io/" ref="nofollow noopener noreferrer">browsersync.io/</a></p>
<p><code>Browser-sync</code> 使用方法和 <code>live-server</code> 大同小异。</p>
<h3 data-id="heading-5">1. 安装 Browser-sync</h3>
<pre><code class="hljs language-bash copyable" lang="bash">npm install -g browser-sync
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-6">2. 配置 npm 脚本</h3>
<pre><code class="hljs language-json copyable" lang="json"><span class="hljs-string">"scripts"</span>: &#123;
    <span class="hljs-attr">"dev"</span>: <span class="hljs-string">"browser-sync start --server --files \"**/**.*\""</span>
&#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
<p>配置稍微有点不一样，关键是 <code>--files</code> 后面跟的是要监测的文件，上面代表监测项目目录下的所有文件。</p>
<h3 data-id="heading-7">3. 启动 live-server</h3>
<pre><code class="hljs language-bash copyable" lang="bash">npm run dev
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9dafeccccfc3445e816c6f3ef893e6b6~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712204909220" loading="lazy" referrerpolicy="no-referrer"></p>
<p>同样，启动后也会打开首页，但是它监听的端口是 <code>3000</code>。</p>
<p>Browser-sync 的功能是非常强大的，也可以用做动态网站开发，具体查看官方文档。</p>
<h2 data-id="heading-8">监听原理</h2>
<blockquote>
<p>以 live-server 原理解释，browser-sync 类似</p>
</blockquote>
<p>live-server 是一个 node 应用，相当于一个功能小巧的服务器，它可以为项目下的所有文件提供服务。当 live-server 运行时，只要通过它请求的 html 文件，live-server 自动往 html 页面插入一小段 JavaScript 代码，这些代码用来和 live-server 建立 socket 链接，这样，浏览器的 HTML 页面就能和 live-server 通信了。同时，live-server 会检测项目下的文件变化，当有文件保存，live-server 通过 socket 通知 HTML 页面，重新加载 HTML 页面并且刷新。特别的，如果是 CSS 文件改变，live-server 并不会刷新整个页面，而是重新加载 CSS 而已。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4e052504273c46e0a6279691826706c8~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712210253766" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-9">live-server 的 VSCode 插件版</h2>
<p>另外，如果你使用的 IDE 是 VSCode，可以安装 <code>live server</code> 插件，使用更简单。</p>
<p>打开 <code>VSCode</code> 的插件面板，搜索 <code>live server</code> (注意：中间是空格，不是一杠)，排名第一的就是。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/398d029fd7c84802abbc2cccb9153950~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712210545448" loading="lazy" referrerpolicy="no-referrer"></p>
<p>安装后注意看右下角，多了一个按钮 <code>Go Live</code>，点一下就启动了！可以愉快地玩耍了。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f57f5867e3d947678d529cb8a0bac77d~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712210650172" loading="lazy" referrerpolicy="no-referrer"></p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b1c91038234c4b4da4139ccad6bd4751~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712210708551" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>其实还可以在 HTML 页面，点击右键，弹出菜单的 <code>Open with Live Server</code> 也是启动 Live Server 的</p>
</blockquote>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/83e478f38e14433ebef4a33fce81f94c~tplv-k3u1fbpfcp-zoom-1.image" alt="image-20210712210817923" loading="lazy" referrerpolicy="no-referrer"></p></div>  
</div>
            