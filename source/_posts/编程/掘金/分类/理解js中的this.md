
---
title: '理解js中的this'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=8410'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 19:22:11 GMT
thumbnail: 'https://picsum.photos/400/300?random=8410'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>人生三大问题，我是谁？我从哪儿来？我到哪里去？哲学上，没有人能真正回答这三个问题，同样，在js中，因为情况太多，要想真正理解各种情况下js中this代表什么也是一比较难的事情，更加尴尬的是，this这个关键字，在js中不但复杂而且使用的很多，以至于不弄懂this到底代表什么，就不敢去写js，更不必谈去看别人的代码，更加的吃力。</p>
<p>理解this指向的一个原则，this的指向一定是一个对象，永远指向函数运行时所在的对象，而不是函数被创建时所在的对象,而且这个对象是最后调用函数的那个对象,<strong>但是箭头函数和bind绑定过的函数除外</strong>。this的四大绑定规则:默认绑定、显式绑定、隐式绑定、new绑定，前面已经说到this不但复杂而且很重要，<strong>但是也不要怕，只要理解了显示绑定，基本就能掌握this，当然是建立在大量练习的前提下</strong>，因为隐式绑定和默认绑定就是从显式绑定派生来的，下面结合各种情况分析this的指向。</p>
<h1 data-id="heading-0">call 、apply与this(显式绑定)</h1>
<p>call和apply的作用是给函数重新指定调用者，指定this的指向，在js中函数也是对象，既然是对象，就有方法，call、apply就是函数的方法，可以显式指定函数的this指向的对象，即call、apply第一个参数。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">foo</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">console</span>.log( <span class="hljs-built_in">this</span>.name);
&#125; 
 
<span class="hljs-keyword">var</span> obj = &#123;
    <span class="hljs-attr">name</span>: <span class="hljs-string">'小明'</span>
&#125;; 
 
foo.call(obj); <span class="hljs-comment">// => 小明</span>
foo.apply(obj); <span class="hljs-comment">// => 小明</span>

<span class="hljs-keyword">var</span> tmp = foo.bind(obj)
tmp() <span class="hljs-comment">// => 小明</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-1">bind与this（显式绑定，硬绑定)</h1>
<p>bind和call,apply有点类似，只不过后者是立即执行，而bind是返回一个永远绑定到某对象的函数，bind 方法来设置函数的 this 值，而不用考虑函数如何被调用的。调用 f.bind(someObject) 会创建一个与 f 具有相同函数体和作用域的函数，但是在这个新函数中，this 将永久地被绑定到了 bind 的第一个参数，无论这个函数是如何被调用的。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">foo</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.a;
&#125;
<span class="hljs-keyword">var</span> bar = foo.bind(&#123;
    <span class="hljs-attr">a</span>: <span class="hljs-string">'hello'</span>
&#125;);
<span class="hljs-built_in">console</span>.log(bar()) <span class="hljs-comment">// hello</span>
<span class="hljs-keyword">var</span> o = &#123;
    <span class="hljs-attr">a</span>: <span class="hljs-string">'world'</span>,
    <span class="hljs-attr">foo</span>: foo,
    <span class="hljs-attr">bar</span>: bar
&#125;;
<span class="hljs-built_in">console</span>.log(o.foo(), o.bar()) <span class="hljs-comment">// world hello</span>

<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-2">全局的this(默认绑定)</h1>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">foo</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">console</span>.log( <span class="hljs-built_in">this</span>);
&#125; 
foo();<span class="hljs-comment">//window</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>用显式绑定的方式去理解，以上代码可以理解为foo.call(window)。</p>
<h1 data-id="heading-3">new与this</h1>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Person</span>(<span class="hljs-params">n, a, g</span>)</span>&#123;
  <span class="hljs-built_in">this</span>.name = n;
  <span class="hljs-built_in">this</span>.age = a;
  <span class="hljs-built_in">this</span>.gender = g;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>);
&#125;
<span class="hljs-comment">//作为构造函数使用</span>
<span class="hljs-keyword">var</span> o = <span class="hljs-keyword">new</span> Person(<span class="hljs-string">"Lily"</span>, <span class="hljs-number">18</span>, <span class="hljs-string">"F"</span>); <span class="hljs-comment">//this为当前对象 Person &#123;name: "Lily", age: 18, gender: "F"&#125;</span>

