
---
title: '用 JavaScript 刷 LeetCode 的正确姿势【进阶】'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3b64e61f96274e5fa20d8166861700d4~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 17:36:49 GMT
thumbnail: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3b64e61f96274e5fa20d8166861700d4~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>@charset "UTF-8";.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1:first-child,.markdown-body h2:first-child,.markdown-body h3:first-child,.markdown-body h4:first-child,.markdown-body h5:first-child,.markdown-body h6:first-child&#123;margin-top:-1.5rem;margin-bottom:1rem&#125;.markdown-body h1:before,.markdown-body h2:before,.markdown-body h3:before,.markdown-body h4:before,.markdown-body h5:before,.markdown-body h6:before&#123;content:"#";display:inline-block;color:#3eaf7c;padding-right:.23em&#125;.markdown-body h1&#123;position:relative;font-size:2.5rem;margin-bottom:5px&#125;.markdown-body h1:before&#123;font-size:2.5rem&#125;.markdown-body h2&#123;padding-bottom:.5rem;font-size:2.2rem;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:1.5rem;padding-bottom:0&#125;.markdown-body h4&#123;font-size:1.25rem&#125;.markdown-body h5&#123;font-size:1rem&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body strong&#123;color:#3eaf7c&#125;.markdown-body img&#123;max-width:100%;border-radius:2px;display:block;margin:auto;border:3px solid rgba(62,175,124,.2)&#125;.markdown-body hr&#123;border:none;border-top:1px solid #3eaf7c;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;overflow-x:auto;padding:.2rem .5rem;margin:0;color:#3eaf7c;font-weight:700;font-size:.85em;background-color:rgba(27,31,35,.05);border-radius:3px&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;border-radius:6px;border:2px solid #3eaf7c&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;font-weight:500;text-decoration:none;color:#3eaf7c&#125;.markdown-body a:active,.markdown-body a:hover&#123;border-bottom:1.5px solid #3eaf7c&#125;.markdown-body a:before&#123;content:"⇲"&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #3eaf7c&#125;.markdown-body thead&#123;background:#3eaf7c;color:#fff;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:rgba(62,175,124,.2)&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:.5rem solid;border-color:#42b983;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body details&#123;outline:none;border:none;border-left:4px solid #3eaf7c;padding-left:10px;margin-left:4px&#125;.markdown-body details summary&#123;cursor:pointer;border:none;outline:none;background:#fff;margin:0 -17px&#125;.markdown-body details summary::-webkit-details-marker&#123;color:#3eaf7c&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body ol li::marker&#123;color:#3eaf7c&#125;.markdown-body ul li&#123;list-style:none&#125;.markdown-body ul li:before&#123;content:"•";margin-right:4px;color:#3eaf7c&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>本文已参与好文召集令活动，点击查看：<a href="https://juejin.cn/post/6978685539985653767" target="_blank" title="https://juejin.cn/post/6978685539985653767">后端、大前端双赛道投稿，2万元奖池等你挑战！</a></p>
<p>之前写了篇文章 <a href="https://juejin.cn/post/6844903876206805005" target="_blank" title="https://juejin.cn/post/6844903876206805005">用JavaScript刷LeetCode的正确姿势</a>，简单总结一些用 JavaScript 刷力扣的基本调试技巧。最近又刷了点题，总结了些数据结构和算法，希望能对各为 JSer 刷题提供帮助。</p>
<p>此篇文章主要想给大家一些开箱即用的 JavaScipt 版本的代码模板，涉及到较复杂的知识点，原理部分可能会省略，有需要的话后面有时间可以给部分知识点单独写一篇详细的讲解。</p>
<p><small>走过路过发现 bug 请指出，拯救一个辣鸡（但很帅）的少年就靠您啦！！！</small></p>
<h2 data-id="heading-0">BigInt</h2>
<p>众所周知，JavaScript 只能精确表达 <code>Number.MIN_SAFE_INTEGER(-2^53+1)</code> ~ <code>Number.MAX_SAFE_INTEGER(2^53-1)</code> 的值。</p>
<p>而在一些题目中，常常会有较大的数字计算，这时就会产生误差。举个栗子：在控制台输入下面的两个表达式会得到相同的结果：</p>
<pre><code class="hljs language-js copyable" lang="js">>> <span class="hljs-number">123456789</span>*<span class="hljs-number">123456789</span>      <span class="hljs-comment">// 15241578750190520</span>
>> <span class="hljs-number">123456789</span>*<span class="hljs-number">123456789</span>+<span class="hljs-number">1</span>    <span class="hljs-comment">// 15241578750190520</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>而如果使用 BigInt 则可以精确求值：</p>
<pre><code class="hljs language-js copyable" lang="js">>> <span class="hljs-built_in">BigInt</span>(<span class="hljs-number">123456789</span>)*<span class="hljs-built_in">BigInt</span>(<span class="hljs-number">123456789</span>)              <span class="hljs-comment">// 15241578750190521n</span>
>> <span class="hljs-built_in">BigInt</span>(<span class="hljs-number">123456789</span>)*<span class="hljs-built_in">BigInt</span>(<span class="hljs-number">123456789</span>)+<span class="hljs-built_in">BigInt</span>(<span class="hljs-number">1</span>)    <span class="hljs-comment">// 15241578750190522n</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>可以通过在一个整数字面量后面加 <code>n</code> 的方式定义一个 <code>BigInt</code> ，如：<code>10n</code>，或者调用函数 <code>BigInt()</code>。上面的表达式也可以写成：</p>
<pre><code class="hljs language-js copyable" lang="js">>> <span class="hljs-number">123456789n</span>*<span class="hljs-number">123456789n</span>       <span class="hljs-comment">// 15241578750190521n</span>
>> <span class="hljs-number">123456789n</span>*<span class="hljs-number">123456789n</span>+<span class="hljs-number">1n</span>    <span class="hljs-comment">// 15241578750190522n</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>BigInt</code> 只能与 <code>BigInt</code> 做运算，如果和 <code>Number</code> 进行计算需要先通过 <code>BigInt()</code> 做类型转换。</p>
<p><code>BigInt</code> 支持运算符，<code>+</code>、<code>*</code>、<code>-</code>、<code>**</code>、<code>%</code> 。除 <code>>>></code>（无符号右移）之外的<strong>位操作</strong>也可以支持。因为 <code>BigInt</code> 都是有符号的， <code>>>></code>（无符号右移）不能用于 <code>BigInt</code>。<code>BigInt</code> 不支持单目 (<code>+</code>) 运算符。</p>
<p><code>BigInt</code> 也支持 <code>/</code> 运算符，但是会被向上取整。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> rounded = <span class="hljs-number">5n</span> / <span class="hljs-number">2n</span>; <span class="hljs-comment">// 2n, not 2.5n</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-1">取模运算</h2>
<p>在数据较大时，一般没有办法直接去进行计算，通常都会给一个大质数（例如，<code>1000000007</code>），求对质数取模后的结果。</p>
<p><strong>取模运算的常用性质：</strong></p>
<pre><code class="hljs language-js copyable" lang="js">(a + b) % p = (a % p + b % p) % p
(a - b) % p = (a % p - b % p) % p
(a * b) % p = (a % p * b % p) % p
a ^ b % p = ((a % p) ^ b) % p
<span class="copy-code-btn">复制代码</span></code></pre>
<p>可以看出，加/减/乘/乘方，都可直接在运算的时候取模，至于除法则会复杂一些，稍后再讲。</p>
<p>举一个例子，<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fprime-arrangements%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/prime-arrangements/" ref="nofollow noopener noreferrer">LeetCode 1175. 质数排列</a></p>
<blockquote>
<p>请你帮忙给从 <code>1</code> 到 <code>n</code> 的数设计排列方案，使得所有的「质数」都应该被放在「质数索引」（索引从 <code>1</code> 开始）上；你需要返回可能的方案总数。</p>
<p>让我们一起来回顾一下「质数」：质数一定是大于 <code>1</code> 的，并且不能用两个小于它的正整数的乘积来表示。</p>
<p>由于答案可能会很大，所以请你返回答案 <strong>模 mod</strong> <code>10^9 + 7</code> 之后的结果即可。</p>
</blockquote>
<p>题目很简单，先求出质数的个数 <code>x</code>，则答案为 <code>x!(n-x)!</code>（不理解的可以去看题解区找题解，这里就不详细解释了）</p>
<p>由于阶乘的值很大，所以在求阶乘的时候需要在运算时取模，同时这里用到了上面所说的<code>BigInt</code>。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;number&#125;</span> <span class="hljs-variable">n</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
<span class="hljs-keyword">var</span> numPrimeArrangements = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">n</span>) </span>&#123;
    <span class="hljs-keyword">const</span> mod = <span class="hljs-number">1000000007n</span>;
    <span class="hljs-comment">// 先把100以内的质数打表（不想再写判断质数的代码了</span>
    <span class="hljs-keyword">const</span> prime = [<span class="hljs-number">2</span>,<span class="hljs-number">3</span>,<span class="hljs-number">5</span>,<span class="hljs-number">7</span>,<span class="hljs-number">11</span>,<span class="hljs-number">13</span>,<span class="hljs-number">17</span>,<span class="hljs-number">19</span>,<span class="hljs-number">23</span>,<span class="hljs-number">29</span>,<span class="hljs-number">31</span>,<span class="hljs-number">37</span>,<span class="hljs-number">41</span>,<span class="hljs-number">43</span>,<span class="hljs-number">47</span>,<span class="hljs-number">53</span>,<span class="hljs-number">59</span>,<span class="hljs-number">61</span>,<span class="hljs-number">67</span>,<span class="hljs-number">71</span>,<span class="hljs-number">73</span>,<span class="hljs-number">79</span>,<span class="hljs-number">83</span>,<span class="hljs-number">89</span>,<span class="hljs-number">97</span>];
    <span class="hljs-comment">// 预处理阶乘</span>
    <span class="hljs-keyword">const</span> fac = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Array</span>(n + <span class="hljs-number">1</span>);
    fac[<span class="hljs-number">0</span>] = <span class="hljs-number">1n</span>; <span class="hljs-comment">// 要用bigint</span>
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">1</span>; i <= n; i++) &#123;
        fac[i] = fac[i - <span class="hljs-number">1</span>] * <span class="hljs-built_in">BigInt</span>(i) % mod;
    &#125;
    <span class="hljs-comment">// 先求n以内的质数的个数</span>
    <span class="hljs-keyword">const</span> x = prime.filter(<span class="hljs-function"><span class="hljs-params">i</span> =></span> i <= n).length;
    <span class="hljs-comment">// x!(n-x)!</span>
    <span class="hljs-keyword">return</span> fac[x] * fac[n - x] % mod;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-2">快速幂</h2>
