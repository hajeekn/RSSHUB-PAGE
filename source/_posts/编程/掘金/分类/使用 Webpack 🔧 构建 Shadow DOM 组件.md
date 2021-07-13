
---
title: '使用 Webpack 🔧 构建 Shadow DOM 组件'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=9301'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 01:46:20 GMT
thumbnail: 'https://picsum.photos/400/300?random=9301'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">前前言</h1>
<p>本文来自推啊前端团队 <a href="https://juejin.cn/user/3570835597038638" target="_blank" title="https://juejin.cn/user/3570835597038638">Winter97</a> 同学，主要介绍如何使用 Webpack 构建工具解决编写 Shadow DOM 组件的一些开发痛点。阅读时长在5-8分钟左右。如有错误，欢迎在评论区指出👏</p>
<h1 data-id="heading-1">前言</h1>
<p><code>Shadow DOM</code>（影子DOM）是 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FWeb_Components" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/en-US/docs/Web/Web_Components" ref="nofollow noopener noreferrer"><code>Web Components</code></a> 主要技术组成之一，可以将一个隐藏的、独立的 DOM 附加到一个元素上<sup>[1]</sup>，结合 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FWeb_Components%2FUsing_custom_elements" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements" ref="nofollow noopener noreferrer">Custom elements（自定义元素）</a>，可以创建一个与外界隔离的 Web 组件（以下简称为 Shadow DOM 组件），不用担心与页面的其他部分发生冲突，可复用性高。其基本概念与基本使用方式可以从 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FWeb_Components%2FUsing_shadow_DOM" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/Using_shadow_DOM" ref="nofollow noopener noreferrer">MDN 文档</a>上获知，在此不再赘述。</p>
<p>本文主要探讨开发一个复杂 Shadow DOM 组件过程中的痛点，以及提供一种思路，用以降低编写 Shadow DOM 组件的复杂度。</p>
<h1 data-id="heading-2">开发痛点</h1>
<p>沿用MDN上的 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FWeb_Components%2FUsing_shadow_DOM%23%25E7%25BC%2596%25E5%2586%2599%25E7%25AE%2580%25E5%258D%2595%25E7%25A4%25BA%25E4%25BE%258B" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/Using_shadow_DOM#%E7%BC%96%E5%86%99%E7%AE%80%E5%8D%95%E7%A4%BA%E4%BE%8B" ref="nofollow noopener noreferrer">popup-info-box🌰</a>，可以看出手撸一个 Shadow DOM 复杂度主要体现在以下几个方面：</p>
<h2 data-id="heading-3">1. 创建 Shadow DOM 结构</h2>
<p>Shadow DOM 的创建是通过<a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FAPI%2FElement%2FattachShadow" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/API/Element/attachShadow" ref="nofollow noopener noreferrer"><code>Element.attachShadow()</code></a>来挂载一个 Shadow DOM，并返回对 ShadowRoot 的引用。之后像操作普通 DOM 一样为 shadow root 节点添加子节点、设置属性等。创建 Shadow DOM 结构只需对该 ShadowRoot 对象进行 appendChild 操作：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-comment">// 创建 shadow root</span>
<span class="hljs-keyword">var</span> shadow = <span class="hljs-built_in">this</span>.attachShadow(&#123;<span class="hljs-attr">mode</span>: <span class="hljs-string">'open'</span>&#125;);
<span class="hljs-comment">// 创建 span</span>
<span class="hljs-keyword">var</span> wrapper = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'span'</span>);
wrapper.setAttribute(<span class="hljs-string">'class'</span>,<span class="hljs-string">'wrapper'</span>);
<span class="hljs-keyword">var</span> icon = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'span'</span>);
icon.setAttribute(<span class="hljs-string">'class'</span>,<span class="hljs-string">'icon'</span>);
icon.setAttribute(<span class="hljs-string">'tabindex'</span>, <span class="hljs-number">0</span>);
<span class="hljs-keyword">var</span> info = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'span'</span>);
info.setAttribute(<span class="hljs-string">'class'</span>,<span class="hljs-string">'info'</span>);