<span class="copy-code-btn">复制代码</span></code></pre>
<p>构造函数与普通函数区别是调用方式而不是定义方式，使用new关键字就是构造函数，否则就是普通函数。new关键字改变了函数内this的指向，使其指向刚创建的对象。</p>
<p>不能返回一个空对象。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript">    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Person</span>(<span class="hljs-params">n, a, g</span>)</span>&#123;
        <span class="hljs-built_in">this</span>.name = n;
        <span class="hljs-built_in">this</span>.age = a;
        <span class="hljs-built_in">this</span>.gender = g;
        <span class="hljs-keyword">return</span> &#123;&#125;;<span class="hljs-comment">//返回空对象</span>
    &#125;
    <span class="hljs-comment">//作为构造函数使用</span>
    <span class="hljs-keyword">var</span> o = <span class="hljs-keyword">new</span> Person(<span class="hljs-string">"Lily"</span>, <span class="hljs-number">18</span>, <span class="hljs-string">"F"</span>);
    <span class="hljs-built_in">console</span>.log(o.name) <span class="hljs-comment">//undefined</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>但是可以返回基本数据问题。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript">    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Person</span>(<span class="hljs-params">n, a, g</span>)</span>&#123;
        <span class="hljs-built_in">this</span>.name = n;
        <span class="hljs-built_in">this</span>.age = a;
        <span class="hljs-built_in">this</span>.gender = g;
        <span class="hljs-keyword">return</span> <span class="hljs-number">1</span>;  <span class="hljs-comment">//返回标量</span>
    &#125;
    <span class="hljs-comment">//作为构造函数使用</span>
    <span class="hljs-keyword">var</span> o = <span class="hljs-keyword">new</span> Person(<span class="hljs-string">"Lily"</span>, <span class="hljs-number">18</span>, <span class="hljs-string">"F"</span>);
    <span class="hljs-built_in">console</span>.log(o.name) <span class="hljs-comment">//Lily</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-4">作为对象方法的this（隐式绑定）</h1>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">let</span> name = <span class="hljs-string">'全局'</span>;
<span class="hljs-keyword">var</span> obj = &#123;
    <span class="hljs-attr">name</span>: <span class="hljs-string">'小明'</span>,
    <span class="hljs-attr">getName</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.name;
    &#125;
&#125;;
<span class="hljs-comment">//作为对象方法调用</span>
<span class="hljs-built_in">console</span>.log(obj.getName());   <span class="hljs-comment">//小明</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>用显式绑定的方式去理解，以上代码可以理解为obj.getName.call(obj)。<br>
this指向最后一个调用函数的对象，而不是开始的那个对象</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> parent = &#123;
    <span class="hljs-attr">age</span>:<span class="hljs-number">30</span>,
    <span class="hljs-attr">son</span>:&#123;
        <span class="hljs-attr">age</span>:<span class="hljs-number">5</span>,
        <span class="hljs-attr">getAge</span>:<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
            <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.age); <span class="hljs-comment">//5 ,会打印出来son的年龄，而不是parent的年龄</span>
        &#125;
    &#125;
&#125;
parent.son.getAge();
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-5">对象方法作为函数调用的this(默认绑定)</h1>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-built_in">window</span>.age = <span class="hljs-number">100</span>;

<span class="hljs-keyword">var</span> obj = &#123;
    <span class="hljs-attr">age</span>: <span class="hljs-number">10</span>,
    <span class="hljs-attr">getAge</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.age;
    &#125;
&#125;;
<span class="hljs-keyword">var</span> getAge = obj.getAge;
<span class="hljs-comment">//作为普通函数调用</span>
<span class="hljs-built_in">console</span>.log(getAge());   <span class="hljs-comment">//100</span>

<span class="copy-code-btn">复制代码</span></code></pre>
<p>尽管getAge方法是obj对象的， 但是最终调用这个方法的对象是window，可以理解为getAge.call(window)</p>
<h1 data-id="heading-6">对象原型链上的this</h1>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Foo</span>(<span class="hljs-params"></span>)</span>&#123;
    <span class="hljs-built_in">this</span>.x = <span class="hljs-number">10</span>;
&#125;
Foo.prototype.getX = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>);        <span class="hljs-comment">//Foo &#123;x: 10, getX: function&#125;</span>
    <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.x);      <span class="hljs-comment">//10</span>