<p>快速幂，顾名思义，快速求幂运算。原理也很简单，比如我们求 <code>x^10</code> 我们可以求 <code>(x^5)^2</code> 可以减少一半的运算。</p>
<p>假设我们求 <code>(x^n)</code></p>
<ul>
<li>如果 <code>n</code> 是偶数，变为求 <code>(x^(n/2))^2</code></li>
<li>如果 <code>n</code> 是奇数，则求 <code>(x^⌊n/2⌋)^2 * x</code> （<code>⌊⌋</code> 是向下取整）</li>
</ul>
<p>因为快速幂涉及到的题目一般数据都很大，需要取模，所以加了取模运算。其中，代码中 <code>n>>=1</code> 相当于 <code>n=n/2</code>，<code>if(n&1)</code>是在判断<code>n</code>是否为奇数。</p>
<p>代码如下：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// x ^ n % mod</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">pow</span>(<span class="hljs-params">x, n, mod</span>) </span>&#123;
    <span class="hljs-keyword">let</span> ans = <span class="hljs-number">1</span>;
    <span class="hljs-keyword">while</span> (n > <span class="hljs-number">0</span>) &#123;
        <span class="hljs-keyword">if</span> (n & <span class="hljs-number">1</span>) ans = ans * x % mod;
        x = x * x % mod;
        n >>= <span class="hljs-number">1</span>;
    &#125;
    <span class="hljs-keyword">return</span> ans;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-3">乘法逆元（数论倒数）</h2>
