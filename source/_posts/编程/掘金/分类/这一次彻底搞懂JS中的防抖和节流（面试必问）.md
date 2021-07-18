
---
title: '这一次彻底搞懂JS中的防抖和节流（面试必问）'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=5198'
author: 掘金
comments: false
date: Thu, 15 Jul 2021 18:56:43 GMT
thumbnail: 'https://picsum.photos/400/300?random=5198'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;color:#595959;font-size:15px;font-family:-apple-system,system-ui,BlinkMacSystemFont,Helvetica Neue,PingFang SC,Hiragino Sans GB,Microsoft YaHei,Arial,sans-serif;background-image:linear-gradient(90deg,rgba(60,10,30,.04) 3%,transparent 0),linear-gradient(1turn,rgba(60,10,30,.04) 3%,transparent 0);background-size:20px 20px;background-position:50%&#125;.markdown-body p&#123;color:#595959;font-size:15px;line-height:2;font-weight:400&#125;.markdown-body p+p&#123;margin-top:16px&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;padding:30px 0;margin:0;color:#135ce0&#125;.markdown-body h1&#123;position:relative;text-align:center;font-size:22px;margin:50px 0&#125;.markdown-body h1:before&#123;position:absolute;content:"";top:-10px;left:50%;width:32px;height:32px;transform:translateX(-50%);background-size:100% 100%;opacity:.36;background-repeat:no-repeat;background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAABfVBMVEX///8Ad/8AgP8AgP8AgP8Aff8AgP8Af/8AgP8AVf8Af/8Af/8AgP8AgP8Af/8Afv8AAP8Afv8Afv8Aef8AgP8AdP8Afv8AgP8AgP8Acf8Ae/8AgP8Af/8AgP8Af/8Af/8AfP8Afv8AgP8Af/8Af/8Afv8Afv8AgP8Afv8AgP8Af/8Af/8AgP8AgP8Afv8AgP8Af/8AgP8AgP8AgP8Ae/8Afv8Af/8AgP8Af/8AgP8Af/8Af/8Aff8Af/8Abf8AgP8Af/8AgP8Af/8Af/8Afv8AgP8AgP8Afv8Afv8AgP8Af/8Aff8AgP8Afv8AgP8Aff8AgP8AfP8AgP8Ae/8AgP8Af/8AgP8AgP8AgP8Afv8AgP8AgP8AgP8Afv8AgP8AgP8AgP8AgP8AgP8Af/8AgP8Af/8Af/8Aev8Af/8AgP8Aff8Afv8AgP8AgP8AgP8Af/8AgP8Af/8Af/8AgP8Afv8AgP8AgP8AgP8AgP8Af/8AeP8Af/8Af/8Af//////rzEHnAAAAfXRSTlMAD7CCAivatxIDx5EMrP19AXdLEwgLR+6iCR/M0yLRzyFF7JupSXn8cw6v60Q0QeqzKtgeG237HMne850/6Qeq7QaZ+WdydHtj+OM3qENCMRYl1B3K2U7wnlWE/mhlirjkODa9FN/BF7/iNV/2kASNZpX1Wlf03C4stRGxgUPclqoAAAABYktHRACIBR1IAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4gEaBzgZ4yeM3AAAAT9JREFUOMvNUldbwkAQvCAqsSBoABE7asSOBRUVVBQNNuy9996789+9cMFAMHnVebmdm+/bmdtbQv4dOFOW2UjPzgFyLfo6nweKfIMOBYWwFtmMPGz2Yj2pJI0JDq3udJW6VVbmKa9I192VQFV1ktXUAl5NB0cd4KpnORqsEO2ZIRpF9gJfE9Dckqq0KuZt7UAH5+8EPF3spjsRpCeQNO/tA/qDwIDA+OCQbBoKA8NOdjMySgcZGVM6jwcgRuUiSs0nlPFNSrEpJfU0jTLD6llqbvKxei7OzvkFNQohi0vAsj81+MoqsCaoPOQFgus/1LyxichW+hS2JWCHZ7VlF9jb187pIAYcHiViHAMnp5mTjJ8B5xeEXF4B1ze/fTh/C0h398DDI9HB07O8ci+vRBdvdGnfP4gBuM8vw7X/G3wDmFhFZEdxzjMAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTgtMDEtMjZUMDc6NTY6MjUrMDE6MDA67pVWAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE4LTAxLTI2VDA3OjU2OjI1KzAxOjAwS7Mt6gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAAWdEVYdFRpdGxlAGp1ZWppbl9sb2dvIGNvcHlxapmKAAAAV3pUWHRSYXcgcHJvZmlsZSB0eXBlIGlwdGMAAHic4/IMCHFWKCjKT8vMSeVSAAMjCy5jCxMjE0uTFAMTIESANMNkAyOzVCDL2NTIxMzEHMQHy4BIoEouAOoXEXTyQjWVAAAAAElFTkSuQmCC)&#125;.markdown-body h2&#123;position:relative;font-size:20px;border-left:4px solid;padding:0 0 0 10px;margin:30px 0&#125;.markdown-body h3&#123;font-size:16px&#125;.markdown-body ul&#123;list-style:disc outside;margin-left:2em;margin-top:1em&#125;.markdown-body li&#123;line-height:2;color:#595959&#125;.markdown-body img.loaded&#123;margin:0 auto;display:block&#125;.markdown-body blockquote&#123;background:#fff9f9;margin:2em 0;padding:2px 20px;border-left:4px solid #b2aec5&#125;.markdown-body blockquote p&#123;color:#666;line-height:2&#125;.markdown-body a&#123;color:#036aca;border-bottom:1px solid rgba(3,106,202,.8);font-weight:400;text-decoration:none&#125;.markdown-body em strong,.markdown-body strong&#123;color:#036aca&#125;.markdown-body hr&#123;border-top:1px solid #135ce0&#125;.markdown-body pre&#123;overflow:auto&#125;.markdown-body code,.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body table&#123;border-collapse:collapse;margin:1rem 0;overflow-x:auto&#125;.markdown-body table td,.markdown-body table th&#123;border:1px solid #dfe2e5;padding:.6em 1em&#125;.markdown-body table tr&#123;border-top:1px solid #dfe2e5&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f6f8fa&#125;</style><h2 data-id="heading-0">什么是防抖？</h2>
<blockquote>
<p>通过setTimeout的方式，在一定的时间间隔内，将多次触发变成一次触发。（通俗的说是在最后一次点击间隔规定时间之后才能再次成功触发，否则触发不成功）</p>
</blockquote>
<h2 data-id="heading-1">防抖的实现思路</h2>
<ol>
<li>在防抖函数返回的函数的上级作用域设置一个定时器变量t置为null;</li>
<li>通过t来判断是否是第一次执行。</li>
<li>如果不是第一次执行，清空定时器</li>
<li>如果是第一次执行，则通过apply(this,arguments)进行执行.</li>
<li>最后设置定时器，规定时间之后将t设置为null,使得间隔时间之后t为null，间隔时间之后的点击变为第一次点击。</li>
</ol>
<h2 data-id="heading-2">防抖实现代码</h2>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> btn = <span class="hljs-built_in">document</span>.querySelector(<span class="hljs-string">'#input'</span>);

