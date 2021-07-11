
---
title: '跟着 underscore.js 写 debounce'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cd464b027a404e3e8dde1e8a8e360722~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 18:56:53 GMT
thumbnail: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cd464b027a404e3e8dde1e8a8e360722~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>在我的观念里，我一直觉得这道题算是比较简单的一道，直到一名面试官问我，你能在 5 分钟内写出一个 bug-free 的、考虑完备的 <code>debounce</code> 函数吗？我瞬间没了自信。</p>
<p>所以，我打算还是写一篇，梳理一下自己的思路。同时也非常推荐看到这篇文章的同学自己写一遍，因为很多设计只看源码并不会理解，但是真正落实到自己写后，才会真正的想通，作者在当时为什么会这么想。</p>
<p>在不看 underscore 源码之前，我自己写的一版可能是这样的。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">debounce</span>(<span class="hljs-params">func,wait = <span class="hljs-number">1500</span></span>) </span>&#123;
  <span class="hljs-keyword">let</span> timeout;

  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">later</span>(<span class="hljs-params"></span>) </span>&#123;
    timeout = <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =></span> &#123;
      func();
      <span class="hljs-built_in">clearTimeout</span>(timeout);
      timeout = <span class="hljs-literal">null</span>;
    &#125;, wait)
  &#125;

  <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">debounced</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">if</span> (timeout) &#123;
      <span class="hljs-built_in">clearTimeout</span>(timeout);
      timeout = <span class="hljs-literal">null</span>;
      later();
    &#125; <span class="hljs-keyword">else</span> &#123;
      later();
    &#125;
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>可能很多同学和我一样，都使用 <code>clearTimeout</code> 去中途中断定时器，但是 <code>_.debounce</code> 却没有，它是怎么做到的？</p>
<p>分析过源码之后，才知道，它是用当前时间戳和上一次触发 <code>debounced</code> 的时间戳做比较来确定的。</p>
<p>我们把上一次的时间戳记作 <code>previous</code>，当前的时间戳记作 <code>now</code>，<code>now - previous</code> 的差值记作 <code>passed</code>。</p>
<p>每次重新触发 <code>debounced</code> 时，<code>previous</code> 的时间戳都会更新，而此时我们计算 <code>passed</code> 的规则也就变化了，此时仅仅通过比较 <code>wait - passed</code> 就能知道要不要执行了。 从而避免了 <code>clearTimeout</code> 这一步。</p>
<p>如果把这个思路应用到我们写的第一版上去，就会变成：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">now</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-keyword">return</span> <span class="hljs-built_in">Date</span>.now();
&#125;

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">debounce</span>(<span class="hljs-params">func,wait = <span class="hljs-number">1500</span></span>) </span>&#123;
  <span class="hljs-keyword">let</span> timeout, previous;

  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">later</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">const</span> passed = now() - previous;
    <span class="hljs-keyword">if</span> (wait > passed) &#123;
      timeout = <span class="hljs-built_in">setTimeout</span>(later, wait - passed);
    &#125; <span class="hljs-keyword">else</span> &#123;
      timeout = <span class="hljs-literal">null</span>;
      func();
    &#125;
  &#125;

  <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">debounced</span>(<span class="hljs-params"></span>) </span>&#123;
    previous = now()
    <span class="hljs-keyword">if</span> (!timeout) &#123;
      timeout = <span class="hljs-built_in">setTimeout</span>(later, wait)
    &#125; 
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>理清楚了这个思路后，剩下的代码相对比较简单，只是一些扩展 API 的代码，相信大家也都能自己看明白，只不过有一行代码刚看会比较懵，我给大家解释一下。</p>
<p>这是它的 <code>later</code> 函数，大家请看倒数第三、四行</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> later = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">var</span> passed = now() - previous;
    <span class="hljs-keyword">if</span> (wait > passed) &#123;
      timeout = <span class="hljs-built_in">setTimeout</span>(later, wait - passed);
    &#125; <span class="hljs-keyword">else</span> &#123;
      timeout = <span class="hljs-literal">null</span>;
      func.apply(context, args);
      <span class="hljs-comment">// This check is needed because `func` can recursively invoke `debounced`.</span>
      <span class="hljs-keyword">if</span> (!timeout) args = context = <span class="hljs-literal">null</span>; <span class="hljs-comment">// 这一行。</span>
    &#125;
  &#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>我们上一步不是让 <code>timeout = null</code> 了吗，怎么下一步还要有 <code>if (!timeout)</code> 这个判断？这个肯定成立呀！</p>