<p>上面说了除法的取模会复杂一些，其实就是涉及了<strong>乘法逆元</strong>。</p>
<p>当我们求 <code>(a/b)%p</code> 你以为会是简单的 <code>((a%p)/(b%p))%p</code>？当然不是！（反例自己想去Orz</p>
<p>假设有 <code>(a*x)%p=1</code> 则称 <code>a</code>和<code>x</code>关于<code>p</code>互为逆元（<code>a</code> 是 <code>x</code> 关于 <code>p</code> 的逆元，<code>x</code> 是 <code>a</code> 关于 <code>p</code> 的逆元）。比如：<code>2*3%5=1</code> 则 <code>2</code> 和 <code>3</code> 关于 <code>5</code> 互为逆元。</p>
<p>我们把 <code>a</code> 的逆元用 <code>inv(a)</code> 表示。那么：</p>
<pre><code class="hljs language-js copyable" lang="js">(a/b) % p
= ( (a/b) * (b*inv(b)) ) % p <span class="hljs-comment">// 因为(b*inv(b))为1</span>
= (a * inv(b)) % p
= (a%p * inv(b)%p) % p
<span class="copy-code-btn">复制代码</span></code></pre>
<p>现在通过逆元神奇的把除法运算变没了~~~</p>
<p>问题在于怎么求乘法逆元。有两种方式，<strong>费马小定理</strong> 和 <strong>扩展欧几里德算法</strong></p>
<p>不求甚解的我只记了一种解法，即费马小定理：<code>a^(p-1) ≡ 1 (mod p)</code></p>
<p>由费马小定理我们可以推论：<code>a^(p-2) ≡ inv(a)  (mod p)</code></p>
<p>数学家的事我们程序员就不要想那么多啦，记结论就好了。即：</p>
<blockquote>
<p><strong><code>a</code>关于<code>p</code>的逆元为<code>a^(p-2)</code></strong></p>
</blockquote>
<p>好了，现在可以通过快速幂求出 <code>a</code> 的逆元了。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inv</span>(<span class="hljs-params">a, p</span>) </span>&#123;
    <span class="hljs-keyword">return</span> pow(a, p - <span class="hljs-number">2</span>, p); <span class="hljs-comment">// pow是上面定义的快速幂函数</span>
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>（P.S.其实我数论很烂= =，平时都是直接记结论，所以此处讲解可能存在不准确的情况。仅供参考。</p>
<h2 data-id="heading-4">二分答案</h2>
<p>解题的时候往往会考虑枚举答案然后检验枚举的值是否正确。若满足单调性，则满足使用二分法的条件。把这里的枚举换成二分，就变成了“二分答案”。二分答案的时间复杂度是<code>O(logN * (单次验证当前值是否满足条件的复杂度))</code></p>
<p>很多同学在边界问题上经常出bug，也会不小心写个死循环什么的，我总结了一个简单清晰不会出错的二分模板：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// isValid 判断某个值是否合法 根据题目要求实现</span>
<span class="hljs-comment">// 假设 如果x合法则大于x一定合法 如果x不合法则小于x一定不合法</span>
<span class="hljs-comment">// 求最小合法值</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">binaryCalc</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">let</span> l = <span class="hljs-number">0</span>, r = <span class="hljs-number">10000</span>;   <span class="hljs-comment">// 答案可能出现的最小值l和最大值r 根据题目设置具体值</span>
    <span class="hljs-keyword">let</span> ans;    <span class="hljs-comment">// 最终答案</span>
    <span class="hljs-keyword">while</span> (l <= r) &#123;
        <span class="hljs-keyword">let</span> mid = (l + r) >> <span class="hljs-number">1</span>; <span class="hljs-comment">// 位运算取中间值 相当于 floor((l+r)/2)</span>
        <span class="hljs-keyword">if</span> (isValid(mid)) &#123;
            <span class="hljs-comment">// 如果 mid 合法 则 [mid, r] 都是合法的</span>
            <span class="hljs-comment">// 我们先把ans设置为当前获取的合法值的最小值 mid</span>
            ans = mid;
            <span class="hljs-comment">// 然后再去继续去求[l,mid-1]里面是否有合法值</span>
            r = mid - <span class="hljs-number">1</span>;
        &#125; <span class="hljs-keyword">else</span> &#123;
            <span class="hljs-comment">// 如果mid不合法 则[l,mid]都是不合法的</span>
            <span class="hljs-comment">// 我们去[mid+1,r]中找答案</span>
            l = mid + <span class="hljs-number">1</span>;
        &#125;
    &#125;
    <span class="hljs-keyword">return</span> ans;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>举一个简单的例子，<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsqrtx%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/sqrtx/" ref="nofollow noopener noreferrer">LeetCode 69. x 的平方根</a> 是一个二分模板题。题目要求是，给一个数字 <code>x</code> 求平方小于等于 <code>x</code>的最大整数。此处求的是最大值，和模板中对<code>l</code>和<code>r</code>的处理刚好相反。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;number&#125;</span> <span class="hljs-variable">x</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
 <span class="hljs-keyword">var</span> mySqrt = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">x</span>) </span>&#123;
    <span class="hljs-keyword">let</span> l = <span class="hljs-number">0</span>, r = x; <span class="hljs-comment">// 根据题目要求 答案可能的值最小为0 最大为x</span>
    <span class="hljs-keyword">let</span> ans = <span class="hljs-number">0</span>;      <span class="hljs-comment">// 最终答案</span>
    
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">isValid</span>(<span class="hljs-params">v</span>) </span>&#123;       <span class="hljs-comment">// 判断一个数是否合法</span>
        <span class="hljs-keyword">return</span> v * v <= x;
    &#125;

    <span class="hljs-keyword">while</span> (l <= r) &#123;
        <span class="hljs-keyword">let</span> mid = (l + r) >> <span class="hljs-number">1</span>; <span class="hljs-comment">// 取中间值</span>
        <span class="hljs-keyword">if</span> (isValid(mid)) &#123;
            ans = mid;
            l = mid + <span class="hljs-number">1</span>;
        &#125; <span class="hljs-keyword">else</span> &#123;
            r = mid - <span class="hljs-number">1</span>;
        &#125;
    &#125;
    <span class="hljs-keyword">return</span> ans;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-5">并查集</h2>