<span class="hljs-comment">// 获取属性的内容并将内容添加到 info 元素内</span>
<span class="hljs-keyword">var</span> text = <span class="hljs-built_in">this</span>.getAttribute(<span class="hljs-string">'text'</span>);
info.textContent = text;

<span class="hljs-comment">// 插入 icon</span>
<span class="hljs-keyword">var</span> imgUrl;
<span class="hljs-keyword">if</span>(<span class="hljs-built_in">this</span>.hasAttribute(<span class="hljs-string">'img'</span>)) &#123;
  imgUrl = <span class="hljs-built_in">this</span>.getAttribute(<span class="hljs-string">'img'</span>);
&#125; <span class="hljs-keyword">else</span> &#123;
  imgUrl = <span class="hljs-string">'img/default.png'</span>;
&#125;
<span class="hljs-keyword">var</span> img = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'img'</span>);
img.src = imgUrl;
icon.appendChild(img);

<span class="hljs-comment">// 将所创建的元素添加到 Shadow DOM 上</span>
shadow.appendChild(wrapper);
wrapper.appendChild(icon);
wrapper.appendChild(info);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>像这样命令式地批量 appendChild 需编写大量代码，如果仅是静态 HTML 结构，另一种更佳的方式是创建一个根结点，只执行一次 appendChild 操作：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">const</span> template = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'template'</span>);
template.innerHTML = <span class="hljs-string">`
  <span class="wrapper"></span>
  <span class="icon" tabindex="0"></span>
  <span class="info"></span>
`</span>;

shadow.appendChild(template.content.cloneNode(<span class="hljs-literal">true</span>));
<span class="copy-code-btn">复制代码</span></code></pre>
<p>借助 innerHTML 和模板字符串，可以声明式地描述 Shadow DOM 的结构，相较前者可阅读性更好。但由于其仅是字符串，编辑器不会为其语法高亮，当 DOM 结构变得复杂的时候，可维护性与可阅读性将会变差。</p>
<h2 data-id="heading-4">2. 为Shadow DOM添加样式</h2>
<p>为 Shadow DOM 添加样式，可以创建<code><style></code>元素，并加入一些样式：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-comment">// 为 shadow DOM 添加一些 CSS 样式</span>
<span class="hljs-keyword">var</span> style = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'style'</span>);

style.textContent = <span class="hljs-string">`
.wrapper &#123;
  position: relative;
&#125;

.info &#123;
  font-size: 0.8rem;
  width: 200px;
  display: inline-block;
  border: 1px solid black;
  padding: 10px;
  background: white;
  border-radius: 10px;
  opacity: 0;
  transition: 0.6s all;
  position: absolute;
  bottom: 20px;
  left: 10px;
  z-index: 3;
&#125;

img &#123;
  width: 1.2rem;
&#125;

.icon:hover + .info, .icon:focus + .info &#123;
  opacity: 1;
&#125;`</span>;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>然后，依然是通过 appendChild 操作添加到 Shadow root 上：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript">shadow.appendChild(style);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这与前面提到的创建 DOM 结构的方式几乎一模一样，在可维护性与可阅读性上得不到保证，并且不支持 CSS 预处理器，开发效率上大打折扣。</p>
<p>除了行内<code><style></code>元素为 Shadow DOM 添加样式，也可以通过<code><link></code>标签引用外部样式表来替代行内样式：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-comment">// 将外部引用的样式添加到 Shadow DOM 上</span>
<span class="hljs-keyword">const</span> linkElem = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'link'</span>);
linkElem.setAttribute(<span class="hljs-string">'rel'</span>, <span class="hljs-string">'stylesheet'</span>);
linkElem.setAttribute(<span class="hljs-string">'href'</span>, <span class="hljs-string">'style.css'</span>);

<span class="hljs-comment">// 将所创建的元素添加到 Shadow DOM 上</span>

