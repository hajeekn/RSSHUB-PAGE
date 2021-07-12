
---
title: '手把手教你 Electron + Vue 搭建前端桌面应用'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/24c875527f2d4f50b5126b1185fcf4dd~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 17:49:25 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/24c875527f2d4f50b5126b1185fcf4dd~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">一、在使用 Electron 之前我们要了解 Electron 是什么？</h3>
<p>Electron 官网地址 点此 :   <a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.electronjs.org%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://www.electronjs.org/" ref="nofollow noopener noreferrer">electron 官方地址</a></p>
<blockquote>
<p>Electron 相当于一个浏览器的外壳 , 我们将 编写的 HTML , CSS , Javascript 网页程序 嵌入进 Electron 里面</p>
<p>以便于在桌面上进行运行。 通俗来讲它就是一个软件 ， 如 QQ 、网易云音乐、优酷视频 等等。功能至强大</p>
<p>超乎你的想象</p>
</blockquote>
<h3 data-id="heading-1">二、开发环境的准备</h3>
<ol>
<li>
<p>安装 Node.js 坏境</p>
<p>Node.js 官网地址 点此 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fnodejs.org%2Fzh-cn%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://nodejs.org/zh-cn/" ref="nofollow noopener noreferrer">node.js 官方地址</a></p>
</li>
<li>
<p>安装 Vue Cli</p>
<pre><code class="hljs language-javascript copyable" lang="javascript">npm install -g @vue/cli
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>安装 淘宝镜像 cnpm    ( 因 electron 包 特别大  本人尝试过 npm 或 yarn 的 方法 需要等待很长时间 )</p>
</li>
<li>
<p>全局安装 Electron</p>
<pre><code class="hljs language-javascript copyable" lang="javascript">cnpm install electron -g

<span class="hljs-comment">//如果安装还是 特比慢 或 不想安装cnpn 可以联系我们</span>
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
</ol>
<p>​ 查看 是否安装成功 :</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/24c875527f2d4f50b5126b1185fcf4dd~tplv-k3u1fbpfcp-watermark.image" alt="elec2.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-2">三、 搭建 vue 环境</h3>
<pre><code class="copyable">1. 首先使用 vue-cli 搭建基础 vue框架
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ae8f15c916a45efb2a7eb3f34b63e6a~tplv-k3u1fbpfcp-watermark.image" alt="elec3.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>和平时写 vue项目一样 选择自己需要的</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dac0c5107710455587fc1338ec6b8ddf~tplv-k3u1fbpfcp-watermark.image" alt="elec4.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>cd electron-demo      进入项目目录</p>
<p>yarn serve     启动项目</p>
</blockquote>
<h3 data-id="heading-3">四、vue项目中添加 electron 模块</h3>
<blockquote>
<p>输入     vue  add  electron-builder  后 按下回车</p>
</blockquote>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ed66d320006a408a88319d894b378705~tplv-k3u1fbpfcp-watermark.image" alt="elec5.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>安装过程中  此处我们选择   ^13.0.0    按下回车</p>
</blockquote>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6101831dc75d44d8b33b69b510413a7a~tplv-k3u1fbpfcp-watermark.image" alt="elec6.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>因 electron 安装时间过长  导致安装失败</p>
</blockquote>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4b3a54eafd2495eb6d81c01eb73aa06~tplv-k3u1fbpfcp-watermark.image" alt="elec7.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/23410b9db6fe49a1bf36fc2acb44d746~tplv-k3u1fbpfcp-watermark.image" alt="elec8.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>解决办法  直接使用 cnpm install 进行安装</p>
</blockquote>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4974ccf860cc4c9189b9df010a74fff9~tplv-k3u1fbpfcp-watermark.image" alt="elec9.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>安装 完成后 我们使用 npm run electron:serve  运行项目 依旧是报错的。请耐心往下看完</p>
</blockquote>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/238be00304eb4a219b5da78e8c899d12~tplv-k3u1fbpfcp-watermark.image" alt="elec10.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>此处 我们需要打开项目的目录  找到 node_modules 下的 electron 。 删除 这个文件以后 重新使用 cnpm install</p>
</blockquote>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8960bac02b98492285d5b8fed541e8d8~tplv-k3u1fbpfcp-watermark.image" alt="elec12.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>至此。 electron 应用 已经搭建完成。   我们使用  npm run electron:serve 进行启动项目 ( windows 与 imac  一样 )</p>
</blockquote>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4f86bd1238040d785ceb8017bb41e11~tplv-k3u1fbpfcp-watermark.image" alt="elec13.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>已经完美运行成功  可以看到桌面已经弹出 electron-demo 应用</p>
</blockquote>
<h3 data-id="heading-4">五、查看electron+vue 项目目录</h3>
<blockquote>
<p>相比于  基础 vue 项目  我们可以发现在目录中 多出一个 background.js 文件</p>
</blockquote>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/107da3a92b2b42378a9b9665febfd1dc~tplv-k3u1fbpfcp-watermark.image" alt="elec14.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>此处可以 配置 electron 应用的一些设置。 如窗口大小 、 是否可以缩放、是否可以移动窗口等等</p>
</blockquote>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3c16053308d246da945126264a1378e8~tplv-k3u1fbpfcp-watermark.image" alt="elec15.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>Background.js 文件</p>
</blockquote>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-meta">'use strict'</span>

