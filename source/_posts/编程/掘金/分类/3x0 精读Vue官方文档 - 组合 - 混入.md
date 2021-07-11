
---
title: '3x0 精读Vue官方文档 - 组合 - 混入'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=3563'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 01:07:08 GMT
thumbnail: 'https://picsum.photos/400/300?random=3563'
---

<div>   
<div class="markdown-body"><style>@charset "UTF-8";.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1:first-child,.markdown-body h2:first-child,.markdown-body h3:first-child,.markdown-body h4:first-child,.markdown-body h5:first-child,.markdown-body h6:first-child&#123;margin-top:-1.5rem;margin-bottom:1rem&#125;.markdown-body h1:before,.markdown-body h2:before,.markdown-body h3:before,.markdown-body h4:before,.markdown-body h5:before,.markdown-body h6:before&#123;content:"#";display:inline-block;color:#3eaf7c;padding-right:.23em&#125;.markdown-body h1&#123;position:relative;font-size:2.5rem;margin-bottom:5px&#125;.markdown-body h1:before&#123;font-size:2.5rem&#125;.markdown-body h2&#123;padding-bottom:.5rem;font-size:2.2rem;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:1.5rem;padding-bottom:0&#125;.markdown-body h4&#123;font-size:1.25rem&#125;.markdown-body h5&#123;font-size:1rem&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body strong&#123;color:#3eaf7c&#125;.markdown-body img&#123;max-width:100%;border-radius:2px;display:block;margin:auto;border:3px solid rgba(62,175,124,.2)&#125;.markdown-body hr&#123;border:none;border-top:1px solid #3eaf7c;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;overflow-x:auto;padding:.2rem .5rem;margin:0;color:#3eaf7c;font-weight:700;font-size:.85em;background-color:rgba(27,31,35,.05);border-radius:3px&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;border-radius:6px;border:2px solid #3eaf7c&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;font-weight:500;text-decoration:none;color:#3eaf7c&#125;.markdown-body a:active,.markdown-body a:hover&#123;border-bottom:1.5px solid #3eaf7c&#125;.markdown-body a:before&#123;content:"⇲"&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #3eaf7c&#125;.markdown-body thead&#123;background:#3eaf7c;color:#fff;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:rgba(62,175,124,.2)&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:.5rem solid;border-color:#42b983;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body details&#123;outline:none;border:none;border-left:4px solid #3eaf7c;padding-left:10px;margin-left:4px&#125;.markdown-body details summary&#123;cursor:pointer;border:none;outline:none;background:#fff;margin:0 -17px&#125;.markdown-body details summary::-webkit-details-marker&#123;color:#3eaf7c&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body ol li::marker&#123;color:#3eaf7c&#125;.markdown-body ul li&#123;list-style:none&#125;.markdown-body ul li:before&#123;content:"•";margin-right:4px;color:#3eaf7c&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0"><a href="https://juejin.cn/column/6976899977133948965" target="_blank" title="https://juejin.cn/column/6976899977133948965">精读 Vue 官方文档系列</a> 🎉</h2>
<h2 data-id="heading-1">基础</h2>
<p>Mixin（混入）指的是向目标组件中混入能够在多个组件间进行复用的<strong>逻辑</strong>或<strong>功能</strong>。</p>
<p>简单粗暴的理解，可以将“混入对象”等同为组件的纯逻辑部分（SFC 中的 <code><script></code> 部分），然后将其抽离到一个独立的文件中，等待分发到别的组件中进行混合，以实现功能的复用。</p>
<p>混入对象可以包含任意的<strong>组件选项</strong>，这些选项会按照恰当的方式与目标组件的选项进行”混合合并“。</p>
<blockquote>
<p>混入对象中的<strong>方法</strong>与<strong>数据</strong>可以在多个组件中共用但是不能共享。</p>
</blockquote>
<p>一个简单的混入对象：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">//src/mixins/sayHelloMixin.js</span>
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> &#123;
    <span class="hljs-function"><span class="hljs-title">data</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-keyword">return</span> &#123;
            <span class="hljs-attr">message</span>: <span class="hljs-string">'hello!'</span>
        &#125;
    &#125;,
    <span class="hljs-function"><span class="hljs-title">created</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.message)
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>导入 <code>sayHelloMixin</code>，然后传入到目标组件的 <code>mixins</code> 选项中进行局部注册。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> sayHelloMixin <span class="hljs-keyword">from</span> <span class="hljs-string">"../mixins/sayHello"</span>;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> &#123;
    <span class="hljs-attr">name</span>:<span class="hljs-string">'Hello'</span>,
    <span class="hljs-attr">mixins</span>:[sayHelloMixin]
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>或者使用 <code>Vue.extend()</code> 方法基于混入对象创建一个完整的全新的组件对象。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> sayHelloMixin <span class="hljs-keyword">from</span> <span class="hljs-string">"../mixins/sayHello"</span>;
<span class="hljs-keyword">import</span> Vue <span class="hljs-keyword">from</span> <span class="hljs-string">'vue'</span>
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> Vue.extend(&#123;<span class="hljs-attr">mixins</span>: [sayHelloMixin]&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-2">选项合并</h2>
<p>混入对象与目标组件混合的规则如下：</p>
<ul>
<li>数据方法会进行递归合并数据的键值对，如果键发生冲突，则优先使用组件中的数据。</li>
<li>钩子函数会被合并成一个数组，因此都将被调用，注意的是混入对象的钩子在组件自身的钩子之前执行。</li>
<li>值为对象的组件选项会进行合并，对象键名冲突时，取组件对象的键值对。</li>
</ul>
<h2 data-id="heading-3">全局混入</h2>
<p>使用 <code>Vue.mixin()</code> 方法来注册全局的混入对象。</p>
<blockquote>
<p>应当避免使用全局混入的方式。
这里主要注意采用不同方式注册的混入对象的执行优先级：<code>组件自身选项</code> → <code>局部注册的混入对象</code> → <code>全局注册的混入对象</code></p>
</blockquote>
<h2 data-id="heading-4">自定义选项合并策略</h2>
<p>通过 <code>Vue.config.optionMergeStrategies.[myOption]</code> 可以自定义混入对象与组件对象中某个选项的合并策略。</p>
<p>其中 <code>myOption</code> 是一个占位符，其实际名称应当是要合并的选项名。</p>
<p>对于多数值为对象的选项，可以使用与 <code>methods</code> 相同的合并策略：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> strategies = Vue.config.optionMergeStrategies
strategies.myOption = strategies.methods
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-5">示例说明</h2>
<p>设想，现在有两个组件，<code>Modal</code> 与 <code>Tooltip</code>，虽然它们展现的形式上存在差异，但存在着相同的交互逻辑，例如都有着切换显示隐藏的功能。</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c845c713f3ef4c6a84509a5d2b6a24d3~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>此时，按照<strong>混入</strong>的目标与定义，我们便可以将能复用的功能抽离到一个 <code>mixin</code> 对象中了。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> toggleMixin = &#123;
    <span class="hljs-function"><span class="hljs-title">data</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-keyword">return</span> &#123;
            <span class="hljs-attr">show</span>: <span class="hljs-literal">false</span>
        &#125;
    &#125;,
    <span class="hljs-attr">methods</span>: &#123;
        <span class="hljs-function"><span class="hljs-title">toggle</span>(<span class="hljs-params"></span>)</span> &#123;
            <span class="hljs-built_in">this</span>.show = !<span class="hljs-built_in">this</span>.show;
        &#125;
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>然后分别在 <code>Modal</code> 与 <code>Tooltip</code> 中使用：</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-comment"><!--Modal.vue--></span>
export default &#123;
    name:'Modal',
    mixins:[toggleMixin],
&#125;

<span class="hljs-comment"><!--Tooltip.vue--></span>
export default &#123;
    name:'Modal',
    mixins:[toggleMixin],
&#125;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            