shadow.appendChild(linkElem);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>但因为<code><link></code>元素不会打断 shadow root 的绘制, 因此在加载样式表时可能会出现未添加样式内容（FOUC），导致闪烁<sup>[1]</sup>。引用外部样式在一定程度上也会导致 Shadow DOM 的表现依赖于外部，从而失去封装的意义，独立性也得不到体现。因此还是推荐使用行内<code><style></code>样式。</p>
<h1 data-id="heading-5">解决方法</h1>
<p>为了解决以上痛点，笔者决定采用 <code>Webpack</code> 来帮助构建Shadow DOM组件。总体思路是：采用传统的 Web 开发思维，将结构（<code>HTML</code>）和表现（<code>CSS</code>）分离，然后将其组装成我们需要的Shadow DOM组件。在正式改造前，先创建一个Webpack项目：</p>
<pre><code class="hljs language-shell copyable" lang="shell">npm init
npm install --save-dev webpack
npm install --save-dev webpack-cli
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-6">1. 使用html-loader分离Shadow DOM结构</h2>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fwebpack.js.org%2Floaders%2Fhtml-loader%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://webpack.js.org/loaders/html-loader/" ref="nofollow noopener noreferrer">html-loader</a>是一个 Webpack 的Loader，可以将 HTML 导出为字符串，在入口文件中将其引入，赋值给 innerHTML 以此组成 Shadow DOM 结构。
首先，安装依赖：</p>
<pre><code class="hljs language-shell copyable" lang="shell">npm install --save-dev html-loader
<span class="copy-code-btn">复制代码</span></code></pre>
<p>接着在 Webpack 配置文件中配置该插件。因为 innerHTML 可以设置 HTML 语法表示的元素的后代，我们不需要为此创建完整的HTML结构，甚至是否有根结点也不是硬性要求。Webpack 配置如下：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// wepback.config.js</span>
<span class="hljs-built_in">module</span>.exports = &#123;
  <span class="hljs-attr">mode</span>: <span class="hljs-string">'production'</span>,
  <span class="hljs-attr">entry</span>: <span class="hljs-string">'./src/index.js'</span>,
  <span class="hljs-attr">output</span>: &#123;
    <span class="hljs-attr">filename</span>: <span class="hljs-string">'popup-info.js'</span>
  &#125;,
  <span class="hljs-attr">module</span>: &#123;
    <span class="hljs-attr">rules</span>: [
      &#123;
        <span class="hljs-attr">test</span>: <span class="hljs-regexp">/\.html$/i</span>,
        loader: <span class="hljs-string">'html-loader'</span>
      &#125;,
    ],
  &#125;,
&#125;;

<span class="copy-code-btn">复制代码</span></code></pre>
<p>指定 mode 为 production，html-loader 会在生产模式下对 HTML 进行压缩。在 src 目录下新建 <code>index.js</code> 和 <code>template.html</code> 文件，分别作为入口文件与 Shadow DOM 结构描述文件：</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-comment"><!-- template.html --></span>
<span class="hljs-tag"><<span class="hljs-name">span</span> <span class="hljs-attr">class</span>=<span class="hljs-string">"wrapper"</span>></span>
  <span class="hljs-tag"><<span class="hljs-name">span</span> <span class="hljs-attr">class</span>=<span class="hljs-string">"icon"</span> <span class="hljs-attr">tabindex</span>=<span class="hljs-string">"0"</span>></span><span class="hljs-tag"></<span class="hljs-name">span</span>></span>
  <span class="hljs-tag"><<span class="hljs-name">span</span> <span class="hljs-attr">class</span>=<span class="hljs-string">"info"</span>></span><span class="hljs-tag"></<span class="hljs-name">span</span>></span>
<span class="hljs-tag"></<span class="hljs-name">span</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// index.js</span>
<span class="hljs-keyword">import</span> html <span class="hljs-keyword">from</span> <span class="hljs-string">'./template.html'</span>;

