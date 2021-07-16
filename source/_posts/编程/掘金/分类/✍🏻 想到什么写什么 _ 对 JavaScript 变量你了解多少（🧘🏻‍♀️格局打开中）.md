
---
title: '✍🏻 想到什么写什么 _ 对 JavaScript 变量你了解多少（🧘🏻‍♀️格局打开中）'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8536f71b05df47efb83d7231ce441ef7~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Wed, 14 Jul 2021 23:35:31 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8536f71b05df47efb83d7231ce441ef7~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;color:#595959;font-size:15px;font-family:-apple-system,system-ui,BlinkMacSystemFont,Helvetica Neue,PingFang SC,Hiragino Sans GB,Microsoft YaHei,Arial,sans-serif;background-image:linear-gradient(90deg,rgba(60,10,30,.04) 3%,transparent 0),linear-gradient(1turn,rgba(60,10,30,.04) 3%,transparent 0);background-size:20px 20px;background-position:50%&#125;.markdown-body p&#123;color:#595959;font-size:15px;line-height:2;font-weight:400&#125;.markdown-body p+p&#123;margin-top:16px&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;padding:30px 0;margin:0;color:#135ce0&#125;.markdown-body h1&#123;position:relative;text-align:center;font-size:22px;margin:50px 0&#125;.markdown-body h1:before&#123;position:absolute;content:"";top:-10px;left:50%;width:32px;height:32px;transform:translateX(-50%);background-size:100% 100%;opacity:.36;background-repeat:no-repeat;background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAABfVBMVEX///8Ad/8AgP8AgP8AgP8Aff8AgP8Af/8AgP8AVf8Af/8Af/8AgP8AgP8Af/8Afv8AAP8Afv8Afv8Aef8AgP8AdP8Afv8AgP8AgP8Acf8Ae/8AgP8Af/8AgP8Af/8Af/8AfP8Afv8AgP8Af/8Af/8Afv8Afv8AgP8Afv8AgP8Af/8Af/8AgP8AgP8Afv8AgP8Af/8AgP8AgP8AgP8Ae/8Afv8Af/8AgP8Af/8AgP8Af/8Af/8Aff8Af/8Abf8AgP8Af/8AgP8Af/8Af/8Afv8AgP8AgP8Afv8Afv8AgP8Af/8Aff8AgP8Afv8AgP8Aff8AgP8AfP8AgP8Ae/8AgP8Af/8AgP8AgP8AgP8Afv8AgP8AgP8AgP8Afv8AgP8AgP8AgP8AgP8AgP8Af/8AgP8Af/8Af/8Aev8Af/8AgP8Aff8Afv8AgP8AgP8AgP8Af/8AgP8Af/8Af/8AgP8Afv8AgP8AgP8AgP8AgP8Af/8AeP8Af/8Af/8Af//////rzEHnAAAAfXRSTlMAD7CCAivatxIDx5EMrP19AXdLEwgLR+6iCR/M0yLRzyFF7JupSXn8cw6v60Q0QeqzKtgeG237HMne850/6Qeq7QaZ+WdydHtj+OM3qENCMRYl1B3K2U7wnlWE/mhlirjkODa9FN/BF7/iNV/2kASNZpX1Wlf03C4stRGxgUPclqoAAAABYktHRACIBR1IAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4gEaBzgZ4yeM3AAAAT9JREFUOMvNUldbwkAQvCAqsSBoABE7asSOBRUVVBQNNuy9996789+9cMFAMHnVebmdm+/bmdtbQv4dOFOW2UjPzgFyLfo6nweKfIMOBYWwFtmMPGz2Yj2pJI0JDq3udJW6VVbmKa9I192VQFV1ktXUAl5NB0cd4KpnORqsEO2ZIRpF9gJfE9Dckqq0KuZt7UAH5+8EPF3spjsRpCeQNO/tA/qDwIDA+OCQbBoKA8NOdjMySgcZGVM6jwcgRuUiSs0nlPFNSrEpJfU0jTLD6llqbvKxei7OzvkFNQohi0vAsj81+MoqsCaoPOQFgus/1LyxichW+hS2JWCHZ7VlF9jb187pIAYcHiViHAMnp5mTjJ8B5xeEXF4B1ze/fTh/C0h398DDI9HB07O8ci+vRBdvdGnfP4gBuM8vw7X/G3wDmFhFZEdxzjMAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTgtMDEtMjZUMDc6NTY6MjUrMDE6MDA67pVWAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE4LTAxLTI2VDA3OjU2OjI1KzAxOjAwS7Mt6gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAAWdEVYdFRpdGxlAGp1ZWppbl9sb2dvIGNvcHlxapmKAAAAV3pUWHRSYXcgcHJvZmlsZSB0eXBlIGlwdGMAAHic4/IMCHFWKCjKT8vMSeVSAAMjCy5jCxMjE0uTFAMTIESANMNkAyOzVCDL2NTIxMzEHMQHy4BIoEouAOoXEXTyQjWVAAAAAElFTkSuQmCC)&#125;.markdown-body h2&#123;position:relative;font-size:20px;border-left:4px solid;padding:0 0 0 10px;margin:30px 0&#125;.markdown-body h3&#123;font-size:16px&#125;.markdown-body ul&#123;list-style:disc outside;margin-left:2em;margin-top:1em&#125;.markdown-body li&#123;line-height:2;color:#595959&#125;.markdown-body img.loaded&#123;margin:0 auto;display:block&#125;.markdown-body blockquote&#123;background:#fff9f9;margin:2em 0;padding:2px 20px;border-left:4px solid #b2aec5&#125;.markdown-body blockquote p&#123;color:#666;line-height:2&#125;.markdown-body a&#123;color:#036aca;border-bottom:1px solid rgba(3,106,202,.8);font-weight:400;text-decoration:none&#125;.markdown-body em strong,.markdown-body strong&#123;color:#036aca&#125;.markdown-body hr&#123;border-top:1px solid #135ce0&#125;.markdown-body pre&#123;overflow:auto&#125;.markdown-body code,.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body table&#123;border-collapse:collapse;margin:1rem 0;overflow-x:auto&#125;.markdown-body table td,.markdown-body table th&#123;border:1px solid #dfe2e5;padding:.6em 1em&#125;.markdown-body table tr&#123;border-top:1px solid #dfe2e5&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f6f8fa&#125;</style><p>本文已参与好文召集令活动，点击查看：<a href="https://juejin.cn/post/6978685539985653767" target="_blank" title="https://juejin.cn/post/6978685539985653767">后端、大前端双赛道投稿，2万元奖池等你挑战</a>！</p>
<p><strong>前言</strong></p>
<blockquote>
<p>本系列诞生的原因是之前写一些文章时，对文章结构很是头疼（总是感觉不够清晰左改右改）🤦🏻‍♀️ 。所以不想只是为了让文章看起来干净，而刻意去整理一个对理解过程没有帮助的结构出来，定了这个系列。全系列文章都是随着思路的发散，想到啥写啥😂，不会太去关心文章结构或者前后是否连贯。觉得内容太多的小伙伴可以按照目录选看自己感兴趣的片段。<br>
<a href="https://link.juejin.cn/?target=https%3A%2F%2F262.ecma-international.org%2F12.0%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://262.ecma-international.org/12.0/" ref="nofollow noopener noreferrer">ECMA-262 规范</a>  镇楼 🙏🏻 ，祝看到此文的小伙伴快乐暴富~</p>
</blockquote>
<h2 data-id="heading-0">变量在内存中如何存储（第1版）</h2>
<p>JavaScript 内存空间分为两块 —— <strong>栈</strong>内存和<strong>堆</strong>内存。</p>
<p>一般将<strong>原始数据类型</strong>的变量直接存放在<strong>栈内存</strong>中（便于快速读写和内存释放），而对于<strong>引用数据类型</strong>则是将变量存放在<strong>堆内存</strong>中，对应会产生一个<strong>堆内存</strong>的<strong>内存地址</strong>（<strong>hashCode</strong>），<strong>栈内存</strong>中该变量值则是存储了这个<strong>地址</strong>，当我们访问该变量时，会在按照这个地址找到对应<strong>堆内存</strong>中的数据值。</p>
<p>这么说可能还有些云里雾里，我们再补充一下知识路径，更好理解这个概念。</p>
<h2 data-id="heading-1">插一嘴， JavaScript 规定了几种数据类型？</h2>
<p><strong>8 种（7 种原始数据类型 + 1 中引用数据类型）</strong></p>





































