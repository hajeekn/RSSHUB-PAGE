
---
title: 'JavaScript中的继承'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/12505bcbc5804daea2280ec0d64051ac~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 15 Jul 2021 04:57:43 GMT
thumbnail: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/12505bcbc5804daea2280ec0d64051ac~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;position:relative;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#282d36&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px;color:#2f845e&#125;.markdown-body h2&#123;font-size:24px;display:inline-block;font-weight:700;background:#2f845e;color:#fff;padding:6px 8px 0 0;border-top-right-radius:6px;margin-right:2px;box-shadow:6px 3px 0 0 rgba(47,132,194,.2)&#125;.markdown-body h2:before&#123;content:" ";display:inline-block;width:8px&#125;.markdown-body h2:after&#123;content:" ";position:absolute;display:block;width:calc(100% - 40px);border-bottom:3px solid #2f845e&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%;box-shadow:6px 6px 6px #888&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75;border-top:6px solid #2f845e&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#262626;background:linear-gradient(180deg,rgba(66,185,131,.1),transparent)!important&#125;.markdown-body strong&#123;background-color:inherit;color:#2f845e&#125;.markdown-body em&#123;background-color:inherit;color:#949415&#125;.markdown-body a&#123;text-decoration:none;color:#2f8e54;border-bottom:1px solid #3f9e64&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#3f9e64&#125;.markdown-body a[class^=footnote]&#123;margin-left:4px&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:100%;max-width:100%;overflow:auto;border:2px solid #2f8e54&#125;.markdown-body thead&#123;background:#2f8e54;color:#fff;text-align:left;font-weight:700&#125;.markdown-body tr:nth-child(2n)&#123;background-color:rgba(153,255,188,.1)&#125;.markdown-body td,.markdown-body th&#123;width:100%;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;padding:1px 22px;margin:22px 0;border-left:6px solid #2f845e;background-color:rgba(66,185,131,.1);border-radius:4px&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body del&#123;color:#2f845e&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">JavaScript中的继承</h1>
<h2 data-id="heading-1">1.原型链</h2>
<p>ECMA-262 把原型链定义为 ECMAScript 的主要继承方式。其基本思想就是通过原型继承多个引用类型的属性和方法。重温一下构造函数、原型和实例的关系：每个构造函数都有一个原型对象，原型有一个属性指回构造函数，而实例有一个内部指针指向原型。如果原型是另一个类型的实例那就意味着这个原型本身有一个内部指针指向另一个原型，相应地另一个原型也有一个指针指向另一个构造函数。这样就在实例和原型之间构造了一条原型链。这就是原型链的基本构想。实现原型链涉及如下代码模式：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SuperType</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-built_in">this</span>.property = <span class="hljs-literal">true</span>; 
&#125; 
SuperType.prototype.getSuperValue = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.property; 
&#125;; 
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SubType</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-built_in">this</span>.subproperty = <span class="hljs-literal">false</span>; 
&#125; 
<span class="hljs-comment">// 继承 SuperType </span>
SubType.prototype = <span class="hljs-keyword">new</span> SuperType(); 
SubType.prototype.getSubValue = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
 <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.subproperty; 
&#125;; 
<span class="hljs-keyword">let</span> instance = <span class="hljs-keyword">new</span> SubType(); 
<span class="hljs-built_in">console</span>.log(instance.getSuperValue()); <span class="hljs-comment">// true</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>由上述的代码不难看出将<strong>SubType</strong>的原型指向了<strong>SuperType</strong>的实例化对象这样SubType 的实例不仅能从SuperType 的实例中继承属性和方法，而且还与 SuperType 的原型挂上了钩。如下图所示JavaScript中的原型链关系图：</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/12505bcbc5804daea2280ec0d64051ac~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>原型链实现继承特点</strong></p>
<ul>
<li>
<ol>
<li>实例可继承的属性有: 实例的构造函数属性, 父类构造函数属性, 父类原型的属性. (新实例不会继承父类实例属性)</li>
</ol>
</li>
</ul>
<p><strong>原型链实现继承存在的问题</strong>：</p>
<ul>
<li>1.原型中包含的引用值会在所有实例间共享</li>
<li>2.子类型在实例化时不能给父类型的构造函数传参</li>
</ul>
<h2 data-id="heading-2">2.盗用构造函数</h2>
<p>在子类构造函数中调用父类构造函数。因为毕竟函数就是在特定上下文中执行代码的简单对象，所以可以使用
apply()和 call()方法以新创建的对象为上下文执行构造函数。如下列所示</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SuperType</span>(<span class="hljs-params">name</span>)</span>&#123; 
 <span class="hljs-built_in">this</span>.name = name; 
