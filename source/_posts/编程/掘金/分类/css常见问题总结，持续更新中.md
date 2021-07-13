
---
title: 'css常见问题总结，持续更新中...'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c52211acc6354d9f9a59050989c9d508~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 19:58:19 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c52211acc6354d9f9a59050989c9d508~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">1、盒子模型</h2>
<h3 data-id="heading-1">什么是盒子模型</h3>
<p>所有HTML元素可以看作盒子，CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距（margin），边框(border)，填充(padding)，和实际内容(content)</p>
<p>常见的盒子模型：标准盒子模型和IE盒子模型</p>
<h3 data-id="heading-2">标准盒子模型</h3>
<p>盒子的实际尺寸 = 内容（设置的宽/高） + 内边距 + 边框</p>
<p>如果使用标准模型宽度 = 410px (350 + 25 + 25 + 5 + 5)，高度 = 210px (150 + 25 + 25 + 5 + 5)，padding 加 border 再加 content box。</p>
<pre><code class="hljs language-js copyable" lang="js">.box &#123;
  <span class="hljs-attr">width</span>: 350px;
  height: 150px;
  margin: 25px;
  padding: 25px;
  border: 5px solid black;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c52211acc6354d9f9a59050989c9d508~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-3">IE盒子模型</h3>
<p>盒子的实际尺寸 = 设置的宽/高 = 内容 + 内边距 + 边框</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ccb4ff5ffee0427380801f787421e2a3~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>现在高版本的浏览器基本上默认都是使用标准盒模型，而像 IE6 默认使用 IE 盒模型的
在 CSS3 中新增了一个属性 box-sizing，允许开发者来指定盒子使用什么标准，它有 2 个值：</p>
<p>content-box：标准盒模型；
border-box：IE 盒模型；</p>
<h2 data-id="heading-4">2、BFC</h2>
<p>BFC（Block Formating Context）块级格式化上下文，是CSS中的一种渲染机制。是一个拥有独立渲染区域的盒子，规定了内部元素如何布局，并且盒子内部元素与外部元素互不影响。</p>
<h3 data-id="heading-5">BFC 渲染规则</h3>
<ol>
<li>内部的盒子会在垂直方向，一个接一个地放置；</li>
<li>盒子垂直方向的距离由 margin 决定，</li>
<li>属于同一个 BFC 的两个相邻盒子的 margin 会发生重叠；</li>
<li>每个元素的 margin 的左边，与包含块 border 的左边相接触(对于从左往右的格式化，否则相反)，即使存在浮动也是如此；</li>
<li>BFC 的区域不会与 float 盒子重叠；</li>
<li>BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。</li>
<li>计算 BFC 的高度时，浮动元素也参与计算。</li>
</ol>
<h3 data-id="heading-6">如何创建 BFC？</h3>
<ol>
<li>根元素：html</li>
<li>非溢出的可见元素：overflow 不为 visible</li>
<li>设置浮动：float 属性不为 none</li>
<li>设置定位：position 为 absolute 或 fixed</li>
<li>定义成块级的非块级元素：display: inline-block/table-cell/table-caption/flex/inline-flex/grid/inline-grid</li>
</ol>
<h3 data-id="heading-7">BFC的应用</h3>
<h4 data-id="heading-8">1、两栏布局</h4>
<p>BFC 的区域不会与 float 盒子重叠</p>
<pre><code class="copyable"> <div class="layout">
  <div class="aside">aside</div>
  <div class="main">main</div>
</div>


<style>
  .aside&#123;
     width:120px;
     float:left;
  &#125;
  .main&#123;
    background-color: blue;
    overflow: hidden;
  &#125;
</style>
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-9">2、margin间距合并</h4>
<p>属于同一个 BFC 的两个相邻盒子的 margin 会发生重叠；</p>
<pre><code class="copyable"> <div class="parent">
   <div class="child child1">我是child1</div>
   <div class="child child2">我是child1</div>
 </div>
 
 <style>
    .child1&#123;
      margin-bottom:10px;
      margin-top:10px;
      background-color: green;
    &#125;
    .child2&#123;
      background-color: red;
      margin-top:10px;
    &#125;
 </style>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>我们以为child1和child2的间距会是20px，但是由于BFC的两个相邻盒子的 margin 会发生重叠，他们之间的间距会取最大的值作为结果，即10px，那如何解决呢？</p>