<table><thead><tr><th><strong>原始类型值（存储在栈内存中）</strong></th><th>描述</th></tr></thead><tbody><tr><td><code>null</code></td><td>变量值为null（<code>typeof null === 'object'</code>，值为null的变量会被垃圾回收）</td></tr><tr><td><code>undefined</code></td><td>一个没有被赋值的变量默认值为undefined（有变量提升的情况下，在赋值语句前打印变量，默认值也是undefined）</td></tr><tr><td><code>boolean</code></td><td>变量值为<code>true</code>或者<code>false</code></td></tr><tr><td><code>number</code></td><td>数值型（精度丢失！浏览器对请求返回数据json中是数值型的数据，末尾会有抹0的动作）</td></tr><tr><td><code>string</code></td><td>字符串型（在做js加法运算时，会先将变量转换成原始类型，如果加号两边的变量有任一个为字符串类型，则另一个也会强制转换成字符串类型做字符串）</td></tr><tr><td><code>symbol</code></td><td>一个永远不会和其他值相等的值（可以用在对象内部私有变量做唯一标识）</td></tr><tr><td><code>bigInt</code></td><td>任意精度的<strong>整数</strong>（很多人都以为只有小数才会遇见精度丢失问题，其实整数也会，<code>BigInt(n)</code>生成的整数不会出现精度丢失）</td></tr></tbody></table>