<p>个人觉得并查集是非常精妙且简洁优雅的数据结构，推荐学习。</p>
<p>并查集应用场景为，存在一些元素，分别包含在不同集合中，需要快速合并两个集合，同时可快速求出两个元素是否处于同一集合。</p>
<p>简单的理解并查集的实现，就是把每一个集合都当做一棵树，每个节点都有一个父节点，每棵树都有一个根节点（根节点的父节点为其本身）。</p>
<p>判断是否同一集合：我们可以顺着节点的父节点找到该节点所在集合的根节点。当我们确定两个集合拥有同一个根节点，则证明两个节点处于同一个集合。</p>
<p>合并操作：分别取得两个节点所在集合的根节点，把其中一个根节点的父节点设置为另一个根节点即可。</p>
<p>可能说的比较抽象，想详细了解的同学可以自己深入学习，这里直接给出代码模板。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">UnionFind</span> </span>&#123;
    <span class="hljs-function"><span class="hljs-title">constructor</span>(<span class="hljs-params">n</span>)</span> &#123;
        <span class="hljs-built_in">this</span>.n = n; <span class="hljs-comment">// 节点个数</span>
        <span class="hljs-comment">// 记录每个节点的父节点 初始时每个节点自己为一个集合 即每个节点的父节点都是其本身</span>
        <span class="hljs-built_in">this</span>.father = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Array</span>(n).fill().map(<span class="hljs-function">(<span class="hljs-params">v, index</span>) =></span> index);
    &#125;
    <span class="hljs-comment">// 寻找一个节点的根节点</span>
    <span class="hljs-function"><span class="hljs-title">find</span>(<span class="hljs-params">x</span>)</span> &#123;
        <span class="hljs-comment">// 如果父节点为其本身 则证明是根节点</span>
        <span class="hljs-keyword">if</span> (x == <span class="hljs-built_in">this</span>.father[x]) &#123;
            <span class="hljs-keyword">return</span> x;
        &#125;
        <span class="hljs-comment">// 递归查询</span>
        <span class="hljs-comment">// 此处进行了路径压缩 即将x的父节点直接设置为根节点 下一次查询的时候 将减少递归次数</span>
        <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.father[x] = <span class="hljs-built_in">this</span>.find(<span class="hljs-built_in">this</span>.father[x]);
    &#125;
    <span class="hljs-comment">// 合并x和y所在的两个集合</span>
    <span class="hljs-function"><span class="hljs-title">merge</span>(<span class="hljs-params">x, y</span>)</span> &#123;
        <span class="hljs-keyword">const</span> xRoot = <span class="hljs-built_in">this</span>.find(x); <span class="hljs-comment">// 找到x的根节点</span>
        <span class="hljs-keyword">const</span> yRoot = <span class="hljs-built_in">this</span>.find(y); <span class="hljs-comment">// 找到y的根节点</span>
        <span class="hljs-built_in">this</span>.father[xRoot] = yRoot; <span class="hljs-comment">// 将xRoot的父节点设置为yRoot 即可将两个集合合并</span>
    &#125;
    <span class="hljs-comment">// 计算集合个数</span>
    <span class="hljs-function"><span class="hljs-title">count</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-comment">// 其实就是查询根节点的个数</span>
        <span class="hljs-keyword">let</span> cnt = <span class="hljs-number">0</span>;
        <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i < <span class="hljs-built_in">this</span>.n; i++) &#123;
            <span class="hljs-keyword">if</span> (<span class="hljs-built_in">this</span>.father[i] === i) &#123; <span class="hljs-comment">// 判断是否为根节点</span>
                cnt++;
            &#125;
        &#125;
        <span class="hljs-keyword">return</span> cnt;
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>找一个并查集的题目，方便大家理解并查集的妙处。并查集的题目可以出得非常灵活，可能不会轻易看出是并查集。 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmost-stones-removed-with-same-row-or-column%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/most-stones-removed-with-same-row-or-column/" ref="nofollow noopener noreferrer">LeetCode 947. 移除最多的同行或同列石头
</a></p>
<blockquote>
<p><code>n</code> 块石头放置在二维平面中的一些整数坐标点上。每个坐标点上最多只能有一块石头。</p>
<p>如果一块石头的 <strong>同行或者同列</strong> 上有其他石头存在，那么就可以移除这块石头。</p>
<p>给你一个长度为 <code>n</code> 的数组 <code>stones</code> ，其中 <code>stones[i] = [xi, yi]</code> 表示第 <code>i</code> 块石头的位置，返回 <strong>可以移除的石子</strong> 的最大数量。</p>
</blockquote>
<p>此处参考了官方的<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmost-stones-removed-with-same-row-or-column%2Fsolution%2F947-yi-chu-zui-duo-de-tong-xing-huo-tong-ezha%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/most-stones-removed-with-same-row-or-column/solution/947-yi-chu-zui-duo-de-tong-xing-huo-tong-ezha/" ref="nofollow noopener noreferrer">题解</a></p>
<p>把二维坐标平面上的石头想象成图的顶点，如果两个石头横坐标相同、或者纵坐标相同，在它们之间形成一条边。</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3b64e61f96274e5fa20d8166861700d4~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>根据可以移除石头的规则：如果一块石头的 <strong>同行或者同列</strong> 上有其他石头存在，那么就可以移除这块石头。可以发现：一定可以把一个连通图里的所有顶点根据这个规则删到只剩下一个顶点。</p>
<p>我们遍历所有的石头，发现如果有两个石头的横坐标或者纵坐标相等，则证明这两块石头应该在同一个集合（即上面说的连通图）里。那么最后每个集合只留一块石头，剩下的则全部可以被移除。</p>
<p>AC代码：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// 定义 UnionFind 相关代码</span>
<span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;number[][]&#125;</span> <span class="hljs-variable">stones</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
 <span class="hljs-keyword">var</span> removeStones = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">stones</span>) </span>&#123;
    <span class="hljs-keyword">let</span> n = stones.length;
    <span class="hljs-keyword">let</span> uf = <span class="hljs-keyword">new</span> UnionFind(n);
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i < n; i++) &#123;
        <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> j = i + <span class="hljs-number">1</span>; j < n; j++) &#123;
            <span class="hljs-comment">// 有两个石头的横坐标或者纵坐标相等 则合并</span>
            <span class="hljs-keyword">if</span> (stones[i][<span class="hljs-number">0</span>] == stones[j][<span class="hljs-number">0</span>] || stones[i][<span class="hljs-number">1</span>] == stones[j][<span class="hljs-number">1</span>]) &#123;
                uf.merge(i, j);
            &#125;
        &#125;
    &#125;
    <span class="hljs-comment">// 石头总数减去集合的个数就是答案</span>
    <span class="hljs-keyword">return</span> n - uf.count();
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-6">KMP</h2>
<p>KMP 被一些算法初学者认为是高难度数据结构，一般遇到直接放弃那种。所以我想了下几句话应该也解释不清，那就跳过原理直接上模板吧。:P</p>
<p>先简单说一下背景，KMP 解决的是子串查找的问题。给两个字符串<code>S</code>和<code>T</code>，求<code>T</code>是否是<code>S</code>的子串。解决方法是先预处理<code>T</code>，求出<code>T</code>的<code>next</code>数组，其中<code>next[i]</code>代表<code>T</code>的子串<code>T[0...i-1]</code>（即<code>T.substring(0, i)</code>）<strong>最长相等的前缀后缀</strong> 的长度。</p>
<p>嘛，最长相等的前缀后缀，就是说，比如字符串<code>"abcuuabc"</code>最长相等的前缀后缀就是<code>abc</code>，那么其长度就应该是<code>3</code>。</p>
<p>然后借助<code>next</code>数组，可以在线性时间复杂度内求出<code>T</code>是否为<code>S</code>的子串，首次出现下标，以及出现次数。</p>
<p>模板代码：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// 求字符串 s 的 next 数组</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getNext</span>(<span class="hljs-params">s</span>) </span>&#123;
    <span class="hljs-keyword">let</span> len = s.length;
    <span class="hljs-keyword">let</span> next = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Array</span>(len + <span class="hljs-number">1</span>);
    <span class="hljs-keyword">let</span> j = <span class="hljs-number">0</span>, k = -<span class="hljs-number">1</span>;
    next[<span class="hljs-number">0</span>] = -<span class="hljs-number">1</span>;
    <span class="hljs-keyword">while</span> (j < len) &#123;
        <span class="hljs-keyword">if</span> (k == -<span class="hljs-number">1</span> || s[j] === s[k]) next[++j] = ++k;
        <span class="hljs-keyword">else</span> k = next[k];
    &#125;
    <span class="hljs-keyword">return</span> next;
