
---
title: '阮一峰JS三轮复习——第三天'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=4118'
author: 掘金
comments: false
date: Tue, 13 Jul 2021 05:56:11 GMT
thumbnail: 'https://picsum.photos/400/300?random=4118'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">4. 语法专题</h1>
<h2 data-id="heading-1">4.1 数据类型转换</h2>
<p>运算符对数据类型是有要求的。如果运算符发现，运算子的类型与预期不符，就会自动转换类型。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-string">'4'</span> - <span class="hljs-string">'3'</span> <span class="hljs-comment">// 1</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-2">4.1.1 强制转换</h3>
<h4 data-id="heading-3">1. Number()</h4>
<ol>
<li>原始类型值</li>
</ol>
<p>Number函数将字符串转为数值，要比parseInt函数严格很多。基本上，只要有一个字符无法转成数值，整个字符串就会被转为NaN。parseInt逐个解析字符，而Number函数整体转换字符串的类型</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-built_in">parseInt</span>(<span class="hljs-string">'42 cats'</span>) <span class="hljs-comment">// 42</span>
<span class="hljs-built_in">Number</span>(<span class="hljs-string">'42 cats'</span>) <span class="hljs-comment">// NaN</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-4">2. String()</h4>
<p>String方法的参数如果是对象，返回一个类型字符串；如果是数组，返回该数组的字符串形式。String方法背后的转换规则，与Number方法基本相同，只是互换了valueOf方法和toString方法的执行顺序。</p>
<h4 data-id="heading-5">3. 自动转换</h4>
<p>自动转换的规则是这样的：预期什么类型的值，就调用该类型的转换函数。比如，某个位置预期为字符串，就调用String()函数进行转换。如果该位置既可以是字符串，也可能是数值，那么默认转为数值。</p>
<h2 data-id="heading-6">4.2 错误处理机制</h2>
<ol>
<li>SyntaxError: 解析代码时发生的语法错误。</li>
</ol>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> 1a;
<span class="hljs-comment">// Uncaught SyntaxError: Invalid or unexpected token</span>

<span class="hljs-comment">// 缺少括号</span>
<span class="hljs-built_in">console</span>.log <span class="hljs-string">'hello'</span>);
<span class="hljs-comment">// Uncaught SyntaxError: Unexpected string</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<ol start="2">
<li>RangeError: 一个值超出有效范围时发生的错误,一是数组长度为负数，二是Number对象的方法参数超出范围，以及函数堆栈超过最大值。</li>
<li>TypeError: 变量或者参数不是预期类型时发生的错误。</li>
</ol>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">new</span> <span class="hljs-number">123</span>
<span class="hljs-comment">// Uncaught TypeError: 123 is not a constructor</span>

<span class="hljs-keyword">var</span> obj = &#123;&#125;;
obj.unknownMethod()
<span class="hljs-comment">// Uncaught TypeError: obj.unknownMethod is not a function</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-7">4.2.1 throw语句</h3>
<p>throw语句的作用是手动中断程序执行，抛出一个错误。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> x = -<span class="hljs-number">1</span>;

<span class="hljs-keyword">if</span> (x <= <span class="hljs-number">0</span>) &#123;
  <span class="hljs-keyword">throw</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">'x 必须为正数'</span>);
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-8">4.2.2 try...catch 结构</h3>
<p>一旦发生错误，程序就中止执行了。JavaScript 提供了try...catch结构，允许对错误进行处理，选择是否往下执行。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">try</span> &#123;
  <span class="hljs-keyword">throw</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">'出错了!'</span>);
&#125; <span class="hljs-keyword">catch</span> (e) &#123;
  <span class="hljs-built_in">console</span>.log(e.name + <span class="hljs-string">": "</span> + e.message);
  <span class="hljs-built_in">console</span>.log(e.stack);
&#125;
<span class="hljs-comment">// Error: 出错了!</span>
<span class="hljs-comment">//   at <anonymous>:3:9</span>
<span class="hljs-comment">//   ...</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>上面代码中，try代码块抛出错误（上例用的是throw语句），JavaScript 引擎就立即把代码的执行，转到catch代码块，或者说错误被catch代码块捕获了。catch接受一个参数，表示try代码块抛出的值。</p>
<h3 data-id="heading-9">4.2.3 finally 代码块</h3>
<p>try...catch结构允许在最后添加一个finally代码块，表示不管是否出现错误，都必需在最后运行的语句。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">cleansUp</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-keyword">try</span> &#123;
    <span class="hljs-keyword">throw</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">'出错了……'</span>);
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'此行不会执行'</span>);
  &#125; <span class="hljs-keyword">finally</span> &#123;
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'完成清理工作'</span>);
  &#125;
&#125;

cleansUp()
<span class="hljs-comment">// 完成清理工作</span>
<span class="hljs-comment">// Uncaught Error: 出错了……</span>
<span class="hljs-comment">//    at cleansUp (<anonymous>:3:11)</span>
<span class="hljs-comment">//    at <anonymous>:10:1</span>
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            