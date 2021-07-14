
---
title: '实战 rollup 第一节， 入门'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b9497552ef7249b7a3ec95cd9e73de2d~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Tue, 13 Jul 2021 21:52:34 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b9497552ef7249b7a3ec95cd9e73de2d~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><blockquote>
<p><code>rollup</code> 是啥，咋不过多介绍，这里记录一下自己在看<code>rollup</code>文档和相关资料，然后手动来敲一些代码，并且以博客的形式输入，加深自己的理解</p>
</blockquote>
<h1 data-id="heading-0">本次的目标</h1>
<blockquote>
<p>熟悉一些基本的配置，相比webpack来说，配置项还是少了许多的，虽然webpack既有 <code>plugin</code>, 也有<code>loader</code>。 但是 <code>rollup</code> 貌似是只有<code>plugin</code>的。</p>
</blockquote>
<p>既然是打包工具，那么肯定先打个包在说。多个文件相互引入，然后输出打包结果。</p>
<h1 data-id="heading-1">目录</h1>
<pre><code class="copyable">my-rollup    //我的项目名称
├─ build  // 配置的打包目录
│  └─ rollup.config.js // 结果配置文件
├─ dist   // 存放打包输出目录
│  └─ index.js // 打包结果的源文件
├─ package-lock.json  // npm 锁定包版本的文件
├─ package.json // npm 入口文件
└─ src  // 源代码
   ├─ add.js  // 对外导出一个add方法
   ├─ index.js // 主入口
   └─ reduce.js // 对外导出一个reduce方法
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-2">代码编写</h1>
<blockquote>
<p>由于我们使用 <code>rollup</code>, 所以就先安装 <code>rollup</code>的包, <code>npm install rollup -D</code>或者<code>npm install --save-dev rollup</code> 都行，然后为了检验代码的结果， 我们在安装一个 将 <code>es6</code> 转成 <code>es5</code>的库——<a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2F%40rollup%2Fplugin-buble" target="_blank" rel="nofollow noopener noreferrer" title="https://www.npmjs.com/package/@rollup/plugin-buble" ref="nofollow noopener noreferrer"><code>@rollup/plugin-buble</code></a>.</p>
</blockquote>
<h2 data-id="heading-3">package.json 文件最终如下</h2>
<pre><code class="copyable">&#123;
  "name": "my-rollup",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": &#123;
    "build": "rollup -c ./build/rollup.config.js" # 执行的命令， 
  &#125;,
  "author": "",
  "license": "ISC",
  "devDependencies": &#123;
    "@rollup/plugin-buble": "^0.21.3",
    "rollup": "^2.53.1"
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-4">配置 <code>rollup.config.js</code> 文件</h2>
<blockquote>
<p><code>rollup.config.js</code>里面的环境是<code>node</code>环境，所以目前需要使用<code>commonJS</code>的语法。<code>rollup</code> 使用插件也是一个配置选项， 直接在对外导出的对象中 包含 <code>plugins</code>这个熟悉就行,详情如下：</p>
</blockquote>
<pre><code class="copyable">
const path = require('path');

const buble = require('@rollup/plugin-buble');
 
const resolve = function(filePath) &#123;
  return path.join(__dirname, '..', filePath)
&#125;


module.exports = &#123;
  input: resolve('src/index.js'),
  output: &#123;
    file: resolve('dist/index.js'),
    format: 'iife' 
  &#125;,
  plugins: [
    buble()
  ]
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-5">书写主要程序的代码</h2>
<h3 data-id="heading-6"><code>src/index.js</code></h3>
<pre><code class="copyable">import &#123; add &#125; from "./add";
import &#123; reduce &#125; from "./reduce";

const arr1 = ['a', 'b','c'];
const arr2 = [4,5,6];

const result = [...arr1, ...arr2];


console.log(result);
const a = 1, b = 2;

const res =  add(a, b);

const d = reduce(a, b); 
console.log(res,);
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-7"><code>add.js</code> 和 <code>reducer.js</code></h3>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b9497552ef7249b7a3ec95cd9e73de2d~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<h1 data-id="heading-8">打包</h1>
<blockquote>
<p>代码写好了，直接在终端 使用 <code>npm run build</code><br>
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/161c1b595049446f8ec6365849b99651~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
</blockquote>
<h1 data-id="heading-9">分析打包姐</h1>
<blockquote>
<p>打包的结果如下：<br>
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1e89fcef4518491fa2e9dda17d865bb4~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"><br>
这里我们就可以简单的得出结论， <code>rollup</code>的 <code>treeshaking</code> 是基于 <code>esm</code> 语法来的。 如果导入了方法没有使用的话，是不会被加入打包结果的。 但是怎么做到的咋们后面来聊</p>
</blockquote>
<h1 data-id="heading-10">代码执行结果</h1>
<blockquote>
<p>这个代码的执行结果，大家一眼就看的出来，我还是放出来吧。</p>
</blockquote>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/76411ec5649646b49c7a334e7d3e4eac~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>本文使用 <a href="https://juejin.cn/post/6940875049587097631" target="_blank" title="https://juejin.cn/post/6940875049587097631">文章同步助手</a> 同步</p>
</blockquote></div>  
</div>
            