<span class="hljs-keyword">const</span> template = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'template'</span>);
template.innerHTML = html

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">PopUpInfo</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">HTMLElement</span> </span>&#123;
  <span class="hljs-function"><span class="hljs-title">constructor</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-built_in">super</span>();
    <span class="hljs-built_in">this</span>.attachShadow(&#123; <span class="hljs-attr">mode</span>: <span class="hljs-string">'open'</span> &#125;);
    <span class="hljs-built_in">this</span>.shadowRoot.appendChild(template.content.cloneNode(<span class="hljs-literal">true</span>));
  &#125;
&#125;

customElements.define(<span class="hljs-string">'popup-info'</span>, PopUpInfo);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这样，就将结构分离了出来，并获得了编辑器语法高亮加持。在 <code>package.json</code> 中的 <code>scripts</code> 中添加打包脚本：</p>
<pre><code class="hljs language-json copyable" lang="json"><span class="hljs-string">"build"</span>: <span class="hljs-string">"webpack  --config webpack.config.js"</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>在项目根目录下执行 <code>npm run build</code> 获得打包后的 <code>popup-info.js</code> 文件，在页面中引入：</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">popup-info</span>></span><span class="hljs-tag"></<span class="hljs-name">popup-info</span>></span>
<span class="hljs-tag"><<span class="hljs-name">script</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"./dist/popup-info.js"</span>></span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>检查 Element：</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/325ec1c309134110a412cd7b148c23e5~tplv-k3u1fbpfcp-watermark.image" alt="截屏2021-06-21 上午12.26.38.png" loading="lazy" referrerpolicy="no-referrer">
但这仅仅是创建了静态结构，对于一些动态行为，依然需要编写代码进行控制：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">PopUpInfo</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">HTMLElement</span> </span>&#123;
  <span class="hljs-function"><span class="hljs-title">constructor</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-built_in">super</span>();
    <span class="hljs-keyword">const</span> shadowRoot = <span class="hljs-built_in">this</span>.attachShadow(&#123; <span class="hljs-attr">mode</span>: <span class="hljs-string">'open'</span> &#125;);
    <span class="hljs-comment">// 获取属性的内容并将内容添加到 info 元素内</span>
    shadowRoot.appendChild(template.content.cloneNode(<span class="hljs-literal">true</span>));
    <span class="hljs-keyword">const</span> text = <span class="hljs-built_in">this</span>.getAttribute(<span class="hljs-string">'text'</span>);
    shadowRoot.querySelector(<span class="hljs-string">'.info'</span>).textContent = text;
    <span class="hljs-comment">// 插入 icon</span>
    <span class="hljs-keyword">let</span> imgUrl;
    <span class="hljs-keyword">if</span> (<span class="hljs-built_in">this</span>.hasAttribute(<span class="hljs-string">'img'</span>)) &#123;
      imgUrl = <span class="hljs-built_in">this</span>.getAttribute(<span class="hljs-string">'img'</span>);
    &#125; <span class="hljs-keyword">else</span> &#123;
      imgUrl = <span class="hljs-string">'img/default.png'</span>;
    &#125;
    <span class="hljs-keyword">const</span> img = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'img'</span>);
    img.src = imgUrl;
    shadowRoot.querySelector(<span class="hljs-string">'.icon'</span>).appendChild(img);
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>修改 <code><popup-info></code> 元素：</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">popup-info</span> <span class="hljs-attr">img</span>=<span class="hljs-string">"img/alt.png"</span> <span class="hljs-attr">text</span>=<span class="hljs-string">"Your card validation code (CVC) is an extra security feature — it is the last 3 or 4 numbers on the back of your card."</span>></span><span class="hljs-tag"></<span class="hljs-name">popup-info</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>再次检查 Element：</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dcb800eaa6ee4d4a81856ae0018bcecd~tplv-k3u1fbpfcp-watermark.image" alt="截屏2021-06-21 上午12.30.18.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-7">2. 分离样式，使用CSS预处理器</h2>
<p>处理完结构，再看样式如何分离。从前所述，为 Shadow DOM 添加样式，需要创建 style 元素，并使用普通 CSS 文本填充，在这种模式下无法借助 CSS 预处理器，并且编辑器无法为其语法高亮。参考了文章：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fmedium.com%2Fswlh%2Fweb-components-with-shadow-dom-and-sass-f780ad23dd90" target="_blank" rel="nofollow noopener noreferrer" title="https://medium.com/swlh/web-components-with-shadow-dom-and-sass-f780ad23dd90" ref="nofollow noopener noreferrer">Web Components with Shadow DOM and Sass.</a><sup>[2]</sup>，下面使用 Sass 来编写 Shadow DOM 组件样式。</p>
<p>首先安装 raw-loader 和 sass-loader：</p>
<pre><code class="hljs language-shell copyable" lang="shell">npm install --save-dev raw-loader
npm install --save-dev sass-loader
npm install --save-dev node-sass
<span class="copy-code-btn">复制代码</span></code></pre>
<p>修改 webpack.config.js，添加 rule：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// webpack.config.js</span>
<span class="hljs-keyword">const</span> path = <span class="hljs-built_in">require</span>(<span class="hljs-string">'path'</span>);

<span class="hljs-built_in">module</span>.exports = &#123;
  <span class="hljs-attr">mode</span>: <span class="hljs-string">'production'</span>,
  <span class="hljs-attr">entry</span>: <span class="hljs-string">'./src/index.js'</span>,
  <span class="hljs-attr">output</span>: &#123;
    <span class="hljs-attr">filename</span>: <span class="hljs-string">'popup-info.js'</span>,
  &#125;,
  <span class="hljs-attr">module</span>: &#123;
    <span class="hljs-attr">rules</span>: [&#123;
        <span class="hljs-attr">test</span>: <span class="hljs-regexp">/\.html$/i</span>,
        loader: <span class="hljs-string">'html-loader'</span>,
        <span class="hljs-attr">options</span>: &#123;
          <span class="hljs-attr">minimize</span>: <span class="hljs-literal">true</span>,
          <span class="hljs-attr">sources</span>: <span class="hljs-literal">false</span>
        &#125;
      &#125;,
      &#123;
        <span class="hljs-attr">test</span>: <span class="hljs-regexp">/\.scss$/</span>,
        use: [
          <span class="hljs-string">'raw-loader'</span>,
          &#123;
            <span class="hljs-attr">loader</span>: <span class="hljs-string">'sass-loader'</span>,
            <span class="hljs-attr">options</span>: &#123;
              <span class="hljs-attr">sassOptions</span>: &#123;
                <span class="hljs-attr">includePaths</span>: [path.resolve(__dirname, <span class="hljs-string">'node_modules'</span>)]
              &#125;
            &#125;
          &#125;
        ]
      &#125;
    ],
  &#125;,
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>接着就可以创建单独的样式文件 <code>popup-info.scss</code> ：</p>
<pre><code class="hljs language-scss copyable" lang="scss"><span class="hljs-variable">$img-width</span>: <span class="hljs-number">1.2rem</span>;

<span class="hljs-selector-class">.wrapper</span> &#123;
  <span class="hljs-attribute">position</span>: relative;
&#125;

<span class="hljs-selector-class">.info</span> &#123;
  <span class="hljs-attribute">font-size</span>: <span class="hljs-number">0.8rem</span>;
  <span class="hljs-attribute">width</span>: <span class="hljs-number">200px</span>;
  <span class="hljs-attribute">display</span>: inline-block;
  <span class="hljs-attribute">border</span>: <span class="hljs-number">1px</span> solid black;
  <span class="hljs-attribute">padding</span>: <span class="hljs-number">10px</span>;
  <span class="hljs-attribute">background</span>: white;
  <span class="hljs-attribute">border-radius</span>: <span class="hljs-number">10px</span>;
  <span class="hljs-attribute">opacity</span>: <span class="hljs-number">0</span>;
  <span class="hljs-attribute">transition</span>: <span class="hljs-number">0.6s</span> all;
  <span class="hljs-attribute">position</span>: absolute;
  <span class="hljs-attribute">bottom</span>: <span class="hljs-number">20px</span>;
  <span class="hljs-attribute">left</span>: <span class="hljs-number">10px</span>;
  <span class="hljs-attribute">z-index</span>: <span class="hljs-number">3</span>;
&#125;

<span class="hljs-selector-tag">img</span> &#123;
  <span class="hljs-attribute">width</span>: <span class="hljs-variable">$img-width</span>;
&#125;

<span class="hljs-selector-class">.icon</span><span class="hljs-selector-pseudo">:hover</span>+<span class="hljs-selector-class">.info</span>,
<span class="hljs-selector-class">.icon</span><span class="hljs-selector-pseudo">:focus</span>+<span class="hljs-selector-class">.info</span> &#123;
  <span class="hljs-attribute">opacity</span>: <span class="hljs-number">1</span>;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>在入口文件中引入：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// index.js</span>
<span class="hljs-keyword">import</span> styleText <span class="hljs-keyword">from</span> <span class="hljs-string">'./popup-info.scss'</span>;

<span class="hljs-keyword">const</span> style = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'style'</span>);
style.appendChild(<span class="hljs-built_in">document</span>.createTextNode(styleText));

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">PopUpInfo</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">HTMLElement</span> </span>&#123;
  <span class="hljs-function"><span class="hljs-title">constructor</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-built_in">super</span>();
    <span class="hljs-keyword">const</span> shadowRoot = <span class="hljs-built_in">this</span>.attachShadow(&#123; <span class="hljs-attr">mode</span>: <span class="hljs-string">'open'</span> &#125;);
    shadowRoot.appendChild(style);
    <span class="hljs-comment">// ...</span>
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>再次检查 Element：</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f652bde9329405b9cb596ad95e2f6b8~tplv-k3u1fbpfcp-watermark.image" alt="截屏2021-06-21 上午12.32.44.png" loading="lazy" referrerpolicy="no-referrer">
<code><style></code>元素已添加上，并且只在 Shadow DOM 内部生效。至此，便完成了一个 Shadow DOM 组件的编写。</p>
<h1 data-id="heading-8">思考</h1>
<p>上述流程的基本思想是将结构和表现分离，再组装起来，在一定程度上提高了组件的可维护性。但是对自定义元素属性的处理以及为 Shadow DOM 添加事件监听器依然需要在构造器中进行。并且由于分离了 DOM 结构和 CSS 样式，关注点也随之分离，开发过程中需要在不同文件来回切换。参考 Vue SFC，一个更为合理的组件结构应该如下所示：</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">template</span>></span>
...
<span class="hljs-tag"></<span class="hljs-name">template</span>></span>

<span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="handlebars"><span class="xml">
...
<span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="handlebars"><span class="xml">

<span class="hljs-tag"><<span class="hljs-name">style</span>></span>
...
<span class="hljs-tag"></<span class="hljs-name">style</span>></span>
</span></span></span></span><span class="copy-code-btn">复制代码</span></code></pre>
<p>以这样的结构编写 Shadow DOM 组件，便需要实现一个能够导出 Shadow DOM 组件的 Webpack Loader，以满足需求。等有精力的时候再研究下。🧑🏻‍💻</p>
<h1 data-id="heading-9">参考文献</h1>
<p>[1] <a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FWeb_Components%2FUsing_shadow_DOM" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM" ref="nofollow noopener noreferrer">Using shadow DOM - Web Components | MDN</a></p>
<p>[2] <a href="https://link.juejin.cn/?target=https%3A%2F%2Fmedium.com%2Fswlh%2Fweb-components-with-shadow-dom-and-sass-f780ad23dd90" target="_blank" rel="nofollow noopener noreferrer" title="https://medium.com/swlh/web-components-with-shadow-dom-and-sass-f780ad23dd90" ref="nofollow noopener noreferrer">Web Components with Shadow DOM and Sass.</a></p>
<blockquote>
<p>投稿来源：<a href="https://juejin.cn/post/6975931284145045517" target="_blank" title="https://juejin.cn/post/6975931284145045517">juejin.cn/post/697593…</a></p>
</blockquote></div>  
</div>
            