
---
title: 'css计数器语法小记'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e1abfb1da2784a25ba1bb6c1cd63cfdc~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 19:50:50 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e1abfb1da2784a25ba1bb6c1cd63cfdc~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;color:#595959;font-size:15px;font-family:-apple-system,system-ui,BlinkMacSystemFont,Helvetica Neue,PingFang SC,Hiragino Sans GB,Microsoft YaHei,Arial,sans-serif;background-image:linear-gradient(90deg,rgba(60,10,30,.04) 3%,transparent 0),linear-gradient(1turn,rgba(60,10,30,.04) 3%,transparent 0);background-size:20px 20px;background-position:50%&#125;.markdown-body p&#123;color:#595959;font-size:15px;line-height:2;font-weight:400&#125;.markdown-body p+p&#123;margin-top:16px&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;padding:30px 0;margin:0;color:#135ce0&#125;.markdown-body h1&#123;position:relative;text-align:center;font-size:22px;margin:50px 0&#125;.markdown-body h1:before&#123;position:absolute;content:"";top:-10px;left:50%;width:32px;height:32px;transform:translateX(-50%);background-size:100% 100%;opacity:.36;background-repeat:no-repeat;background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAABfVBMVEX///8Ad/8AgP8AgP8AgP8Aff8AgP8Af/8AgP8AVf8Af/8Af/8AgP8AgP8Af/8Afv8AAP8Afv8Afv8Aef8AgP8AdP8Afv8AgP8AgP8Acf8Ae/8AgP8Af/8AgP8Af/8Af/8AfP8Afv8AgP8Af/8Af/8Afv8Afv8AgP8Afv8AgP8Af/8Af/8AgP8AgP8Afv8AgP8Af/8AgP8AgP8AgP8Ae/8Afv8Af/8AgP8Af/8AgP8Af/8Af/8Aff8Af/8Abf8AgP8Af/8AgP8Af/8Af/8Afv8AgP8AgP8Afv8Afv8AgP8Af/8Aff8AgP8Afv8AgP8Aff8AgP8AfP8AgP8Ae/8AgP8Af/8AgP8AgP8AgP8Afv8AgP8AgP8AgP8Afv8AgP8AgP8AgP8AgP8AgP8Af/8AgP8Af/8Af/8Aev8Af/8AgP8Aff8Afv8AgP8AgP8AgP8Af/8AgP8Af/8Af/8AgP8Afv8AgP8AgP8AgP8AgP8Af/8AeP8Af/8Af/8Af//////rzEHnAAAAfXRSTlMAD7CCAivatxIDx5EMrP19AXdLEwgLR+6iCR/M0yLRzyFF7JupSXn8cw6v60Q0QeqzKtgeG237HMne850/6Qeq7QaZ+WdydHtj+OM3qENCMRYl1B3K2U7wnlWE/mhlirjkODa9FN/BF7/iNV/2kASNZpX1Wlf03C4stRGxgUPclqoAAAABYktHRACIBR1IAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4gEaBzgZ4yeM3AAAAT9JREFUOMvNUldbwkAQvCAqsSBoABE7asSOBRUVVBQNNuy9996789+9cMFAMHnVebmdm+/bmdtbQv4dOFOW2UjPzgFyLfo6nweKfIMOBYWwFtmMPGz2Yj2pJI0JDq3udJW6VVbmKa9I192VQFV1ktXUAl5NB0cd4KpnORqsEO2ZIRpF9gJfE9Dckqq0KuZt7UAH5+8EPF3spjsRpCeQNO/tA/qDwIDA+OCQbBoKA8NOdjMySgcZGVM6jwcgRuUiSs0nlPFNSrEpJfU0jTLD6llqbvKxei7OzvkFNQohi0vAsj81+MoqsCaoPOQFgus/1LyxichW+hS2JWCHZ7VlF9jb187pIAYcHiViHAMnp5mTjJ8B5xeEXF4B1ze/fTh/C0h398DDI9HB07O8ci+vRBdvdGnfP4gBuM8vw7X/G3wDmFhFZEdxzjMAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTgtMDEtMjZUMDc6NTY6MjUrMDE6MDA67pVWAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE4LTAxLTI2VDA3OjU2OjI1KzAxOjAwS7Mt6gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAAWdEVYdFRpdGxlAGp1ZWppbl9sb2dvIGNvcHlxapmKAAAAV3pUWHRSYXcgcHJvZmlsZSB0eXBlIGlwdGMAAHic4/IMCHFWKCjKT8vMSeVSAAMjCy5jCxMjE0uTFAMTIESANMNkAyOzVCDL2NTIxMzEHMQHy4BIoEouAOoXEXTyQjWVAAAAAElFTkSuQmCC)&#125;.markdown-body h2&#123;position:relative;font-size:20px;border-left:4px solid;padding:0 0 0 10px;margin:30px 0&#125;.markdown-body h3&#123;font-size:16px&#125;.markdown-body ul&#123;list-style:disc outside;margin-left:2em;margin-top:1em&#125;.markdown-body li&#123;line-height:2;color:#595959&#125;.markdown-body img.loaded&#123;margin:0 auto;display:block&#125;.markdown-body blockquote&#123;background:#fff9f9;margin:2em 0;padding:2px 20px;border-left:4px solid #b2aec5&#125;.markdown-body blockquote p&#123;color:#666;line-height:2&#125;.markdown-body a&#123;color:#036aca;border-bottom:1px solid rgba(3,106,202,.8);font-weight:400;text-decoration:none&#125;.markdown-body em strong,.markdown-body strong&#123;color:#036aca&#125;.markdown-body hr&#123;border-top:1px solid #135ce0&#125;.markdown-body pre&#123;overflow:auto&#125;.markdown-body code,.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body table&#123;border-collapse:collapse;margin:1rem 0;overflow-x:auto&#125;.markdown-body table td,.markdown-body table th&#123;border:1px solid #dfe2e5;padding:.6em 1em&#125;.markdown-body table tr&#123;border-top:1px solid #dfe2e5&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f6f8fa&#125;</style><p>CSS 计数器通过一个变量来设置，根据规则递增变量。</p>
<h2 data-id="heading-0">CSS 计数器使用到以下几个属性：</h2>
<ul>
<li>counter-reset - 创建或者重置计数器</li>
<li>counter-increment - 递增变量</li>
<li>content - 插入生成的内容</li>
<li>counter() 或 counters() 函数 - 将计数器的值添加到元素</li>
</ul>
<p>counter() 或 counters() 函数 是 content 属性中的方法。</p>
<h3 data-id="heading-1">1. counter-reset 创建或者重置计数器</h3>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-reset</span>: name;              // 默认从<span class="hljs-number">0</span>开始计数
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-reset</span>: name <span class="hljs-number">2</span>;            // 从<span class="hljs-number">2</span>开始计数，可以为负数或者小数(小数向下取整)，负数或小数IE和FireFox都不识别，会默认值<span class="hljs-number">0</span>来处理。
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-reset</span>: name1 <span class="hljs-number">2</span> name2 <span class="hljs-number">3</span>;   // 可以多个计数器同时命名
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-reset</span>: none | inherit;    // 干掉重置 | 继承重置
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-2">2. counter-increment 递增变量</h3>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-increment</span>: name;            // 默认+<span class="hljs-number">1</span>，每次递增+<span class="hljs-number">1</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-increment</span>: name <span class="hljs-number">2</span>;          // 每次递增+<span class="hljs-number">2</span>，可以设置为负数，来实现递减排序
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-increment</span>: name1 name2;     // 多个名称（与<span class="hljs-attribute">counter-reset</span>命名相呼应）
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">counter-increment</span>: none | inherit;  // 干掉递增 | 继承递增
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-3">3. counter() 或者 counters()  --将计数器的值添加到元素</h3>
<p><strong>counter()</strong></p>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">content</span>: <span class="hljs-built_in">counter</span>(name); 
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">content</span>: <span class="hljs-built_in">counter</span>(name,style); 
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">content</span>: <span class="hljs-built_in">counter</span>(name1) <span class="hljs-built_in">counter</span>(name2);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>style参数支持的关键字值就是 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.runoob.com%2Fcssref%2Fpr-list-style-type.html" target="_blank" rel="nofollow noopener noreferrer" title="https://www.runoob.com/cssref/pr-list-style-type.html" ref="nofollow noopener noreferrer">list-style-type</a> 支持的那些值。</p>
<p><strong>counters()</strong></p>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">content</span>: <span class="hljs-built_in">counters</span>(name, string);
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-css copyable" lang="css"><span class="hljs-attribute">content</span>: <span class="hljs-built_in">counters</span>(name, string, style)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>string参数为字符串（必须），表示子序号的连接字符串。例如1.1的string就是<code>'.'</code>，1-1就是<code>'-'</code>。</p>
<p>counters()也是支持style自定义递增形式的，表现与counter()的style参数使用一致。</p>
<blockquote>
<p>我们平时的序号，不可能就只是1,2,3,4,.., 还会有诸如 1.1,1.2,1.3,...等的子序号。前者就是counter()干的事情，后者就是counters()干的事情。</p>
</blockquote>
<h2 data-id="heading-4">案例参考</h2>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.zhangxinxu.com%2Fstudy%2F201408%2Fcss-counters-string.html" target="_blank" rel="nofollow noopener noreferrer" title="https://www.zhangxinxu.com/study/201408/css-counters-string.html" ref="nofollow noopener noreferrer">案例链接</a></p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e1abfb1da2784a25ba1bb6c1cd63cfdc~tplv-k3u1fbpfcp-watermark.image" alt="微信图片_20210713111750.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-5">CSS计数器与display:none</h2>
<blockquote>
<p>一个元素，如果设置了counter-increment, 但是其display的属性值是none或者含有hidden属性（针对支持浏览器），则此计数值是不会增加的。而visibility:hidden以及其他声明不会有此现象。</p>
</blockquote>
<h2 data-id="heading-6">浏览器支持</h2>
<blockquote>
<p>所有主流浏览器都支持counter-reset/counter-increment/Content属性。</p>
<p>注意： IE8只有指定!DOCTYPE才支持counter-reset/counter-increment/Content属性。</p>
</blockquote>
<h2 data-id="heading-7">结语</h2>
<p>此篇为观后感，只对语法上的使用总结排序一下，具体的解析和理解可以看以下的文档和参考链接。</p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2FCSS_Lists_and_Counters%2FUsing_CSS_counters" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters" ref="nofollow noopener noreferrer">文档链接 MDN</a>
/
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.runoob.com%2Fcss%2Fcss-counters.html" target="_blank" rel="nofollow noopener noreferrer" title="https://www.runoob.com/css/css-counters.html" ref="nofollow noopener noreferrer">文档链接 菜鸟</a>
/
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.zhangxinxu.com%2Fwordpress%2F2014%2F08%2Fcss-counters-automatic-number-content%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://www.zhangxinxu.com/wordpress/2014/08/css-counters-automatic-number-content/" ref="nofollow noopener noreferrer">参考链接 张鑫旭</a></p></div>  
</div>
            