<p>大家觉得这个判断不必要的原因可能是：这一段并不是异步代码，执行了上一语句肯定就直接执行下一条语句了，所以，这个判断没有必要。</p>
<p>我看过其他同学的源码解析，好像都没有比较详细的说明这一个过程，甚至有些同学说这行代码没有必要，其实是很有必要的。</p>
<p>下面我就来带大家分析一下这个过程。</p>
<p>我们只要举一个反例就好了，下面我们来设计一个例子：</p>
<p>我们写一个简单的递归函数：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>;
<span class="hljs-keyword">const</span> debouncedFn = debounce(<span class="hljs-function">() =></span> &#123;
  <span class="hljs-keyword">if</span> (i >= <span class="hljs-number">10</span>) &#123;
    <span class="hljs-keyword">return</span>;
  &#125;
  i++;
  debouncedFn()
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>同时把 <code>later</code> 打个标记：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">later</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">const</span> passed = now() - previous;
    <span class="hljs-keyword">if</span> (wait > passed) &#123;
      timeout = <span class="hljs-built_in">setTimeout</span>(later, wait - passed);
    &#125; <span class="hljs-keyword">else</span> &#123;
      timeout = <span class="hljs-literal">null</span>;
      func();
      <span class="hljs-keyword">if</span> (!timeout) &#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'调用这里-1'</span>)
      &#125; <span class="hljs-keyword">else</span> &#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'调用这里-2'</span>)
      &#125;
    &#125;
  &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cd464b027a404e3e8dde1e8a8e360722~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>我们惊奇的发现 '调用这里-2' 被调用了 10 次。</p>
<p>这时候我们就发现了这个判断的必要性，因为我们 <code>debounce</code> 的第一个参数 <code>func</code> ，也可能递归的调用 <code>func</code> 的 debounced 版 。如果不加这个判断的话，就会出现无法递归调用的问题。</p>
<p>这一点，如果我不看它的源码，我肯定不会想到还有这种场景。而我不动手写一遍，也肯定理解不了它的真正用意。总的来说，还是很有收获的。</p>
<p>本篇文章就着重分析了 <code>debounce</code> 的两个点：</p>
<ol>
<li>使用时间戳来判断执行点</li>
<li>考虑递归函数的场景</li>
</ol>
<p>希望能帮助到你，谢谢阅读！</p>
<hr>
<p><code>_.debounce</code> 的源码如下：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">debounce</span>(<span class="hljs-params">func, wait, immediate</span>) </span>&#123;
  <span class="hljs-keyword">var</span> timeout, previous, args, result, context;

  <span class="hljs-keyword">var</span> later = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">var</span> passed = now() - previous;
    <span class="hljs-keyword">if</span> (wait > passed) &#123;
      timeout = <span class="hljs-built_in">setTimeout</span>(later, wait - passed);
    &#125; <span class="hljs-keyword">else</span> &#123;
      timeout = <span class="hljs-literal">null</span>;
      <span class="hljs-keyword">if</span> (!immediate) result = func.apply(context, args);
      <span class="hljs-comment">// This check is needed because `func` can recursively invoke `debounced`.</span>
      <span class="hljs-keyword">if</span> (!timeout) args = context = <span class="hljs-literal">null</span>;
    &#125;
  &#125;;

  <span class="hljs-keyword">var</span> debounced = restArguments(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">_args</span>) </span>&#123;
    context = <span class="hljs-built_in">this</span>;
    args = _args;
    previous = now();
    <span class="hljs-keyword">if</span> (!timeout) &#123;
      timeout = <span class="hljs-built_in">setTimeout</span>(later, wait);
      <span class="hljs-keyword">if</span> (immediate) result = func.apply(context, args);
    &#125;
    <span class="hljs-keyword">return</span> result;
  &#125;);

  debounced.cancel = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">clearTimeout</span>(timeout);
    timeout = args = context = <span class="hljs-literal">null</span>;
  &#125;;

  <span class="hljs-keyword">return</span> debounced;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            