<table><thead><tr><th><strong>引用类型值（存储在堆内存中）</strong></th><th>描述</th></tr></thead><tbody><tr><td><code>object</code></td><td>一组键值对的集合</td></tr></tbody></table>
<p>ps：这里需要注意这里的类型指的都是<code>值</code>的类型（下面👇会有对此点的说明）</p>
<p>e.g.</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">typeof</span> <span class="hljs-literal">undefined</span> === <span class="hljs-string">"undefined"</span> <span class="hljs-comment">// true</span>
<span class="hljs-keyword">typeof</span> <span class="hljs-literal">true</span> === <span class="hljs-string">"boolean"</span> <span class="hljs-comment">// true</span>
<span class="hljs-keyword">typeof</span> <span class="hljs-number">32</span> === <span class="hljs-string">"number"</span> <span class="hljs-comment">// true</span>
<span class="hljs-keyword">typeof</span> <span class="hljs-string">"js"</span> === <span class="hljs-string">"string"</span> <span class="hljs-comment">// true</span>
<span class="hljs-keyword">typeof</span> &#123;
    <span class="hljs-attr">name</span>: <span class="hljs-string">'Mike'</span>
&#125; === <span class="hljs-string">"object"</span> <span class="hljs-comment">// true</span>
<span class="hljs-comment">// ES6 新加入</span>
<span class="hljs-keyword">typeof</span> <span class="hljs-built_in">Symbol</span>() === <span class="hljs-string">"symbol"</span> <span class="hljs-comment">// true</span>
<span class="hljs-comment">// ES2020 新加入</span>
<span class="hljs-keyword">typeof</span> <span class="hljs-built_in">BigInt</span>(<span class="hljs-number">123</span>) === <span class="hljs-string">"bigint"</span> <span class="hljs-comment">// true</span>
<span class="hljs-comment">// 注意</span>
<span class="hljs-keyword">typeof</span> <span class="hljs-literal">null</span> === <span class="hljs-string">"object"</span> <span class="hljs-comment">// true</span>
<span class="hljs-comment">// object 下的子类型</span>
<span class="hljs-keyword">typeof</span>(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;&#125;) === <span class="hljs-string">"function"</span> <span class="hljs-comment">// true</span>
<span class="hljs-keyword">typeof</span>(<span class="hljs-keyword">new</span> <span class="hljs-built_in">Date</span>()) === <span class="hljs-string">"object"</span> <span class="hljs-comment">// true</span>
<span class="hljs-keyword">typeof</span> [] === <span class="hljs-string">"object"</span> <span class="hljs-comment">// true</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-2"><code>null</code> 和 <code>undefined</code> 的区别</h3>
<p>// todo</p>
<h3 data-id="heading-3">判断变量类型的方法（plus如何准确的判断数组类型）</h3>
<p>// todo</p>
<h3 data-id="heading-4">Symbol有应用场景么？</h3>
<p>// todo</p>
<p>💭：讲了数据类型，我上个段落的文字中总是提到 <code>xxx型变量</code> 这样的字眼，可能大多数人不会疑惑，但我在学习的时候因为下文会提到 <code>原始类型值是不能被修改的</code> 这一概念，我感到非常困惑 🤯</p>
<p>因为通常我们设置了一个数值型变量 <code>var a = 1</code> ，然后可能通过一些逻辑噼里啪啦之后将其改为 <code>10</code> 之类的其他数值，这个操作是如此的常见，其他原始类型也是如此，我就非常不理解 <code>原始类型值不能被修改</code> 这句话。于是我挣扎了一会儿通透了🎉 ，才返过来补了这段内容以及理解的思路，可以直接跟我看下去。</p>
<h2 data-id="heading-5">变量类型是指变量的值的类型</h2>
<p>JavaScript 是一种弱类型且动态的语言，<strong>弱类型是指不需要提前指定变量类型，js引擎在运算时会计算出变量是什么数据类型。动态是指同一个变量可以保存不同类型的数据。</strong></p>
<p>有一个概念需要明确，当看到 <code>var a = 1</code> 时，通常会说 “我创建了一个数值型变量 <code>a</code> ” 。</p>
<p><code>var a = xxx</code> 这个简单的赋值语句其实是三个步骤，</p>
<ol>
<li>创建了一个值 <code>xxx</code></li>
<li>创建了一个变量 <code>a</code></li>
<li>让值和变量关联</li>
</ol>
<p>其实更准确的说法是，我们创建了一个变量 <code>a</code> ，它的值是数值型。JavaScript 动态语言的特性，事实上并不存在变量类型的概念，我们在描述一个变量类型时，不是说这个变量就是xxx类型，而是这个变量在我们使用当下（ <code>js引擎在运算时会计算出值的数据类型</code> - 弱类型特性 ）的值是xxx类型。</p>
<p>再看一个例子，这个例子清晰的说明了JavaScript动态性的特点。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> a = <span class="hljs-number">1</span> <span class="hljs-comment">// 数值1</span>
<span class="hljs-built_in">console</span>.log(a)
a = <span class="hljs-number">10</span> <span class="hljs-comment">// 数值10</span>
<span class="hljs-built_in">console</span>.log(a)
a = <span class="hljs-string">'一个装睡的人'</span> <span class="hljs-comment">// 字符串'一个装睡的人'</span>
<span class="hljs-built_in">console</span>.log(a)
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>run code</code> 输出如下结果：</p>
<pre><code class="hljs language-md copyable" lang="md">1
10
一个装睡的人

[Done] exited with code=0 in 1.46 seconds
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-6">那么当变量的值是原始类型和引用类型时，有什么不同的表现呢？</h2>
<p>前面提到赋值语句的<a href="https://juejin.cn/post/6985053046720102436#%E5%8F%98%E9%87%8F%E7%B1%BB%E5%9E%8B%E6%98%AF%E6%8C%87%E5%8F%98%E9%87%8F%E7%9A%84%E5%80%BC%E7%9A%84%E7%B1%BB%E5%9E%8B" target="_blank" title="#%E5%8F%98%E9%87%8F%E7%B1%BB%E5%9E%8B%E6%98%AF%E6%8C%87%E5%8F%98%E9%87%8F%E7%9A%84%E5%80%BC%E7%9A%84%E7%B1%BB%E5%9E%8B">三个步骤</a>，最后一个步骤 <code>让值和变量关联</code> ，关联的方式有两种，存储值和存储引用，当代码运行后，每一个变量都会在<strong>栈内存</strong>中为它开辟一个内存空间，保存变量以及变量的值。变量就是一个用于标识的名称，而变量的值会根据不同值的数据类型有不同的<strong>存储表现</strong>。不同的表现我们从<strong>使用</strong>和<strong>存储</strong>两个角度分析，</p>
<p><strong>不同的存储表现</strong></p>
<p>原始类型的<strong>值本身</strong>就存储在栈内存中，以支持快速读取及回收清理内存释放。而引用类型的值是存储在<strong>堆内存</strong>中的，堆内存有更大的空间及保存周期更长，相较于栈内存它的读写速度也会慢一点，就很适合复杂类型的存储。</p>
<p>当遇到引用类型的值，<strong>值本身</strong>是存储在堆内存中的，堆内存会提供一个让外部访问到该值的内存地址( <code>hashCode</code> )，而我们在<strong>栈内存</strong>中，该变量的值上存储的就是这个堆内存给出的<strong>引用内存地址</strong>。</p>
<p><strong>不同的使用表现</strong></p>
<p>因为存储时的不同，在使用上自然也就有所不同了。</p>
<p>原始数据类型是<strong>按值访问</strong>的，因为变量的值是将数据的值直接存储在栈内存中的，我们在操作变量时，也就是<strong>直接</strong>在操作变量的值。</p>
<p>相对比，引用类型的变量的值因为根本没有存储在栈内存中，我们能<strong>直接访问</strong>的只是栈内存中存储的<strong>引用地址</strong>，而数据真正的值我们只能间接通过内存地址去堆内存中查询。所以我们在操作值为引用类型的变量时，本质只是在操作<strong>内存地址</strong>。</p>
<p><strong>理解值类型和引用类型</strong></p>
<ul>
<li>值类型和引用类型存储位置和方式不一样</li>
<li>值类型和引用类型占用内存大小及周期不同</li>
<li>值类型和引用类型在读写及赋值操作上会有不同的表现</li>
</ul>
<p>讲到这里，我觉得我开头阐述的文字不太严谨，稍加修改 ✍🏻</p>
<h2 data-id="heading-7">变量在内存中如何存储（第2版）</h2>
<p>JavaScript 内存空间分为两块 —— <strong>栈</strong>内存和<strong>堆</strong>内存。</p>
<p>一般将值为<strong>原始数据类型</strong>的变量值直接存放在<strong>栈内存</strong>中（局部的、占用空间确定的数据、便于快速读写和内存释放），而对于值为<strong>引用数据类型</strong>的变量则是将值本身存放在<strong>堆内存</strong>中，对应会产生一个指向该值的<strong>堆内存地址</strong>（<strong>hashCode</strong>），<strong>栈内存</strong>中该变量的值则是存储了这个<strong>地址</strong>。当我们访问变量时，会先在栈内存中找到该变量存储的内存地址，再按照这个地址找到<strong>堆内存</strong>中对应的数据值。</p>
<p>这样有没有感觉稍微通透了一点点？再附一个小例子，加深理解</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8536f71b05df47efb83d7231ce441ef7~tplv-k3u1fbpfcp-zoom-1.image" alt="格局打开" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-8">栈内存和堆内存中变量的赋值操作有不同表现</h3>
<p><strong>栈内存</strong></p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>
<span class="hljs-keyword">var</span> b = a <span class="hljs-comment">// b是a的值的一个复本</span>
b = <span class="hljs-number">100</span> <span class="hljs-comment">// 修改b的值</span>

<span class="hljs-comment">// a,b 属于原始数据类型，存放在栈内存中</span>
<span class="hljs-built_in">console</span>.log(&#123;
    a
&#125;, &#123;
    b
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>运行结果如下:</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4fef81d0bb394c61b67ff3986b7006c3~tplv-k3u1fbpfcp-watermark.image" alt="栈内存" loading="lazy" referrerpolicy="no-referrer"></p>
<p>可以看到我们将 <code>a</code> 复制给了 <code>b</code> 后，当我们修改 <code>b</code> 的值，并没有对 <code>a</code> 造成影响。这是为什么呢？</p>
<p>正如我们上面所说的，原始数据类型是存放在栈内存中的，并且属性值就是原始值。什么意思呢？我们按行分析。</p>
<ul>
<li>
<p><code>var a = 10</code></p>
<p>声明了一个 number 变量 <code>a</code> ，JS 会给 <code>a</code> 分配内存（栈内存），并将 <code>a</code> 的原始值 10 存在分配的内存中。</p>
</li>
<li>
<p><code>var b = a</code></p>
<p>声明了一个变量 <code>b</code> ， <code>b = a</code> 是一个引用赋值的操作，因为 <code>a</code> 是原始数据类型（number），对于原始数据类型变量，引用赋值操作是直接在内存中查找到<strong>变量值</strong>将其赋值给新声明变量的。最后就相当于 <code>var b = 10</code> ，声明了一个 number 变量 <code>b</code> ，JS 会给 <code>b</code> 分配内存（栈内存），并将 <code>b</code> 的原始值 10 存在分配的内存中。</p>
</li>
<li>
<p><code>b = 100</code></p>
<p>这一步就是上述所说的内存生命周期中的第二步——对已分配的内存进行读写。JS 找到分配给 <code>b</code> 的内存并将数值 100 写入该内存中。</p>
</li>
</ul>
<p>✅：<strong>虽然是复制操作，但是对于原始数据类型相当于是写入一个值的操作，两个变量相互独立，互不影响。</strong></p>
<p><strong>堆内存</strong></p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> personA = &#123;
    <span class="hljs-attr">name</span>: <span class="hljs-string">'Peter'</span>
&#125;
<span class="hljs-keyword">var</span> personB = personA <span class="hljs-comment">// personB是&#123;name:'Peter'&#125;的一个引用</span>
personB.name = <span class="hljs-string">'Alice'</span> <span class="hljs-comment">// 修改personB的值</span>

<span class="hljs-comment">// personA,personB 属于引用数据类型，存放在堆内存中</span>
<span class="hljs-built_in">console</span>.log(&#123;
    personA
&#125;, &#123;
    personB
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>运行结果如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/35d10f39c3ff47e08ba852d9fc73f22e~tplv-k3u1fbpfcp-watermark.image" alt="堆内存" loading="lazy" referrerpolicy="no-referrer"></p>
<p>可以看到我们将 <code>a</code> 复制给了 <code>b</code> 后，当我们修改 <code>b</code> 时，对 <code>a</code> 也造成了影响。这是为什么呢？</p>
<p>正如我们上面所说的，引用类型的变量是存放在堆内存中的，在栈中变量值存放的是该变量对应的堆内存地址（hashCode）。什么意思呢？我们依然按行分析一下。</p>
<ul>
<li>
<p><code>var personA = &#123; name: 'Peter' &#125;</code></p>
<p>声明了一个 object 变量 <code>personA</code> ，JS 会先给对象 <code>&#123; name: 'Peter' &#125;</code> 分配内存（堆内存），给 <code>personA</code> 也分配内存（栈内存），将 <code>&#123; name: 'Peter' &#125;</code> 分配到的堆内存地址赋值给 personA` 。</p>
</li>
<li>
<p><code>var personB = personA</code></p>
<p>声明了一个变量 <code>personB</code> ， <code>personB = personA</code> 因为 <code>personA</code> 是一个引用类型变量，对于引用类型变量的引用赋值操作是直接将被引用变量存储的内存地址复制给新声明的变量。也就是将刚刚在 <code>personA</code> 存储的堆内存地址（假设为 <code>0x167</code> ）写入了给 <code>personB</code> 变量分配的栈内存中，即 <code>var personB = 0x167</code> 。</p>
</li>
<li>
<p><code>personB.name = 'Alice'</code></p>
<p>查找 <code>personB</code> 存储的变量值，根据 <code>personB</code> 存储的内存地址从堆内存中找到对应真正的变量值，修改其 <code>name</code> 属性为 <code>Alice</code> 。因为引用数据类型的变量间赋值操作相当于堆内存地址的传递，它们都指向同一个内存地址，所以任何一方对该地址代表的被引用值进行读写的话，其他引用方按照存储着的内存地址找到的值也会是修改后的值。</p>
</li>
</ul>
<p>✅：<strong>引用数据类型变量间的复制操作就是将内存地址传递给新声明的变量，变量间共享着同一个堆内存变量的引用，任何一方修改了该指向的变量，都会互相影响。</strong></p>
<p>再啰嗦提一点，引用类型的变量持有的是被引用变量的<strong>堆内存地址值</strong>，引用赋值的操作也只是修改变量所指向哪个被引用对象，并不能直接修改被引用对象的值。</p>
<p>承接上面的例子：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> personA = &#123;
    <span class="hljs-attr">name</span>: <span class="hljs-string">'Peter'</span>
&#125;
<span class="hljs-keyword">var</span> personB = personA <span class="hljs-comment">// personB是&#123;name:'Peter'&#125;的一个引用</span>
personB.name = <span class="hljs-string">'Alice'</span> <span class="hljs-comment">// 修改personB的值</span>

<span class="hljs-comment">// personA,personB 属于引用数据类型，存放在堆内存中</span>
<span class="hljs-built_in">console</span>.log(&#123;
    personA
&#125;, &#123;
    personB
&#125;)

<span class="hljs-comment">// 再进行一次引用赋值操作</span>
personB = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>] <span class="hljs-comment">// personB是[1,2,3]的一个引用</span>

<span class="hljs-comment">// 打印查看是否影响personA的值</span>
<span class="hljs-built_in">console</span>.log(&#123;
    personA
&#125;, &#123;
    personB
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>可以看到，正如我们上面所说的，我们虽然修改了 <code>personB</code> 的指向，但是对 <code>personA</code> 不会有任何影响。</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/64dc12614f3f4da982019ed49da69784~tplv-k3u1fbpfcp-watermark.image" alt="引用赋值无法修改被引用对象的值" loading="lazy" referrerpolicy="no-referrer"></p>
<p>✅：<strong>当我们进行复制操作时，根据不同的值的类型会有不同的情况。基本类型使用值复制，引用类型使用引用复制。</strong></p>
<p>格局打开之后我们继续探索一下 🚀</p>
<h2 data-id="heading-9">那么 为什么要将引用类型设计成存储在堆内存中呢</h2>
<blockquote>
<p>不知道大家好不好奇这个，我在学习的时候我是蛮好奇的所以特地去查了一下</p>
</blockquote>
<p><strong>堆内存</strong>是无法直接被访问的，当我们需要访问一个堆内存中的值，必须先拿到它的内存地址（hashCode）// 1步，通过内存地址再到堆内存中进行查找 // 2步（堆中的存放着 key-value 键值对，随着堆内存的体积变化，在查找上也需要花费一定时间）。因为<strong>栈内存</strong>中是直接存储的变量值 // 1步，这样一来，同样一个变量存储在栈内存和堆内存中比较，只需要一步就能访问到变量值的栈内存自然比访问堆内存要节约时间，栈运算速度快于栈运算也是一个道理。</p>
<p>所以为了有效利用栈运算速度快的优势，<strong>将较为简单且内存占用较小的原始数据类型存在了栈内存中</strong>，<strong>而较为复杂且内存占用较大的引用类型（随时可能会被修改或被使用、以及可以无限扩充）存放在了堆内存中</strong>，如果将复杂类型存放在了栈内存中，那频繁的操作对象则会影响栈运算的效率，得不偿失。</p>
<p>📌 <a href="https://link.juejin.cn/?target=http%3A%2F%2Fwww.ruanyifeng.com%2Fblog%2F2013%2F11%2Fstack.html" target="_blank" rel="nofollow noopener noreferrer" title="http://www.ruanyifeng.com/blog/2013/11/stack.html" ref="nofollow noopener noreferrer">栈相关内容可参考这篇文章 ></a></p>
<h3 data-id="heading-10">给个堆和栈的比较结论</h3>
<p>// todo</p>
<h2 data-id="heading-11">讲到堆内存又可以想到闭包，从内存的角度理解闭包</h2>
<p>// todo</p>
<h2 data-id="heading-12">说到数据类型，自然而然又可以扯到包装对象</h2>
<p>之前看一些文章，经常会听到有大佬字里行间会提到拆箱装箱，那么拆箱装箱到底是啥呢？</p>
<h3 data-id="heading-13">JavaScript 标准内置对象</h3>
<p>内置对象是每一种语言都会有的基本功能，内置对象定义了某个类型的对象既有的一些属性和方法。比如你定义了一个数值型变量 <code>a</code> ，你会发现不论你是字面量创建还是构造函数创建，这个变量一创建出来就会带有默认的一些属性和方法，这个就是内置对象实现的。它识别到你是某种数据类型就会</p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects" ref="nofollow noopener noreferrer">MDN文档参考 ></a></p>
<p>// todo</p>
<h2 data-id="heading-14">上文都在说内存使用的场景，那么内存是什么时候分配的</h2>
<p>不管是什么程序语言，内存的<strong>生命周期</strong>基本是一致的：</p>
<ol>
<li>分配所需要的内存（Allocate Memory）</li>
<li>使用分配到的内存进行读/写操作（Use Memory）</li>
<li>不需要时将分配到的内存释放/归还（Release Memory）</li>
</ol>
<p>一般的低级语言（e.g. C 语言）内存分配是需要开发者去手动操作的。而像 JavaScript 这种高级语言，内存分配的动作由 JS 底层完成。伴随着变量声明，底层会感知到此时需要分配内存，再根据变量的不同类型，会分配不同的内存大小。对于<strong>原始数据类型</strong>内存是静态的，大小一般是固定的，也相对较小，而对于<strong>引用类型</strong>内存则是动态的，随着变量的变化时实分配内存）。</p>
<p>📌 更多详细内容可以查阅：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FMemory_Management" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management" ref="nofollow noopener noreferrer">MDN 内存管理 ></a></p>
<h2 data-id="heading-15">我们总是会提到的垃圾回收是个啥东东</h2>
<p>// todo</p>
<h2 data-id="heading-16">map写循环在里面改引用（突然想到CodeReview的时候经常会看到有小伙伴有这种写法）</h2>
<p>// todo</p>
<h2 data-id="heading-17">执行栈和作用域链傻傻分不清楚</h2>
<p>其实没有必然联系，一个动态，一个静态</p>
<p>// todo</p>
<h2 data-id="heading-18">说了半天都在说栈内存，那在堆内存中，引用类型 Object 到底是怎么存储的呢？</h2>
<p>// todo</p>
<h2 data-id="heading-19">JavaScript 对象的底层数据结构到底是什么</h2>
<p>首先我们看下 <code>规范ECMA-262</code> 是怎么定义 <code>Object</code> 类型的。<a href="https://link.juejin.cn/?target=https%3A%2F%2F262.ecma-international.org%2F12.0%2F%23sec-object-type" target="_blank" rel="nofollow noopener noreferrer" title="https://262.ecma-international.org/12.0/#sec-object-type" ref="nofollow noopener noreferrer">原文传送门 ></a></p>
<p>一个对象逻辑上是指一堆属性的集合。属性又分为两种：数据属性和访问器属性。</p>
<p><strong>数据属性</strong>将键值与 <code>ECMAScript 语言值</code> 和一组布尔属性相关联。</p>
<p><strong>访问器属性</strong>将键值与一个或两个访问器函数以及一组布尔属性相关联。访问器函数用于存储或检索与属性关联的 <code>ECMAScript 语言值</code> 。</p>
<p><code>ECMAScript 语言值</code> 指的就是我们上文说的 JavaScript 定义的那8种数据类型值。</p>
<p>因为对象的结构是<strong>键值对之间的映射</strong>， <code>key</code> 可以是<strong>任意字符串</strong>， <code>value</code> 可以接受<strong>任意类型的值</strong>，使得对象自然而然的符合了<strong>哈希表</strong>的设计 —— 可以将<strong>键映射到值</strong>的数据结构。</p>
<p>// todo</p>
<h2 data-id="heading-20">Numeric Type Data 精度丢失相关</h2>
<h3 data-id="heading-21">精度在哪里丢失了（整数/小数）</h3>
<p>// todo</p>
<h3 data-id="heading-22">为什么浏览器要自动抹零</h3>
<p>// todo</p>
<h3 data-id="heading-23">JavaScript 为什么要这么设计（即使这会造成精度丢是）</h3>
<p>// todo</p>
<h3 data-id="heading-24">避免精度丢失的方法</h3>
<p>// todo</p>
<p><strong>结束语</strong></p>
<blockquote>
<p>以上就是本文的全部内容，如果哪里不够通透，请<strong>务必</strong>评论我，加以修改！！另外有错误的/遗漏的也欢迎指出，一起探讨！！</p>
</blockquote>
<div align="center">
<p>感谢阅读 👏🏻  / 感谢阅读 🤙🏼  /  感谢阅读 👋🏽</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/62ab195fa8c342418928c0f31cc4d256~tplv-k3u1fbpfcp-watermark.image" alt="再见吧朋友.jpg" loading="lazy" referrerpolicy="no-referrer"></p>
</div></div>  
</div>
            