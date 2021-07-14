
---
title: '在vue中使用jsx的正确姿势'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=5964'
author: 掘金
comments: false
date: Tue, 13 Jul 2021 21:55:33 GMT
thumbnail: 'https://picsum.photos/400/300?random=5964'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;color:#595959;font-size:15px;font-family:-apple-system,system-ui,BlinkMacSystemFont,Helvetica Neue,PingFang SC,Hiragino Sans GB,Microsoft YaHei,Arial,sans-serif;background-image:linear-gradient(90deg,rgba(60,10,30,.04) 3%,transparent 0),linear-gradient(1turn,rgba(60,10,30,.04) 3%,transparent 0);background-size:20px 20px;background-position:50%&#125;.markdown-body p&#123;color:#595959;font-size:15px;line-height:2;font-weight:400&#125;.markdown-body p+p&#123;margin-top:16px&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;padding:30px 0;margin:0;color:#135ce0&#125;.markdown-body h1&#123;position:relative;text-align:center;font-size:22px;margin:50px 0&#125;.markdown-body h1:before&#123;position:absolute;content:"";top:-10px;left:50%;width:32px;height:32px;transform:translateX(-50%);background-size:100% 100%;opacity:.36;background-repeat:no-repeat;background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAABfVBMVEX///8Ad/8AgP8AgP8AgP8Aff8AgP8Af/8AgP8AVf8Af/8Af/8AgP8AgP8Af/8Afv8AAP8Afv8Afv8Aef8AgP8AdP8Afv8AgP8AgP8Acf8Ae/8AgP8Af/8AgP8Af/8Af/8AfP8Afv8AgP8Af/8Af/8Afv8Afv8AgP8Afv8AgP8Af/8Af/8AgP8AgP8Afv8AgP8Af/8AgP8AgP8AgP8Ae/8Afv8Af/8AgP8Af/8AgP8Af/8Af/8Aff8Af/8Abf8AgP8Af/8AgP8Af/8Af/8Afv8AgP8AgP8Afv8Afv8AgP8Af/8Aff8AgP8Afv8AgP8Aff8AgP8AfP8AgP8Ae/8AgP8Af/8AgP8AgP8AgP8Afv8AgP8AgP8AgP8Afv8AgP8AgP8AgP8AgP8AgP8Af/8AgP8Af/8Af/8Aev8Af/8AgP8Aff8Afv8AgP8AgP8AgP8Af/8AgP8Af/8Af/8AgP8Afv8AgP8AgP8AgP8AgP8Af/8AeP8Af/8Af/8Af//////rzEHnAAAAfXRSTlMAD7CCAivatxIDx5EMrP19AXdLEwgLR+6iCR/M0yLRzyFF7JupSXn8cw6v60Q0QeqzKtgeG237HMne850/6Qeq7QaZ+WdydHtj+OM3qENCMRYl1B3K2U7wnlWE/mhlirjkODa9FN/BF7/iNV/2kASNZpX1Wlf03C4stRGxgUPclqoAAAABYktHRACIBR1IAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4gEaBzgZ4yeM3AAAAT9JREFUOMvNUldbwkAQvCAqsSBoABE7asSOBRUVVBQNNuy9996789+9cMFAMHnVebmdm+/bmdtbQv4dOFOW2UjPzgFyLfo6nweKfIMOBYWwFtmMPGz2Yj2pJI0JDq3udJW6VVbmKa9I192VQFV1ktXUAl5NB0cd4KpnORqsEO2ZIRpF9gJfE9Dckqq0KuZt7UAH5+8EPF3spjsRpCeQNO/tA/qDwIDA+OCQbBoKA8NOdjMySgcZGVM6jwcgRuUiSs0nlPFNSrEpJfU0jTLD6llqbvKxei7OzvkFNQohi0vAsj81+MoqsCaoPOQFgus/1LyxichW+hS2JWCHZ7VlF9jb187pIAYcHiViHAMnp5mTjJ8B5xeEXF4B1ze/fTh/C0h398DDI9HB07O8ci+vRBdvdGnfP4gBuM8vw7X/G3wDmFhFZEdxzjMAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTgtMDEtMjZUMDc6NTY6MjUrMDE6MDA67pVWAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE4LTAxLTI2VDA3OjU2OjI1KzAxOjAwS7Mt6gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAAWdEVYdFRpdGxlAGp1ZWppbl9sb2dvIGNvcHlxapmKAAAAV3pUWHRSYXcgcHJvZmlsZSB0eXBlIGlwdGMAAHic4/IMCHFWKCjKT8vMSeVSAAMjCy5jCxMjE0uTFAMTIESANMNkAyOzVCDL2NTIxMzEHMQHy4BIoEouAOoXEXTyQjWVAAAAAElFTkSuQmCC)&#125;.markdown-body h2&#123;position:relative;font-size:20px;border-left:4px solid;padding:0 0 0 10px;margin:30px 0&#125;.markdown-body h3&#123;font-size:16px&#125;.markdown-body ul&#123;list-style:disc outside;margin-left:2em;margin-top:1em&#125;.markdown-body li&#123;line-height:2;color:#595959&#125;.markdown-body img.loaded&#123;margin:0 auto;display:block&#125;.markdown-body blockquote&#123;background:#fff9f9;margin:2em 0;padding:2px 20px;border-left:4px solid #b2aec5&#125;.markdown-body blockquote p&#123;color:#666;line-height:2&#125;.markdown-body a&#123;color:#036aca;border-bottom:1px solid rgba(3,106,202,.8);font-weight:400;text-decoration:none&#125;.markdown-body em strong,.markdown-body strong&#123;color:#036aca&#125;.markdown-body hr&#123;border-top:1px solid #135ce0&#125;.markdown-body pre&#123;overflow:auto&#125;.markdown-body code,.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body table&#123;border-collapse:collapse;margin:1rem 0;overflow-x:auto&#125;.markdown-body table td,.markdown-body table th&#123;border:1px solid #dfe2e5;padding:.6em 1em&#125;.markdown-body table tr&#123;border-top:1px solid #dfe2e5&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f6f8fa&#125;</style><h1 data-id="heading-0">在vue3中使用jsx的正确姿势</h1>
<h2 data-id="heading-1">前言</h2>
<p>又到了愉快的摸鱼时间,我觉得不能荒废,H5页面我一直用的vant,出于对源码的好奇,我从git上拉了一份vant源码,里面竟然都是jsx写的组件,于是我开始了对在vue中使用jsx的探索</p>
<h2 data-id="heading-2">虚拟DOM</h2>
<h3 data-id="heading-3">什么是虚拟DOM</h3>
<p>在这之前，先了解下虚拟DOM，vue和react框架都在内部使用了虚拟DOM，这样做的原因是通过js操作DOM的计算成本很高，虽然js更新速度很快，但是查找dom并更新的成本很高。那么有什么方法可以优化呢，vue等框架使用js对象，通过改变js对象，最后进行批量处理，一次更新DOM，所以虚拟DOM本质上就是一个js对象</p>
<h3 data-id="heading-4">虚拟DOM的优点</h3>
<ul>
<li>从原先的操作真实DOM到操作虚拟DOM，降低查找成本</li>
<li>通过diff比对，我们可以更快的定位数据的变化，从而更新DOM</li>
<li>更好的ui更新</li>
<li>抽象渲染过程，带来了实现跨平台的能力，如vue3中的createRenderer API</li>
</ul>
<h2 data-id="heading-5">渲染函数是什么</h2>
<p>渲染函数是用来生成虚拟DOM的。我们在vue单文件中编写模板语法，最终会在底层实现中被编译成渲染函数</p>
<p>Vue 推荐在绝大多数情况下使用模板来创建你的 HTML。然而在一些场景中，你真的需要 JavaScript 的完全编程的能力。这时你可以用渲染函数，它比模板更接近编译器。</p>
<p>当出现以下场景，虽然下列写法也能实现想要的效果，但是他不仅冗长，而且我们为每个级别标题重复书写了 。当我们添加锚元素时，我们必须在每个 v-if/v-else-if 分支中再次重复它</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> &#123; createApp &#125; = Vue