btn.addEventListener(<span class="hljs-string">'click'</span>,debounce(submit,<span class="hljs-number">3000</span>),<span class="hljs-literal">false</span>);

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">submit</span>(<span class="hljs-params">e</span>) </span>&#123;
    <span class="hljs-built_in">console</span>.log(<span class="hljs-number">1</span>);
&#125;
<span class="hljs-comment">// 防抖函数：最后一次点击之后，3秒之内的点击都无效</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">debounce</span>(<span class="hljs-params">fn,timer</span>) </span>&#123;
    <span class="hljs-keyword">let</span> t = <span class="hljs-literal">null</span>;
    <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-comment">// 判断是否是第一次执行</span>
        <span class="hljs-keyword">let</span> firstClick = !t;
        <span class="hljs-comment">// 如果不是第一次执行，则清空延时  之所以要清空延时就是要防止前面的定时器对最新的定时器产生影响，</span>
        <span class="hljs-keyword">if</span> (t) &#123; <span class="hljs-built_in">clearTimeout</span>(t)&#125;;
        <span class="hljs-comment">// 如果是第一次执行则直接执行</span>
        <span class="hljs-keyword">if</span> (firstClick) &#123;
            fn.apply(<span class="hljs-built_in">this</span>,<span class="hljs-built_in">arguments</span>)
        &#125;
        <span class="hljs-comment">// 在第一次点击之后 间隔的规定时间之后，才将t置为null 为下一次第一次点击做准备</span>
        t = <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =></span> &#123;
            t = <span class="hljs-literal">null</span>;                    
        &#125;,timer)
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<h3 data-id="heading-3"><a href="https://link.juejin.cn/?target=https%3A%2F%2Fcodesandbox.io%2Fs%2Fshouxiefangdouhanshu-8mf22%3Ffile%3D%2Findex.html" target="_blank" rel="nofollow noopener noreferrer" title="https://codesandbox.io/s/shouxiefangdouhanshu-8mf22?file=/index.html" ref="nofollow noopener noreferrer">codeSandBox在线演示</a></h3>
</blockquote>
<hr>
<h2 data-id="heading-4">什么是节流？</h2>
<blockquote>
<p>节流指的是减少一段时间内的触发频率。只有在上一次成功触发间隔规定时间之后，才能再次触发。</p>
</blockquote>
<h2 data-id="heading-5">节流的实现思路</h2>
<ol>
<li>在返回函数的上级作用域定义一个初始时间值begin = 0;</li>
<li>获取当前时间戳，如果(当前时间戳 - 初始值 > 规定时间间隔)则通过apply修改this指向并传参;</li>
<li>修改初始值为当前值;</li>
</ol>
<h2 data-id="heading-6">节流实现代码</h2>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> btn = <span class="hljs-built_in">document</span>.querySelector(<span class="hljs-string">'#input'</span>);