<p>再创建一个div父元素包裹，创建两个BFC，但是这样就改变了dom的结构，我们一般不建议这样做，我们直接设置一个margin值是两个值的和即可</p>
<pre><code class="copyable"> <div class="parent">
   <div class="child child1">我是child1</div>
   <div class="wrap"><div class="child child2">我是child1</div></div>
 </div>
 <style>
 
     .parent&#123;
      background-color: blue;
    &#125;
    .child1&#123;
      margin-bottom:10px;
      margin-top:10px;
      background-color: green;
    &#125;
    .child2&#123;
      background-color: red;
      margin-top:10px;
    &#125;
    .wrap&#123;
      overflow: hidden;
    &#125;
 </style>
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-10">3、margin 塌陷</h4>
<p>什么是margin塌陷，我们来看一段代码</p>
<pre><code class="copyable"><style>
   .parent&#123;
      background-color: blue;
      height: 100px;
    &#125;
    .child&#123;
      margin-top:100px;
      height: 20px;
      background-color: green;
    &#125;
</style>

 <div class="parent">
   <div class="child">我是child</div>
 </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/44ca4428ec2e47159053a357fe2bdf43~tplv-k3u1fbpfcp-watermark.image" alt="abc.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>child并没有距离parent 100px，而是parent距离顶部100px，这就是margin塌陷，那如何解决呢？ 我们还是利用BFC ,给parent创建一个BFC</p>
<pre><code class="copyable"><style>
   .parent&#123;
      background-color: blue;
      height: 100px;
      overflow:hidden;
    &#125;
    .child&#123;
      margin-top:100px;
      height: 20px;
      background-color: green;
    &#125;
</style>

 <div class="parent">
   <div class="child">我是child</div>
 </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-11">4、清除浮动</h4>
<p>这个就不多说了，大家都知道</p>
<h2 data-id="heading-12">3、css隐藏元素的方式以及区别</h2>
<ol>
<li>opacity:0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定 一些事件，如 click 事件，那么点击该区域，也能触发点击事件的</li>
<li>visibility:hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件</li>
<li>display:none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元 素删除掉。</li>
</ol>
<h2 data-id="heading-13">4、元素居中的几种方式</h2>
<h3 data-id="heading-14">固定宽度</h3>
<p>1、子元素利用position和margin为宽高的一半来实现</p>
<pre><code class="copyable"><style>
    .parent1&#123;
      width: 200px;
      height: 200px;
      position: relative;
      background-color: red;
    &#125;
    .chid1&#123;
      width: 50px;
      height: 100px;
      position: absolute;
      left:50%;
      top:50%;
      background-color: gray;
      margin-left:-25px;
      margin-top:-50px;
    &#125;
</style>
  <div class="parent1">
    <div class="chid1">child1</div>
  </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>2、子元素设置 position: absolute，margin:auto 平均分配 margin</p>
<pre><code class="copyable"><style>
.parent2&#123;
      width: 200px;
      height: 200px;
      position: relative;
      background-color: red;
      margin-top:100px;
    &#125;
    .chid2&#123;
      width: 50px;
      height: 100px;
      position: absolute;
      margin:auto;
      left:0;
      top:0;
      right:0;
      bottom:0;
      background-color: gray;
    &#125;
</style>


 <div class="parent2">
    <div class="chid2">child2</div>
  </div>
  
  
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-15">不定宽度</h3>
<p>1、子元素通过transform来实现</p>
<pre><code class="copyable"><style>
    .parent3&#123;
      width: 200px;
      height: 200px;
      position: relative;
      background-color: red;
      margin-top:100px;
    &#125;
    .chid3&#123;
    
      position: absolute;
      margin:auto;
      left:50%;
      top:50%;
      transform:translate(-50%,-50%);
      background-color: gray;
    &#125;