<span class="hljs-keyword">import</span> &#123; app, protocol, BrowserWindow &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'electron'</span>
<span class="hljs-keyword">import</span> &#123; createProtocol &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'vue-cli-plugin-electron-builder/lib'</span>
<span class="hljs-keyword">import</span> installExtension, &#123; VUEJS_DEVTOOLS &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'electron-devtools-installer'</span>
<span class="hljs-keyword">const</span> isDevelopment = process.env.NODE_ENV !== <span class="hljs-string">'production'</span>

<span class="hljs-comment">// Scheme must be registered before the app is ready</span>
protocol.registerSchemesAsPrivileged([
  &#123; <span class="hljs-attr">scheme</span>: <span class="hljs-string">'app'</span>, <span class="hljs-attr">privileges</span>: &#123; <span class="hljs-attr">secure</span>: <span class="hljs-literal">true</span>, <span class="hljs-attr">standard</span>: <span class="hljs-literal">true</span> &#125; &#125;
])

<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">createWindow</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-comment">// Create the browser window.</span>
  <span class="hljs-keyword">const</span> win = <span class="hljs-keyword">new</span> BrowserWindow(&#123;
    <span class="hljs-attr">width</span>: <span class="hljs-number">1120</span>,
    <span class="hljs-attr">height</span>: <span class="hljs-number">1090</span>,
    <span class="hljs-attr">minHeight</span>: <span class="hljs-number">700</span>,
    <span class="hljs-attr">minWidth</span>: <span class="hljs-number">1000</span>,
    <span class="hljs-attr">webPreferences</span>: &#123;

      <span class="hljs-comment">// Use pluginOptions.nodeIntegration, leave this alone</span>
      <span class="hljs-comment">// See nklayman.github.io/vue-cli-plugin-electron-builder/guide/security.html#node-integration for more info</span>
      <span class="hljs-attr">nodeIntegration</span>: process.env.ELECTRON_NODE_INTEGRATION,
      <span class="hljs-attr">contextIsolation</span>: !process.env.ELECTRON_NODE_INTEGRATION
    &#125;
  &#125;)

  <span class="hljs-keyword">if</span> (process.env.WEBPACK_DEV_SERVER_URL) &#123;
    <span class="hljs-comment">// Load the url of the dev server if in development mode</span>
    <span class="hljs-keyword">await</span> win.loadURL(process.env.WEBPACK_DEV_SERVER_URL)
    <span class="hljs-comment">// if (!process.env.IS_TEST) win.webContents.openDevTools()</span>
  &#125; <span class="hljs-keyword">else</span> &#123;
    createProtocol(<span class="hljs-string">'app'</span>)
    <span class="hljs-comment">// Load the index.html when not in development</span>
    win.loadURL(<span class="hljs-string">'app://./index.html'</span>)
  &#125;
&#125;

<span class="hljs-comment">// Quit when all windows are closed.</span>
app.on(<span class="hljs-string">'window-all-closed'</span>, <span class="hljs-function">() =></span> &#123;
  <span class="hljs-comment">// On macOS it is common for applications and their menu bar</span>
  <span class="hljs-comment">// to stay active until the user quits explicitly with Cmd + Q</span>
  <span class="hljs-keyword">if</span> (process.platform !== <span class="hljs-string">'darwin'</span>) &#123;
    app.quit()
  &#125;
&#125;)

app.on(<span class="hljs-string">'activate'</span>, <span class="hljs-function">() =></span> &#123;
  <span class="hljs-comment">// On macOS it's common to re-create a window in the app when the</span>
  <span class="hljs-comment">// dock icon is clicked and there are no other windows open.</span>
  <span class="hljs-keyword">if</span> (BrowserWindow.getAllWindows().length === <span class="hljs-number">0</span>) createWindow()
&#125;)

<span class="hljs-comment">// This method will be called when Electron has finished</span>
<span class="hljs-comment">// initialization and is ready to create browser windows.</span>
<span class="hljs-comment">// Some APIs can only be used after this event occurs.</span>
app.on(<span class="hljs-string">'ready'</span>, <span class="hljs-keyword">async</span> () => &#123;
  <span class="hljs-keyword">if</span> (isDevelopment && !process.env.IS_TEST) &#123;
    <span class="hljs-comment">// Install Vue Devtools</span>
    <span class="hljs-keyword">try</span> &#123;
      <span class="hljs-keyword">await</span> installExtension(VUEJS_DEVTOOLS)
    &#125; <span class="hljs-keyword">catch</span> (e) &#123;
      <span class="hljs-built_in">console</span>.error(<span class="hljs-string">'Vue Devtools failed to install:'</span>, e.toString())
    &#125;
  &#125;
  createWindow()
&#125;)

<span class="hljs-comment">// Exit cleanly on request from parent process in development mode.</span>
<span class="hljs-keyword">if</span> (isDevelopment) &#123;
  <span class="hljs-keyword">if</span> (process.platform === <span class="hljs-string">'win32'</span>) &#123;
    process.on(<span class="hljs-string">'message'</span>, <span class="hljs-function">(<span class="hljs-params">data</span>) =></span> &#123;
      <span class="hljs-keyword">if</span> (data === <span class="hljs-string">'graceful-exit'</span>) &#123;
        app.quit()
      &#125;
    &#125;)
  &#125; <span class="hljs-keyword">else</span> &#123;
    process.on(<span class="hljs-string">'SIGTERM'</span>, <span class="hljs-function">() =></span> &#123;
      app.quit()
    &#125;)
  &#125;
&#125;

<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<p>注意：打开和 关闭 开发者工具 请点击。    操作栏  >  view  >  Toggle Developer tools</p>
</blockquote>
<blockquote>
<p>我们可以在官网的文档里搜索一下。进行一些配置  （ 详细配置请查看官网配置 ） 链接已经放在文章开头啦</p>
</blockquote>
<h3 data-id="heading-5">六、打包 electron 应用</h3>
<blockquote>
<p>打包应用  使用    npm run electron:build  进行打包 （ imac 系统 和 windows系统 一样使用这个 ）</p>
</blockquote>
<blockquote>
<p>此处 以 iMac 为例 （ 下面会有 windows 解决方案 ）</p>
</blockquote>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b56b0c995f994a14a88b27879fd1e6a5~tplv-k3u1fbpfcp-watermark.image" alt="elec16.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>当我们看到。 Build complete ! 时 就说明 打包成功 可以查看 dist_electron / mac   里面就是打包好的应用   （ 苹果系统 ）</p>
</blockquote>
<h5 data-id="heading-6">windows 解决方案</h5>
<ul>
<li>打包 windows 应用时 我们需要将 整个项目的源码 上传到 windows 电脑上</li>
<li>上传到 windows 电脑上后  同样需要安装 cnpm  不然 electron 是安装不上的</li>
<li>打开项目目录   删除掉 node_modules 重新 cnpm install</li>
<li>如果还是无法打包 删除掉 node_modules / electron 目录  重新 cnpm install</li>
<li>然后运行 npm run electron:build 进行打包</li>
</ul>
<br>
<br>
<br>
<h3 data-id="heading-7">PS:大家看了后觉得对自己有帮助可以三连留言,欢迎提出宝贵意见，也欢迎各位对相关技术有兴趣的开发者（由团队开发人员微信号x118422邀请）入群，在线解答讨论数据可视化、优化图表性能等方面的技术问题~</h3></div>  
</div>
            