<span class="hljs-keyword">const</span> app = createApp(&#123;&#125;)

app.component(<span class="hljs-string">'anchored-heading'</span>, &#123;
  <span class="hljs-attr">template</span>: <span class="hljs-string">`
    <h1 v-if="level === 1">
      <slot></slot>
    </h1>
    <h2 v-else-if="level === 2">
      <slot></slot>
    </h2>
    <h3 v-else-if="level === 3">
      <slot></slot>
    </h3>
    <h4 v-else-if="level === 4">
      <slot></slot>
    </h4>
    <h5 v-else-if="level === 5">
      <slot></slot>
    </h5>
    <h6 v-else-if="level === 6">
      <slot></slot>
    </h6>
  `</span>,
  <span class="hljs-attr">props</span>: &#123;
    <span class="hljs-attr">level</span>: &#123;
      <span class="hljs-attr">type</span>: <span class="hljs-built_in">Number</span>,
      <span class="hljs-attr">required</span>: <span class="hljs-literal">true</span>
    &#125;
  &#125;
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>虽然模板在大多数组件中都非常好用，但是显然在这里它就不合适了。那么，我们来尝试使用 render 函数重写上面的例子：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> &#123; createApp, h &#125; = Vue

<span class="hljs-keyword">const</span> app = createApp(&#123;&#125;)

app.component(<span class="hljs-string">'anchored-heading'</span>, &#123;
  <span class="hljs-function"><span class="hljs-title">render</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">return</span> h(
      <span class="hljs-string">'h'</span> + <span class="hljs-built_in">this</span>.level, <span class="hljs-comment">// tag name</span>
      &#123;&#125;, <span class="hljs-comment">// props/attributes</span>
      <span class="hljs-built_in">this</span>.$slots.default() <span class="hljs-comment">// array of children</span>
    )
  &#125;,
  <span class="hljs-attr">props</span>: &#123;
    <span class="hljs-attr">level</span>: &#123;
      <span class="hljs-attr">type</span>: <span class="hljs-built_in">Number</span>,
      <span class="hljs-attr">required</span>: <span class="hljs-literal">true</span>
    &#125;
  &#125;
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-6">jsx</h2>
<p>这样写渲染函数有点痛苦，有没有更接近模板的写法呢，vue提供了一个babel-plugin-jsx babel插件来让vue支持jsx写法</p>
<p>我这边使用的vuecli创建的vue3 + ts项目，脚手架已经集成了jsx和ts的相关依赖</p>
<h3 data-id="heading-7">在vue3中编写jsx的两种方式</h3>
<p>直接将文件后缀名从vue改成tsx或者jsx</p>
<p>在vue3中，可以直接使用render选项编写</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">import</span> &#123; defineComponent &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">"vue"</span>;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> defineComponent(&#123;
  <span class="hljs-attr">name</span>: <span class="hljs-string">"Jsx"</span>,
  <span class="hljs-function"><span class="hljs-title">render</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">return</span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>我是一个div<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>;
  &#125;,
&#125;);

<span class="copy-code-btn">复制代码</span></code></pre>
<p>也可以在setup中返回</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">import</span> &#123; defineComponent &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">"vue"</span>;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> defineComponent(&#123;
  <span class="hljs-attr">name</span>: <span class="hljs-string">"Jsx"</span>,
  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>我是div<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>;
  &#125;,
&#125;);

<span class="copy-code-btn">复制代码</span></code></pre>
<p>两种方式都可以，具体看个人习惯，setup中访问不到this，但是render中可以通过this访问当前vue实例</p>
<h3 data-id="heading-8">用法</h3>
<ul>
<li>
<p>class绑定，和react的jsx绑定的有区别，react中使用className，vue中使用class</p>
<pre><code class="hljs language-tsx copyable" lang="tsx"> <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
   <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span> <span class="hljs-attr">class</span>=<span class="hljs-string">"test"</span>></span>我是div<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>;
 &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>style绑定</p>
<pre><code class="hljs language-tsx copyable" lang="tsx">  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span> <span class="hljs-attr">style</span>=<span class="hljs-string">&#123;&#123;</span> <span class="hljs-attr">color:</span> "<span class="hljs-attr">red</span>" &#125;&#125;></span>我是div<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>;
  &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>props绑定</p>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-comment">// 父组件</span>
<span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span> <span class="hljs-attr">style</span>=<span class="hljs-string">&#123;&#123;</span> <span class="hljs-attr">color:</span> "<span class="hljs-attr">red</span>" &#125;&#125;></span>
        <span class="hljs-tag"><<span class="hljs-name">span</span>></span>我是父组件<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">Mycom</span> <span class="hljs-attr">msg</span>=<span class="hljs-string">&#123;</span>"我是父组件传的值"&#125; /></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
 );
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-comment">// 子组件，setup的第一个参数，可以获取props里的值</span>
  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params">props</span>)</span> &#123;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>我是子组件&#123;props.msg&#125;<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>;
  &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>事件绑定</p>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">eventClick</span>(<span class="hljs-params"></span>) </span>&#123;
      <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"点击"</span>);
    &#125;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">onClick</span>=<span class="hljs-string">&#123;eventClick&#125;</span>></span>按钮<span class="hljs-tag"></<span class="hljs-name">button</span>></span></span>;
&#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>组件自定义事件</p>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-comment">// 子组件</span>
<span class="hljs-keyword">import</span> &#123; defineComponent &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">"vue"</span>;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> defineComponent(&#123;
  <span class="hljs-attr">name</span>: <span class="hljs-string">"Mycom"</span>,
  <span class="hljs-attr">emits</span>: [<span class="hljs-string">"event"</span>],
  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params">props, &#123; emit &#125;</span>)</span> &#123;
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">sendData</span>(<span class="hljs-params"></span>) </span>&#123;
      emit(<span class="hljs-string">"event"</span>, <span class="hljs-string">"子组件传递的数据"</span>);
    &#125;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">span</span>></span>自定义事件<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">onClick</span>=<span class="hljs-string">&#123;sendData&#125;</span>></span>传递数据<span class="hljs-tag"></<span class="hljs-name">button</span>></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
    );
  &#125;,
&#125;);
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-comment">// 父组件</span>
<span class="hljs-comment">// @ts-nocheck</span>
<span class="hljs-comment">// 这样写在jsx中没问题，但是在tsx中会报ts类型错误，所以我在上面忽略了当前文件ts监测@ts-nocheck</span>
<span class="hljs-keyword">import</span> &#123; defineComponent &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">"vue"</span>;
<span class="hljs-keyword">import</span> Mycom <span class="hljs-keyword">from</span> <span class="hljs-string">"./mycom"</span>;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> defineComponent(&#123;
  <span class="hljs-attr">name</span>: <span class="hljs-string">"Jsx"</span>,
  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getSon</span>(<span class="hljs-params">msg: <span class="hljs-built_in">string</span></span>) </span>&#123;
      <span class="hljs-built_in">console</span>.log(msg);
    &#125;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">Mycom</span> <span class="hljs-attr">onEvent</span>=<span class="hljs-string">&#123;getSon&#125;</span> /></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
    );
  &#125;,
&#125;);

<span class="copy-code-btn">复制代码</span></code></pre>
<p>也可以这样解决ts类型报错</p>
<pre><code class="hljs language-tsx copyable" lang="tsx">  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getSon</span>(<span class="hljs-params">msg: <span class="hljs-built_in">string</span></span>) </span>&#123;
      <span class="hljs-built_in">console</span>.log(msg);
    &#125;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">Mycom</span> &#123;<span class="hljs-attr">...</span>&#123; <span class="hljs-attr">onEvent:</span> <span class="hljs-attr">getSon</span> &#125;&#125; /></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
    );
  &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>插槽</p>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-comment">// 父组件</span>
<span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">const</span> slots = &#123;
      <span class="hljs-attr">test</span>: <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>具名插槽<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>,
      <span class="hljs-keyword">default</span>: <span class="hljs-function">() =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>默认插槽<span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>,
    &#125;;
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">Mycom</span> <span class="hljs-attr">v-slots</span>=<span class="hljs-string">&#123;slots&#125;</span>></span><span class="hljs-tag"></<span class="hljs-name">Mycom</span>></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
    );