&#125; 
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SubType</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-comment">// 继承 SuperType 并传参</span>
 SuperType.call(<span class="hljs-built_in">this</span>, <span class="hljs-string">"Nicholas"</span>); 
 <span class="hljs-comment">// 实例属性</span>
 <span class="hljs-built_in">this</span>.age = <span class="hljs-number">29</span>; 
&#125; 
<span class="hljs-keyword">let</span> instance = <span class="hljs-keyword">new</span> SubType(); 
<span class="hljs-built_in">console</span>.log(instance.name); <span class="hljs-comment">// "Nicholas"; </span>
<span class="hljs-built_in">console</span>.log(instance.age); <span class="hljs-comment">// 29</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>相对于原型链继承的优点</strong></p>
<ul>
<li>1.可以在子类构造函数中向父类构造函数传参</li>
</ul>
<p><strong>构造函数实现继承的问题</strong></p>
<ul>
<li>1.使用构造函数模式自定义类型的问题：必须在构造函数中定义方法，因此函数不能重用</li>
<li>2.子类也不能访问父类原型上定义的方法，因此所有类型只能使用构造函数模式。由于存在这些问题，盗用构造函数基本上也不能单独使用。</li>
</ul>
<h2 data-id="heading-3">3.组合继承</h2>
<p>组合继承（有时候也叫伪经典继承）综合了原型链和盗用构造函数，将两者的优点集中了起来。基
本的思路是使用原型链继承原型上的属性和方法，而通过盗用构造函数继承实例属性。这样既可以把方
法定义在原型上以实现重用，又可以让每个实例都有自己的属性。如下例子所示：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SuperType</span>(<span class="hljs-params">name</span>)</span>&#123; 
 <span class="hljs-built_in">this</span>.name = name; 
 <span class="hljs-built_in">this</span>.colors = [<span class="hljs-string">"red"</span>, <span class="hljs-string">"blue"</span>, <span class="hljs-string">"green"</span>]; 
&#125; 
SuperType.prototype.sayName = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.name); 
&#125;; 
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SubType</span>(<span class="hljs-params">name, age</span>)</span>&#123; 
 <span class="hljs-comment">// 继承属性</span>
 SuperType.call(<span class="hljs-built_in">this</span>, name); 
 <span class="hljs-built_in">this</span>.age = age; 
&#125; 
<span class="hljs-comment">// 继承方法</span>
SubType.prototype = <span class="hljs-keyword">new</span> SuperType(); 
SubType.prototype.sayAge = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.age); 
&#125;; 
<span class="hljs-keyword">let</span> instance1 = <span class="hljs-keyword">new</span> SubType(<span class="hljs-string">"Nicholas"</span>, <span class="hljs-number">29</span>); 
instance1.colors.push(<span class="hljs-string">"black"</span>); 
<span class="hljs-built_in">console</span>.log(instance1.colors); <span class="hljs-comment">// "red,blue,green,black" </span>
instance1.sayName(); <span class="hljs-comment">// "Nicholas"; </span>
instance1.sayAge(); <span class="hljs-comment">// 29 </span>
<span class="hljs-keyword">let</span> instance2 = <span class="hljs-keyword">new</span> SubType(<span class="hljs-string">"Greg"</span>, <span class="hljs-number">27</span>); 
<span class="hljs-built_in">console</span>.log(instance2.colors); <span class="hljs-comment">// "red,blue,green" </span>
instance2.sayName(); <span class="hljs-comment">// "Greg"; </span>
instance2.sayAge(); <span class="hljs-comment">// 27</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>组合继承的优点</strong></p>
<ul>
<li>1.结合了两种模式的优点, 传参和复用</li>
</ul>
<p><strong>组合继承的问题</strong></p>
<ul>
<li>1.调用了两次父类构造函数(耗内存), 子类的构造函数会代替原型上的那个父类构造函数。</li>
</ul>
<h2 data-id="heading-4">4.原型式继承</h2>
<p>用一个函数包装一个对象, 然后返回这个函数的调用, 这个函数就变成了个可以随意增添属性的实例或对象<strong>Object.create()</strong> 就是这个原理。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">object</span>(<span class="hljs-params">o</span>) </span>&#123; 
 <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">F</span>(<span class="hljs-params"></span>) </span>&#123;&#125; 
 F.prototype = o; 
 <span class="hljs-keyword">return</span> <span class="hljs-keyword">new</span> F(); 
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这个 object()函数会创建一个临时构造函数，将传入的对象赋值给这个构造函数的原型，然后返回这个临时类型的一个实例。本质上，object()是对传入的对象执行了一次浅复制。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">let</span> person = &#123; 
 <span class="hljs-attr">name</span>: <span class="hljs-string">"Nicholas"</span>, 
 <span class="hljs-attr">friends</span>: [<span class="hljs-string">"Shelby"</span>, <span class="hljs-string">"Court"</span>, <span class="hljs-string">"Van"</span>] 