btn.addEventListener(<span class="hljs-string">'click'</span>,throttle(submit,<span class="hljs-number">2000</span>),<span class="hljs-literal">false</span>);

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">submit</span>(<span class="hljs-params">e</span>) </span>&#123;
    <span class="hljs-built_in">console</span>.log(<span class="hljs-number">1</span>);
&#125;
<span class="hljs-comment">// 节流函数：减少一段时间的触发频率，只有在上一次成功触发 间隔规定时间之后才能再次成功触发。</span>

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">throttle</span>(<span class="hljs-params">fn,delay</span>) </span>&#123;
    <span class="hljs-keyword">let</span> begin = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-keyword">let</span> cur = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Date</span>().getTime();

        <span class="hljs-keyword">if</span> (cur - begin > delay) &#123;
            fn.apply(<span class="hljs-built_in">this</span>,<span class="hljs-built_in">arguments</span>);
            begin = cur;
        &#125;
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<h3 data-id="heading-7"><a href="https://link.juejin.cn/?target=https%3A%2F%2Fcodesandbox.io%2Fs%2Fshouxiejieliuhanshu-645r1%3Ffile%3D%2Findex.html" target="_blank" rel="nofollow noopener noreferrer" title="https://codesandbox.io/s/shouxiejieliuhanshu-645r1?file=/index.html" ref="nofollow noopener noreferrer">codeSandBox在线演示</a></h3>
</blockquote>
<h2 data-id="heading-8">节流与防抖的区别是什么？</h2>
<ol>
<li>防抖只在最后一次成功点击之后间隔规定时间之后才能再次成功触发，如果在时间间隔之内就被点击，需要重新间隔时间间隔才能点击。</li>
<li>节流则不同，节流只要在上一次成功触发规定时间之后点击就能再次触发，中间的触发不会产生影响。</li>
</ol></div>  
</div>
            