&#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-tsx copyable" lang="tsx"><span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params">props, &#123; slots &#125;</span>)</span> &#123;
<span class="hljs-comment">// 子组件</span>
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">span</span>></span>插槽<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
        &#123;slots.default?.()&#125;
        &#123;slots.test?.()&#125;
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
    );
  &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>指令，v-if，v-for等指令在jsx中无法使用，jsx只支持v-model和v-show指令</p>
<pre><code class="hljs language-tsx copyable" lang="tsx">  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">const</span> inputData = ref(<span class="hljs-string">""</span>);
    <span class="hljs-keyword">return</span> <span class="hljs-function">() =></span> (
      <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">span</span> <span class="hljs-attr">v-show</span>=<span class="hljs-string">&#123;true&#125;</span>></span>显示<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">span</span> <span class="hljs-attr">v-show</span>=<span class="hljs-string">&#123;false&#125;</span>></span>隐藏<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">input</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"text"</span> <span class="hljs-attr">v-model</span>=<span class="hljs-string">&#123;inputData.value&#125;</span> /></span>
        <span class="hljs-tag"><<span class="hljs-name">span</span>></span>&#123;inputData.value&#125;<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
    );
&#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
</ul>
<h2 data-id="heading-9">最后</h2>
<p>话不多说，我先打开vant源码,准备开启我的第一个组件源码阅读 src =>button=>button.tsx</p>
<h2 data-id="heading-10">参考</h2>
<ul>
<li><a href="https://link.juejin.cn/?target=https%3A%2F%2Fv3.cn.vuejs.org%2Fguide%2Frender-function.html" target="_blank" rel="nofollow noopener noreferrer" title="https://v3.cn.vuejs.org/guide/render-function.html" ref="nofollow noopener noreferrer">vue渲染函数</a></li>
<li><a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fvuejs%2Fjsx-next%23installation" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/vuejs/jsx-next#installation" ref="nofollow noopener noreferrer">vuejsx文档</a></li>
<li><a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fvuejs%2Fvue-next%2Fissues%2F1553" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/vuejs/vue-next/issues/1553" ref="nofollow noopener noreferrer">issues</a></li>
</ul></div>  
</div>
            