&#125;; 
<span class="hljs-keyword">let</span> anotherPerson = object(person); 
anotherPerson.name = <span class="hljs-string">"Greg"</span>; 
anotherPerson.friends.push(<span class="hljs-string">"Rob"</span>); 
<span class="hljs-keyword">let</span> yetAnotherPerson = object(person); 
yetAnotherPerson.name = <span class="hljs-string">"Linda"</span>; 
yetAnotherPerson.friends.push(<span class="hljs-string">"Barbie"</span>); 
<span class="hljs-built_in">console</span>.log(person.friends); <span class="hljs-comment">// "Shelby,Court,Van,Rob,Barbie"</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>原型式继承的优点</strong></p>
<ul>
<li>原型式继承非常适合不需要单独创建构造函数，但仍然需要在对象间共享信息的场合。</li>
</ul>
<p><strong>原型式继承的不足</strong></p>
<ul>
<li>属性中包含的引用值始终会在相关对象间共享，跟使用原型模式是一样的。</li>
</ul>
<h2 data-id="heading-5">5.寄生式继承</h2>
<p>寄生式继承背后的思路类似于寄生构造函数和工厂模式：创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象。基本的寄生继承模式如下：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">createAnother</span>(<span class="hljs-params">original</span>)</span>&#123; 
 <span class="hljs-keyword">let</span> clone = object(original); <span class="hljs-comment">// 通过调用函数创建一个新对象</span>
 clone.sayHi = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123; <span class="hljs-comment">// 以某种方式增强这个对象</span>
 <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"hi"</span>); 
 &#125;; 
 <span class="hljs-keyword">return</span> clone; <span class="hljs-comment">// 返回这个对象</span>
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>寄生式继承的优点</strong></p>
<ul>
<li>没有创建自定义类型, 因为只是套了个壳子返回对象, 这个函数顺理成章就成了创建的新对象</li>
</ul>
<p><strong>寄生式继承的不足</strong></p>
<ul>
<li>通过寄生式继承给对象添加函数会导致函数难以重用，与构造函数模式类似。</li>
</ul>
<h2 data-id="heading-6">6.寄生组合式继承</h2>
<p>组合继承其实也存在效率问题。最主要的效率问题就是父类构造函数始终会被调用两次：一次在是
创建子类原型时调用，另一次是在子类构造函数中调用。寄生式组合继承通过盗用构造函数继承属性，但使用混合式原型链继承方法。基本思路是不通过调用父类构造函数给子类原型赋值，而是取得父类原型的一个副本。说到底就是使用寄生式继承来继承父类原型，然后将返回的新对象赋值给子类原型。寄生式组合继承的基本模式如下所示：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inheritPrototype</span>(<span class="hljs-params">subType, superType</span>) </span>&#123; 
 <span class="hljs-keyword">let</span> prototype = object(superType.prototype); <span class="hljs-comment">// 创建对象</span>
 prototype.constructor = subType; <span class="hljs-comment">// 增强对象</span>
 subType.prototype = prototype; <span class="hljs-comment">// 赋值对象</span>
&#125;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SuperType</span>(<span class="hljs-params">name</span>) </span>&#123; 
 <span class="hljs-built_in">this</span>.name = name; 
 <span class="hljs-built_in">this</span>.colors = [<span class="hljs-string">"red"</span>, <span class="hljs-string">"blue"</span>, <span class="hljs-string">"green"</span>]; 
&#125; 
SuperType.prototype.sayName = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.name); 
&#125;; 
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">SubType</span>(<span class="hljs-params">name, age</span>) </span>&#123; 
 SuperType.call(<span class="hljs-built_in">this</span>, name);
  <span class="hljs-built_in">this</span>.age = age; 
&#125; 
inheritPrototype(SubType, SuperType); 
SubType.prototype.sayAge = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>&#123; 
 <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.age); 
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>寄生式继承的特点</strong></p>
<ul>
<li>这里只调用了一次 SuperType 构造函数，避免了 SubType.prototype 上不必要也用不到的属性，</li>
</ul>
<p>因此可以说这个例子的效率更高。而且，原型链仍然保持不变，因此 instanceof 操作符和
isPrototypeOf()方法正常有效。寄生式组合继承可以算是引用类型继承的最佳模式。</p></div>  
</div>
            