&#125;
<span class="hljs-keyword">var</span> foo = <span class="hljs-keyword">new</span> Foo();
foo.getX();
<span class="copy-code-btn">复制代码</span></code></pre>
<p>在 Foo.prototype.getX 函数中，this 指向的 foo 对象。不仅仅如此，即便是在整个原型链中，this 代表的也是当前对象的值。</p>
<h1 data-id="heading-7">Es6 箭头函数中的 this</h1>
<p>箭头函数不仅仅是匿名函数的简写，更大的好处是解决了匿名函数的this指向问题，有利于封装回调函数。
箭头函数体内的this对象，就是定义该函数时所在的作用域指向的对象，而不是使用时所在的作用域指向的对象。
如何去理解定义函数所在作用域指向的对象，看了以下代码就会明白：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> name = <span class="hljs-string">'window'</span>; 

<span class="hljs-keyword">var</span> A = &#123;
   <span class="hljs-attr">name</span>: <span class="hljs-string">'A'</span>,
   <span class="hljs-attr">sayHello</span>: <span class="hljs-function">() =></span> &#123;
      <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.name)
   &#125;
&#125;

A.sayHello();<span class="hljs-comment">// 这里不是输出A，而是输出window</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>作用域是指函数内部，这里的箭头函数，也就是sayHello，所在的作用域其实是最外层的js环境，因为没有其他函数包裹；然后最外层的js环境指向的对象是winodw对象，所以这里的this指向的是window对象。<br>
如果要想this指向对象A,那么就要在箭头函数外面再包一层函数</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> name = <span class="hljs-string">'window'</span>; 

<span class="hljs-keyword">var</span> A = &#123;
   <span class="hljs-attr">name</span>: <span class="hljs-string">'A'</span>,
   <span class="hljs-attr">sayHello</span>: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
      <span class="hljs-keyword">var</span> s = <span class="hljs-function">() =></span> <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.name)
      <span class="hljs-keyword">return</span> s<span class="hljs-comment">//返回箭头函数s</span>
   &#125;
&#125;

<span class="hljs-keyword">var</span> sayHello = A.sayHello();
sayHello();<span class="hljs-comment">// 输出A </span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>具体逻辑是因为sayHello是一个函数所以箭头函数s作用域是sayHello,而sayHello指向的对象是A， 所以箭头函数的this指向对象A。</p>
<p>由于JavaScript函数对this绑定的错误处理，下面的代码无法得到预期结果，fn函数中的this会指向指向window或undefined,需要使用var that = this的hack方法修正。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> obj = &#123;
    <span class="hljs-attr">birth</span>: <span class="hljs-number">1990</span>,
    <span class="hljs-attr">getAge</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-keyword">var</span> b = <span class="hljs-built_in">this</span>.birth; <span class="hljs-comment">// 1990</span>
        <span class="hljs-keyword">var</span> fn = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
            <span class="hljs-keyword">return</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Date</span>().getFullYear() - <span class="hljs-built_in">this</span>.birth; <span class="hljs-comment">// this指向window或undefined</span>
        &#125;;
        <span class="hljs-keyword">return</span> fn();
    &#125;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>但是箭头函数完全修复了this的指向，this总是指向词法作用域，也就是外层调用者obj：</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> obj = &#123;
    <span class="hljs-attr">birth</span>: <span class="hljs-number">1990</span>,
    <span class="hljs-attr">getAge</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-keyword">var</span> b = <span class="hljs-built_in">this</span>.birth; <span class="hljs-comment">// 1990</span>
        <span class="hljs-keyword">var</span> fn = <span class="hljs-function">() =></span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Date</span>().getFullYear() - <span class="hljs-built_in">this</span>.birth; <span class="hljs-comment">// this指向obj对象</span>
        <span class="hljs-keyword">return</span> fn();
    &#125;