</style>
 <div class="parent3">
    <div class="chid3">child3</div>
  </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>2、父元素设置display:flex来实现</p>
<pre><code class="copyable">.parent4&#123;
      width: 200px;
      height: 200px;
      position: relative;
      background-color: red;
      margin-top:100px;
      display: flex;
      justify-content: center;
      align-items: center;
    &#125;
    .chid4&#123;
    
      background-color: gray;
    &#125;
    
     <div class="parent4">
    <div class="chid4">child4</div>
  </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>3、父元素设置display:table-cell来实现</p>
<pre><code class="copyable">    .parent5&#123;
      width: 200px;
      height: 200px;
      position: relative;
      background-color: red;
      margin-top:100px;
     display: table-cell;
     vertical-align: middle;
      text-align: center
    &#125;
    .chid5&#123;
      display: inline-block;
      background-color: gray;
    &#125;
    
      <div class="parent5">
            <div class="chid5">child5</div>
      </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-16">5、如何画一个三角形</h2>
<p>利用元素的 border 绘制三角形，先来看一下宽高均为 0，border 有宽度的效果</p>
<pre><code class="copyable"><style>
.triangle &#123;
            width: 0;
            height: 0;
            border-top: 100px solid #f00;
            border-right: 100px solid #0f0;
            border-bottom: 100px solid #00f;
            border-left: 100px solid #ff0;
        &#125;
</style>

<div class="triangle"></div>

<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/11217a402db245a08a83c38198c8a949~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>接下来我们就是给给任意一个边设置颜色，其他边设置透明，来实现不同方向的三角形</p>
<pre><code class="copyable">    .triangle &#123;
                width: 0;
                height: 0;
                border: 100px solid transparent;
                border-bottom: 100px solid #00f;
            &#125;
    </style>
    
    <div class="triangle"></div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e016ef0eef454528af7852e69d7e11e3~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<pre><code class="copyable">    .triangle &#123;
                width: 0;
                height: 0;
                border: 100px solid transparent;
                border-left: 100px solid #00f;
            &#125;
    </style>
    
    <div class="triangle"></div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f2e8c149a1549de912389ecb4d754c8~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>依次类推，就可以设置不同方向的三角形，那如果想让三角形变高，就调整设置方向的数值，让他变大</p>
<pre><code class="copyable">    .triangle &#123;
                width: 0;
                height: 0;
                border: 100px solid transparent;
                border-bottom: 200px solid #00f;
            &#125;
    </style>
    
    <div class="triangle"></div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b6f87a0c268140678e42e9f48c3eb646~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<pre><code class="copyable">    .triangle &#123;
                width: 0;
                height: 0;
                border: 100px solid transparent;
                border-bottom: 50px solid #00f;
            &#125;
    </style>
    
    <div class="triangle"></div>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/79f5fa669d4c447586dcef9c08e7106e~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-17">6、如何使footer永远处于页面的底部</h2>
<p>内容区域的padding值就是footer的高度，切一定要让container设置min-height</p>
<pre><code class="copyable">  <style>
    html,body&#123;
      height: 100%;
      min-height: 100%;
    &#125;
    .footer&#123;
      position:absolute;
      height: 200px;
      bottom: 0;
      width: 100%;
      background-color: gray;
    &#125;
    .container&#123;
      position: relative;
      min-height: 100%;
    &#125;
    .main&#123;
      padding-bottom: 200px;
    &#125;
  </style>
  <div class="container">
    <div class="main">我是content</div>
    <div class="footer">我是footer</div>
  </div>
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-18">参考</h1>
<p><a href="https://juejin.cn/post/6941206439624966152#heading-50" target="_blank" title="https://juejin.cn/post/6941206439624966152#heading-50">juejin.cn/post/694120…</a></p>
<p><a href="https://juejin.cn/post/6844904062593269768#heading-0" target="_blank" title="https://juejin.cn/post/6844904062593269768#heading-0">juejin.cn/post/684490…</a></p></div>  
</div>
            