&#125;
<span class="hljs-comment">// 求字符串 t 在字符串 s 中第一次出现的下标 不存在则返回 -1</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">findIndex</span>(<span class="hljs-params">s, t</span>) </span>&#123;
    <span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>, j = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">let</span> next = getNext(t);
    <span class="hljs-keyword">let</span> slen = s.length, tlen = t.length;
    <span class="hljs-keyword">while</span> (i < slen && j < tlen) &#123;
        <span class="hljs-keyword">if</span> (j === -<span class="hljs-number">1</span> || s[i] === t[j]) ++i, ++j;
        <span class="hljs-keyword">else</span> j = next[j];
    &#125;
    <span class="hljs-keyword">return</span> j === tlen ? i - tlen : -<span class="hljs-number">1</span>;
&#125;
<span class="hljs-comment">// 求字符串 t 在字符串 s 出现的次数</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">findCount</span>(<span class="hljs-params">s, t</span>) </span>&#123;
    <span class="hljs-keyword">let</span> ans = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>, j = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">let</span> next = getNext(t);
    <span class="hljs-keyword">let</span> slen = s.length, tlen = t.length;
    <span class="hljs-keyword">while</span> (i < slen && j < tlen) &#123;
        <span class="hljs-keyword">if</span> (j === -<span class="hljs-number">1</span> || s[i] === t[j]) ++i, ++j;
        <span class="hljs-keyword">else</span> j = next[j];
        <span class="hljs-keyword">if</span> (j === tlen) &#123;
            ++ans;
            j = next[j];
        &#125;
    &#125;
    <span class="hljs-keyword">return</span> ans;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如果多次计算子串相同的话，<code>next</code>数组可以预处理，不需要每次在求<code>index</code>时再计算。</p>