&#125;;
obj.getAge(); <span class="hljs-comment">// 25</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>因为this在箭头函数中已经按照词法作用域绑定了,箭头函数中的this可不改变，仅仅与其定义的位置有关,所以，用call()或者apply()调用箭头函数时，无法对this进行绑定，即传入的第一个参数被忽略。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> obj = &#123;
    <span class="hljs-attr">birth</span>: <span class="hljs-number">1990</span>,
    <span class="hljs-attr">getAge</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">year</span>) </span>&#123;
        <span class="hljs-keyword">var</span> b = <span class="hljs-built_in">this</span>.birth; <span class="hljs-comment">// 1990</span>
        <span class="hljs-keyword">var</span> fn = <span class="hljs-function">(<span class="hljs-params">y</span>) =></span> y - <span class="hljs-built_in">this</span>.birth; <span class="hljs-comment">// this.birth仍是1990</span>
        <span class="hljs-keyword">return</span> fn.call(&#123;<span class="hljs-attr">birth</span>:<span class="hljs-number">2000</span>&#125;, year);<span class="hljs-comment">//call方法的第一个参数会被忽略</span>
    &#125;
&#125;;
obj.getAge(<span class="hljs-number">2015</span>); <span class="hljs-comment">// 25</span>

<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-8">DOM事件绑定与this</h1>
<p>函数被用作事件处理函数时，它的this指向触发事件的元素
click me! btn1
click me! btn2</p>

<p>内联事件的this指向window</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><button id=<span class="hljs-string">'btn1'</span> onclick=<span class="hljs-string">"clickHandler()"</span>>click me! btn1</button>
<span class="xml"><span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">id</span>=<span class="hljs-string">'btn2'</span> <span class="hljs-attr">onclick</span>=<span class="hljs-string">"clickHandler()"</span>></span>click me! btn2<span class="hljs-tag"></<span class="hljs-name">button</span>></span></span>
<span class="xml"><span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">clickHandler</span>(<span class="hljs-params"></span>) </span>&#123;
<span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>, <span class="hljs-built_in">this</span>.id)
&#125;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如果要想在内联事件处理函数中的 this 也指向该元素，那么我们可以用 bind 函数指定其 this 值。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><button id=<span class="hljs-string">'btn1'</span> onclick=<span class="hljs-string">"clickHandler.bind(this)()"</span>>click me! btn1</button>
<span class="xml"><span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">id</span>=<span class="hljs-string">'btn1'</span> <span class="hljs-attr">onclick</span>=<span class="hljs-string">"clickHandler.call(this)"</span>></span>click me! btn1<span class="hljs-tag"></<span class="hljs-name">button</span>></span></span>
<span class="xml"><span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">id</span>=<span class="hljs-string">'btn1'</span> <span class="hljs-attr">onclick</span>=<span class="hljs-string">"clickHandler.apply(this)"</span>></span>click me! btn1<span class="hljs-tag"></<span class="hljs-name">button</span>></span></span>

<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-9">window定时器与this</h1>
<p>由于setTimeout()调用的代码运行在与所在函数完全分离的执行环境上。这会导致这些代码中包含的 this 关键字会指向 window (或全局)对象。</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> num = <span class="hljs-number">0</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Obj</span> (<span class="hljs-params"></span>)</span>&#123;
    <span class="hljs-built_in">this</span>.num = <span class="hljs-number">1</span>,
    <span class="hljs-built_in">this</span>.getNum = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.num);
    &#125;,
    <span class="hljs-built_in">this</span>.getNumLater = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.num);
        &#125;, <span class="hljs-number">1000</span>)
    &#125;
&#125;
<span class="hljs-keyword">var</span> obj = <span class="hljs-keyword">new</span> Obj; 
obj.getNum();<span class="hljs-comment">//1　　打印的为obj.num，值为1</span>
obj.getNumLater()<span class="hljs-comment">//0　　期望打印出来obj的num，然后却打印出来window的num，this指向了window</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如果要想定时器里面的this指向Obj，</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> num = <span class="hljs-number">0</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Obj</span> (<span class="hljs-params"></span>)</span>&#123;
    <span class="hljs-built_in">this</span>.num = <span class="hljs-number">1</span>,
    <span class="hljs-built_in">this</span>.getNum = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.num);
    &#125;,
    <span class="hljs-built_in">this</span>.getNumLater = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.num);
        &#125;.bind(<span class="hljs-built_in">this</span>), <span class="hljs-number">1000</span>)<span class="hljs-comment">//利用bind()将this绑定到这个函数上</span>
    &#125;