<p>举个例子吧，<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flongest-happy-prefix%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/longest-happy-prefix/" ref="nofollow noopener noreferrer">LeetCode 1392. 最长快乐前缀</a></p>
<blockquote>
<p>「快乐前缀」是在原字符串中既是 <strong>非空</strong> 前缀也是后缀（不包括原字符串自身）的字符串。</p>
<p>给你一个字符串 s，请你返回它的 <strong>最长快乐前缀</strong>。</p>
<p>如果不存在满足题意的前缀，则返回一个空字符串。</p>
</blockquote>
<p>我们会发现这不就是 <code>next</code> 数组么，所以我记得这次周赛会 KMP 的同学直接 copy 就得分了.....</p>
<p>AC代码；</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// getNext 定义参考上面模板</span>
<span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;string&#125;</span> <span class="hljs-variable">s</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;string&#125;</span></span>
 */</span>
<span class="hljs-keyword">var</span> longestPrefix = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">s</span>) </span>&#123;
    <span class="hljs-keyword">let</span> len = s.length;
    <span class="hljs-keyword">let</span> next = getNext(s);
    <span class="hljs-keyword">let</span> ansLen = next[len] == len ? len - <span class="hljs-number">1</span> : next[len]; <span class="hljs-comment">// 不包含原字符串 需要特殊判断下</span>
    <span class="hljs-keyword">return</span> s.substring(<span class="hljs-number">0</span>, ansLen);
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>再来一个 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fimplement-strstr%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/implement-strstr/" ref="nofollow noopener noreferrer">LeetCode 28. 实现 strStr()</a> 求一个字符串在另一个字符串中首次出现的位置，就是<code>indexOf</code>的实现，其实也就是模板中的 <code>findIndex</code> 函数。</p>
<p>AC代码：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// findIndex 定义参考模板</span>
<span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;string&#125;</span> <span class="hljs-variable">haystack</span></span>
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;string&#125;</span> <span class="hljs-variable">needle</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
<span class="hljs-keyword">var</span> strStr = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">haystack, needle</span>) </span>&#123;
    <span class="hljs-keyword">return</span> findIndex(haystack, needle);
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-7">优先队列（堆）</h2>
<p>优先队列，我们给每个元素定义优先级，每次取队列中的值都取的是优先级最大的数。</p>
<p>其他的语言中都自带优先队列的实现，JSer就只能QAQ……所以我自己写了一个优先队列，就是通过堆来实现。（原理就不讲啦，学过堆排序的应该懂~（趴</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">PriorityQueue</span> </span>&#123;
    <span class="hljs-comment">/**
     * 构造函数 可以传入比较函数自定义优先级 默认是最小值排在最前
     * <span class="hljs-doctag">@param <span class="hljs-type">&#123;function&#125;</span> </span>compareFunc 比较函数 compareFunc(a, b) 为 true 表示 a 的优先级 > b
     */</span>
    <span class="hljs-function"><span class="hljs-title">constructor</span>(<span class="hljs-params">compareFunc</span>)</span> &#123;
        <span class="hljs-built_in">this</span>.queue = [];
        <span class="hljs-built_in">this</span>.func = compareFunc || (<span class="hljs-function">(<span class="hljs-params">a, b</span>) =></span> a < b);
    &#125;
    <span class="hljs-comment">/**
     * 向优先队列添加一个元素
     */</span>
    <span class="hljs-function"><span class="hljs-title">push</span>(<span class="hljs-params">ele</span>)</span> &#123;
        <span class="hljs-built_in">this</span>.queue.push(ele);
        <span class="hljs-built_in">this</span>.pushup(<span class="hljs-built_in">this</span>.size() - <span class="hljs-number">1</span>)
    &#125;
    <span class="hljs-comment">/**
     * 弹出最小值并返回
     */</span>
    <span class="hljs-function"><span class="hljs-title">pop</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-keyword">let</span> &#123; queue &#125; = <span class="hljs-built_in">this</span>;
        <span class="hljs-keyword">if</span> (queue.length <= <span class="hljs-number">1</span>) <span class="hljs-keyword">return</span> queue.pop();
        
        <span class="hljs-keyword">let</span> min = queue[<span class="hljs-number">0</span>];
        queue[<span class="hljs-number">0</span>] = queue.pop();
        <span class="hljs-built_in">this</span>.pushdown(<span class="hljs-number">0</span>);
        <span class="hljs-keyword">return</span> min;
    &#125;
    <span class="hljs-comment">/**
     * 返回最小值
     */</span>
    <span class="hljs-function"><span class="hljs-title">top</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.size() ? <span class="hljs-built_in">this</span>.queue[<span class="hljs-number">0</span>] : <span class="hljs-literal">null</span>;
    &#125;
    <span class="hljs-comment">/**
     * 返回队列中元素的个数
     */</span>
    <span class="hljs-function"><span class="hljs-title">size</span>(<span class="hljs-params"></span>)</span> &#123;
        <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.queue.length;
    &#125;
    <span class="hljs-comment">/**
     * 初始化堆
     */</span>
    <span class="hljs-function"><span class="hljs-title">setQueue</span>(<span class="hljs-params">queue</span>)</span> &#123;
        <span class="hljs-built_in">this</span>.queue = queue;
        <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = (<span class="hljs-built_in">this</span>.size() >> <span class="hljs-number">1</span>); i >= <span class="hljs-number">0</span>; i--) &#123;
            <span class="hljs-built_in">this</span>.pushdown(i);
        &#125;
    &#125;
    <span class="hljs-comment">/**
     * 调整以保证 queue[index] 是子树中最小的
     * */</span>
    <span class="hljs-function"><span class="hljs-title">pushdown</span>(<span class="hljs-params">index</span>)</span> &#123;
        <span class="hljs-keyword">let</span> &#123; queue, func &#125; = <span class="hljs-built_in">this</span>;
        <span class="hljs-keyword">let</span> fa = index;
        <span class="hljs-keyword">let</span> cd = index * <span class="hljs-number">2</span> + <span class="hljs-number">1</span>;
        <span class="hljs-keyword">let</span> size = queue.length;
        <span class="hljs-keyword">while</span> (cd < size) &#123;
            <span class="hljs-keyword">if</span> (cd + <span class="hljs-number">1</span> < size && func(queue[cd + <span class="hljs-number">1</span>], queue[cd])) cd++;
            <span class="hljs-keyword">if</span> (func(queue[fa], queue[cd])) <span class="hljs-keyword">break</span>;
            <span class="hljs-comment">// 交换 queue[fa] 和 queue[cd]</span>
            [queue[fa], queue[cd]] = [queue[cd], queue[fa]];
            <span class="hljs-comment">// 继续处理子树</span>
            fa = cd;
            cd = fa * <span class="hljs-number">2</span> + <span class="hljs-number">1</span>;
        &#125;
    &#125;
    <span class="hljs-comment">/**
     * 调整 index 到合法位置
     */</span>
    <span class="hljs-function"><span class="hljs-title">pushup</span>(<span class="hljs-params">index</span>)</span> &#123;
        <span class="hljs-keyword">let</span> &#123; queue, func &#125; = <span class="hljs-built_in">this</span>;
        <span class="hljs-keyword">while</span> (index) &#123;
            <span class="hljs-keyword">const</span> fa = (index - <span class="hljs-number">1</span>) >> <span class="hljs-number">1</span>;
            <span class="hljs-keyword">if</span> (func(queue[fa], queue[index])) &#123;
                <span class="hljs-keyword">break</span>;
            &#125;
            [queue[fa], queue[index]] = [queue[index], queue[fa]];
            index = fa;
        &#125;
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>举个例子，<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmerge-k-sorted-lists%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/merge-k-sorted-lists/" ref="nofollow noopener noreferrer">LeetCode 23. 合并K个升序链表</a> 一道困难题目哦~</p>
<blockquote>
<p>给你一个链表数组，每个链表都已经按升序排列。</p>
<p>请你将所有链表合并到一个升序链表中，返回合并后的链表。</p>
</blockquote>
<p>做法很简单，把链表都放到优先队列里，每次取值最小的链表就行。具体实现看代码。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;ListNode[]&#125;</span> <span class="hljs-variable">lists</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;ListNode&#125;</span></span>
 */</span>
<span class="hljs-keyword">var</span> mergeKLists = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">lists</span>) </span>&#123;
    <span class="hljs-keyword">let</span> queue = <span class="hljs-keyword">new</span> PriorityQueue(<span class="hljs-function">(<span class="hljs-params">a, b</span>) =></span> a.val < b.val);

    lists.forEach(<span class="hljs-function"><span class="hljs-params">list</span> =></span> &#123;
        list && queue.push(list);
    &#125;);

    <span class="hljs-keyword">const</span> dummy = <span class="hljs-keyword">new</span> ListNode(<span class="hljs-number">0</span>);
    <span class="hljs-keyword">let</span> cur = dummy;

    <span class="hljs-keyword">while</span> (queue.size()) &#123;
        <span class="hljs-keyword">let</span> node = queue.pop();
        <span class="hljs-keyword">if</span> (node.next) queue.push(node.next);
        cur.next = <span class="hljs-keyword">new</span> ListNode(node.val);
        cur = cur.next;
    &#125;

    <span class="hljs-keyword">return</span> dummy.next;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-8">Trie（字典树/前缀树）</h2>
<p>字典树应该算是一个比较简单而且直观的数据结构~字典树模板题可以看 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fimplement-trie-prefix-tree%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/implement-trie-prefix-tree/" ref="nofollow noopener noreferrer">LeetCode 208. 实现 Trie (前缀树)</a></p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">/**
 * Initialize your data structure here.
 */</span>
<span class="hljs-keyword">var</span> Trie = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">this</span>.nodes = [];
&#125;;

<span class="hljs-comment">/**
 * Inserts a word into the trie. 
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;string&#125;</span> <span class="hljs-variable">word</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;void&#125;</span></span>
 */</span>
Trie.prototype.insert = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">word</span>) </span>&#123;
    <span class="hljs-keyword">let</span> nodes = <span class="hljs-built_in">this</span>.nodes;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> w <span class="hljs-keyword">of</span> word) &#123;
        <span class="hljs-keyword">if</span> (!nodes[w]) &#123;
            nodes[w] = &#123;&#125;;
        &#125;
        nodes = nodes[w];
    &#125;
    nodes.end = <span class="hljs-literal">true</span>;