&#125;
<span class="hljs-keyword">var</span> obj = <span class="hljs-keyword">new</span> Obj; 
obj.getNum();<span class="hljs-comment">//1　　打印的为obj.num，值为1</span>
obj.getNumLater()<span class="hljs-comment">//1　　打印的为obj.num，值为1</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>或者使用箭头函数纠正this的指向</p>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-keyword">var</span> num = <span class="hljs-number">0</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Obj</span> (<span class="hljs-params"></span>)</span>&#123;
    <span class="hljs-built_in">this</span>.num = <span class="hljs-number">1</span>,
    <span class="hljs-built_in">this</span>.getNum = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.num);
    &#125;,
    <span class="hljs-built_in">this</span>.getNumLater = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>&#123;
            <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =></span> &#123;<span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.num);&#125;, <span class="hljs-number">1000</span>)
    &#125;
&#125;
<span class="hljs-keyword">var</span> obj = <span class="hljs-keyword">new</span> Obj; 
obj.getNum();<span class="hljs-comment">//1　　打印的为obj.num，值为1</span>
obj.getNumLater()<span class="hljs-comment">//0　　打印的为window.num，值为0</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-10">with和this</h1>
<p>with 语句 为一个或一组语句指定默认对象，使用 with 语句时，代码变得更短且更易读,<strong>如果在 with 语句块中使用 this，它就代表 with 所指定的对象。</strong>，但是因为with会降低代码的效率，所以在实际开发中不推荐使用，所以不详细讨论。</p>
<h1 data-id="heading-11">严格模式下的this</h1>
<p>严格模式并没有让this变复杂， 严格模式影响的只是context的默认值，仅此而已。</p>
<h1 data-id="heading-12">[]与this，迷惑的[]</h1>
<pre><code class="hljs language-javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">fn</span> (<span class="hljs-params"></span>)</span>&#123; <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>) &#125;
<span class="hljs-keyword">var</span> arr = [fn, fn2]
arr[<span class="hljs-number">0</span>]() 
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这段代码很容易把arr<a href="https://link.juejin.cn/?target=" target="_blank" title ref="nofollow noopener noreferrer">0</a> 理解成fn()，从而让人误解执行的过程是fn.call(window),从而让人理解this指向window,然后实际上的执行过程是arr<a href="https://link.juejin.cn/?target=" target="_blank" title ref="nofollow noopener noreferrer">0</a>  =>  arr.fn()  =>  this指向arr。</p>
<p>总结,this的指向一定是一个对象，永远指向函数运行时所在的对象，而不是函数被创建时所在的对象,而且这个对象是最后调用函数的那个对象,但是箭头函数和bind绑定过的函数除外:<br>
1 . 函数是否在 new 中调用 (new 绑定)，如果是，那么 this 绑定的是新创建的对象。<br>
2 . 函数是否通过 call,apply 调用，或者使用了 bind(即硬绑定)，如果是，那么 this 绑定的就是指定的对象。<br>
3 . 函数是否在某个上下文对象中调用 (隐式绑定)，如果是的话，this 绑定的是那个上下文对象。一般是 obj.foo()。<br>
4 . 如果以上都不是，那么使用默认绑定。如果在严格模式下，则绑定到 undefined，否则绑定到全局对象。<br>
5 . 如果把 Null 或者 undefined 作为 this 的绑定对象传入 call、apply 或者 bind，这些值在调用时会被忽略，实际应用的是默认绑定规则。<br>
6 . 如果是箭头函数，箭头函数的 this 继承的是外层代码块的 this。</p>
<h1 data-id="heading-13">参考文章</h1>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.jianshu.com%2Fp%2F31aec3ab1bb0" target="_blank" rel="nofollow noopener noreferrer" title="https://www.jianshu.com/p/31aec3ab1bb0" ref="nofollow noopener noreferrer">JavaScript this详解</a>
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.liaoxuefeng.com%2Fwiki%2F1022910821149312%2F1031549578462080" target="_blank" rel="nofollow noopener noreferrer" title="https://www.liaoxuefeng.com/wiki/1022910821149312/1031549578462080" ref="nofollow noopener noreferrer">箭头函数</a>
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000016286558" target="_blank" rel="nofollow noopener noreferrer" title="https://segmentfault.com/a/1190000016286558" ref="nofollow noopener noreferrer">Javascript this详解</a>
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F25294187" target="_blank" rel="nofollow noopener noreferrer" title="https://zhuanlan.zhihu.com/p/25294187" ref="nofollow noopener noreferrer">全面解析 Javascript - this</a></p></div>  
</div>
            