&#125;;

<span class="hljs-comment">/**
 * Returns if the word is in the trie. 
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;string&#125;</span> <span class="hljs-variable">word</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;boolean&#125;</span></span>
 */</span>
Trie.prototype.search = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">word</span>) </span>&#123;
    <span class="hljs-keyword">let</span> nodes = <span class="hljs-built_in">this</span>.nodes;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> w <span class="hljs-keyword">of</span> word) &#123;
        <span class="hljs-keyword">if</span> (!nodes[w]) &#123;
            <span class="hljs-keyword">return</span> <span class="hljs-literal">false</span>;
        &#125;
        nodes = nodes[w];
    &#125;
    <span class="hljs-keyword">return</span> !!nodes.end;
&#125;;

<span class="hljs-comment">/**
 * Returns if there is any word in the trie that starts with the given prefix. 
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;string&#125;</span> <span class="hljs-variable">prefix</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;boolean&#125;</span></span>
 */</span>
Trie.prototype.startsWith = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">prefix</span>) </span>&#123;
    <span class="hljs-keyword">let</span> nodes = <span class="hljs-built_in">this</span>.nodes;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> w <span class="hljs-keyword">of</span> prefix) &#123;
        <span class="hljs-keyword">if</span> (!nodes[w]) &#123;
            <span class="hljs-keyword">return</span> <span class="hljs-literal">false</span>;
        &#125;
        nodes = nodes[w];
    &#125;
    <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span>;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>字典树的变种应用，<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmaximum-xor-of-two-numbers-in-an-array%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/" ref="nofollow noopener noreferrer">LeetCode 421. 数组中两个数的最大异或值</a> 参考：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmaximum-xor-of-two-numbers-in-an-array%2Fsolution%2Fshu-zu-zhong-liang-ge-shu-de-zui-da-yi-h-n9m9%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/solution/shu-zu-zhong-liang-ge-shu-de-zui-da-yi-h-n9m9/" ref="nofollow noopener noreferrer">题解</a></p>
<p>我们也可以将数组中的元素看成长度为 <code>31</code> 的字符串，字符串中只包含 <code>0</code> 和 <code>1</code>。如果我们将字符串放入字典树中，那么在字典树中查询一个字符串的过程，恰好就是从高位开始确定每一个二进制位的过程。对于一个数求异或和的最大值，就是从最高位开始，每一位都找异或和最大的那个分支。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> Trie = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">this</span>.nodes = [];
&#125;;
Trie.prototype.insert = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">digit</span>) </span>&#123;
    <span class="hljs-keyword">let</span> nodes = <span class="hljs-built_in">this</span>.nodes;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> d <span class="hljs-keyword">of</span> digit) &#123;
        <span class="hljs-keyword">if</span> (!nodes[d]) &#123;
            nodes[d] = [];
        &#125;
        nodes = nodes[d];
    &#125;
&#125;;
Trie.prototype.maxXor = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">digit</span>) </span>&#123;
    <span class="hljs-keyword">let</span> xor = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">let</span> nodes = <span class="hljs-built_in">this</span>.nodes;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i < digit.length; i++) &#123;
        <span class="hljs-keyword">let</span> d = digit[i];
        <span class="hljs-keyword">if</span> (nodes[d ^ <span class="hljs-number">1</span>]) &#123;
            xor += <span class="hljs-number">1</span> << (digit.length - i - <span class="hljs-number">1</span>);
            nodes = nodes[d ^ <span class="hljs-number">1</span>];
        &#125; <span class="hljs-keyword">else</span> &#123;
            nodes = nodes[d];
        &#125;
    &#125;
    <span class="hljs-keyword">return</span> xor;
&#125;;

<span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;number[]&#125;</span> <span class="hljs-variable">nums</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
<span class="hljs-keyword">var</span> findMaximumXOR = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">nums</span>) </span>&#123;
    <span class="hljs-keyword">let</span> trie = <span class="hljs-keyword">new</span> Trie();
    <span class="hljs-keyword">let</span> maxXor = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> x <span class="hljs-keyword">of</span> nums) &#123;
        <span class="hljs-keyword">let</span> binaryX = x.toString(<span class="hljs-number">2</span>);
        <span class="hljs-comment">// 因为 0 <= nums[i] <= 2^31 - 1 所以最多为31位</span>
        <span class="hljs-comment">// 补前缀0统一变成31位</span>
        binaryX = (<span class="hljs-string">'0'</span>.repeat(<span class="hljs-number">31</span>) + binaryX).substr(-<span class="hljs-number">31</span>);
        <span class="hljs-comment">// 插入Trie</span>
        trie.insert(binaryX);
        maxXor = <span class="hljs-built_in">Math</span>.max(maxXor, trie.maxXor(binaryX));
    &#125;
    <span class="hljs-keyword">return</span> maxXor;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-9">总结</h2>
<p>暂时就想到这么多比较常见的数据结构。如果有其他的可以在评论区补充，如果我会的话会后续加上的。</p>
<p>JSer冲鸭！！！</p>
<h2 data-id="heading-10">参考资料</h2>
<ul>
<li><a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FBigInt" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt" ref="nofollow noopener noreferrer">developer.mozilla.org/zh-CN/docs/…</a></li>
<li><a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.cnblogs.com%2Flinyujun%2Fp%2F5194184.html" target="_blank" rel="nofollow noopener noreferrer" title="https://www.cnblogs.com/linyujun/p/5194184.html" ref="nofollow noopener noreferrer">www.cnblogs.com/linyujun/p/…</a></li>
</ul></div>  
</div>
            