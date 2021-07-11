
---
title: 'js手写系列（1）_  Vue3.x响应式原理'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ac61cdc2111478d9c40567fd3867005~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 00:58:54 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ac61cdc2111478d9c40567fd3867005~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>这是我参与新手入门的第三篇文章</p>
<h2 data-id="heading-0">知识点</h2>
<br>
本篇文章主教你一步一步的手写Vue3.x的响应式原理，文中涉及的知识点如下：
<br>
<ul>
<li>defineProperty 和  Proxy 数据代理</li>
<li>ES6 之 WeakMap</li>
<li>设计模式 | 发布-订阅</li>
</ul>
<h2 data-id="heading-1">一 、defineProperty 和  Proxy 数据代理</h2>
<p><strong>相同点：</strong><br>
（1）两者都能对数据进行挟持<br></p>
<p><strong>不同点</strong><br>
（1）defineProperty<strong>根据key值</strong>来进行监听，Proxy则<strong>根据整个对象</strong>进行监听<br>
（2）defineProperty在原对象上修改操作<strong>污染原对象</strong><br>
（3）Proxy 则是会返回一个新的代理对象，操作都再新对象当中，原对象并<strong>不会被污染</strong><br></p>
<h3 data-id="heading-2"><strong>1. defineProperty</strong><br></h3>
<p>一个简易的<strong>defineProperty</strong>数据挟持</p>
<pre><code class="copyable">    const watch = (target, property, callback) => &#123;
  // 存储当前值
  let _value = target[property];
  
  // 使用defineProperty对数据进行监听
  Object.defineProperty(target, property, &#123;
  get() &#123;
  console.log('正在获取对象的：' + property + '属性值')
  return _value;
  &#125;,
  set(newVal) &#123;
  // 记录旧值
  const lastVal = _value;
  // 设置新值
  _value = newVal;
  // 回调返回新、旧值
  callback && callback(newVal, lastVal);
  &#125;
  &#125;);
  &#125;
  
  // 创建一个测试对象
  let test = &#123;
  count: 1
  &#125;
  
  // 执行监听
  watch(test, 'count', (newVal, lastVal) => &#123;
  console.log("test对象中count发生变化：", newVal, lastVal);
  &#125;)
  
  test.count += 1;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>控制台输出</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ac61cdc2111478d9c40567fd3867005~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-3"><strong>2. Proxy</strong></h3>
<p>一个简易的<strong>Proxy</strong>数据挟持</p>
<pre><code class="copyable">// Proxy 直接传入一个对象，返回一个新对象（代理对象）
const watch = (target, callback) => &#123;
return new Proxy(target, &#123;
get(target, key) &#123;
return target[key];
&#125;,
set(target, key, newVal) &#123;
// 获取旧值
const lastVal = target[key];
// 设置新值
target[key] = newVal;

// 回调 - 返回新、旧值
callback(newVal, lastVal);
&#125;
&#125;)
&#125;

// 创建一个测试对象
let test = &#123;
count: 1
&#125;

let newTest = watch(test, (newVal, lastVal) => &#123;
console.log("test对象中count发生变化：", newVal, lastVal);
&#125;)
// 修改新对象中的count
newTest.count += 1;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>控制台输出：</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71ff142ca1b64ca9a24a408ce24ac838~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h2 data-id="heading-4">二、ES6 WeakMap</h2>
<h3 data-id="heading-5">1.Map</h3>
<p>Map 是 ES6 新增的有序键值对集合。键值对的 key 和 value 都可以是任何类型的元素。</p>
<p>示例：</p>
<pre><code class="hljs language-JavaScript copyable" lang="JavaScript">        <span class="hljs-keyword">let</span> map = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Map</span>();

<span class="hljs-comment">// 创建测试对象</span>
<span class="hljs-keyword">let</span> test_1 = &#123;
<span class="hljs-attr">func</span>: <span class="hljs-function">() =></span> &#123;
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'对象的方法'</span>)
&#125;
&#125;;

<span class="hljs-comment">// 创建测试字符串变量</span>
<span class="hljs-keyword">let</span> test_2 = <span class="hljs-string">'test_2'</span>;

<span class="hljs-comment">// 设置 key - value</span>
map.set(test_1, <span class="hljs-number">1</span>);
map.set(test_2, <span class="hljs-number">2</span>);

<span class="hljs-comment">// 以对象为key来访问数据</span>
<span class="hljs-keyword">let</span> value_1 = map.get(test_1); <span class="hljs-comment">// -> value_1 = 1</span>
<span class="hljs-keyword">let</span> value_2 = map.get(test_2); <span class="hljs-comment">// -> value_2 = 2</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-6">2. WeakMap</h3>
<p>WeakMap 相对于普通的 Map，也是键值对集合，只不过 WeakMap 的 key 只能是非空对象（non-null object）。WeakMap 对它的 key 仅保持弱引用，也就是说它不阻止垃圾回收器回收它所引用的 key。WeakMap 最大的好处是可以避免内存泄漏。一个仅被 WeakMap 作为 key 而引用的对象，会被垃圾回收器回收掉。</p>
<p>示例：</p>
<pre><code class="hljs language-JavaScript copyable" lang="JavaScript">        <span class="hljs-keyword">let</span> map = <span class="hljs-keyword">new</span> <span class="hljs-built_in">WeakMap</span>();

<span class="hljs-comment">// 创建测试对象</span>
<span class="hljs-keyword">let</span> test_1 = &#123;
<span class="hljs-attr">func</span>: <span class="hljs-function">() =></span> &#123;
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'对象的方法'</span>)
&#125;
&#125;;

<span class="hljs-comment">// 创建测试字符串变量, 报异常</span>
<span class="hljs-comment">// let test_2 = 'tt'; // error -> Invalid value used as weak map keyat WeakMap.set</span>
<span class="hljs-comment">// let test_2 = null;// error -> Invalid value used as weak map keyat WeakMap.set</span>


<span class="hljs-keyword">let</span> test_2 = &#123;&#125;;

<span class="hljs-comment">// 设置 key - value</span>
map.set(test_1, <span class="hljs-number">1</span>);
map.set(test_2, <span class="hljs-number">2</span>);

<span class="hljs-comment">// 以对象为key来访问数据</span>
<span class="hljs-keyword">let</span> value_1 = map.get(test_1); <span class="hljs-comment">// -> value_1 = 1</span>
<span class="hljs-keyword">let</span> value_2 = map.get(test_2); <span class="hljs-comment">// -> value_2 = 2</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-7">三、设计模式 | 发布-订阅</h2>
<p>参考本人写的小菜文： <a href="https://juejin.cn/post/6982558686015127589" target="_blank" title="https://juejin.cn/post/6982558686015127589">设计模式 | “观察者”与“订阅发布”</a></p>
<h2 data-id="heading-8">四、手写实现Vue3.x响应式</h2>
<pre><code class="copyable"> let activeEffect;
// 订阅
class Dep &#123;
constructor(arg) &#123;
this.subscribers = new Set();
&#125;

depend() &#123;
// 添加订阅者
if (activeEffect) &#123;
this.subscribers.add(activeEffect);
&#125;
&#125;

notify(...args) &#123;
// 通知
this.subscribers.forEach(effect => effect(...args))
&#125;
&#125;

// 设置当前订阅者
function watchEffect(effect) &#123;
activeEffect = effect;
effect();
activeEffect = null;
&#125;

// 存储所有订阅实例
let depMap = new WeakMap();
// 获取当前对象的dep订阅，不存在则新建
function getDep(target) &#123;
if (!depMap.get(target)) &#123;
depMap.set(target, new Dep());
&#125;
return depMap.get(target);
&#125;

// 响应
function reactive(obj) &#123;
return new Proxy(obj, reactiveHandler);
&#125;

const reactiveHandler = &#123;
get(target, key, reactive) &#123;
let dep = getDep(target);
dep.depend();
// 使用Reflect 的原因
// Reflect 跟 Proxy 一样，只不过Reflect 不会报异常，一旦产生错误，则会返回false
return Reflect.get(target, key, reactive);
&#125;,
set(target, key, value, reactive) &#123;
Reflect.set(target, key, value, reactive);

let dep = getDep(target);
dep.notify();
&#125;
&#125;

const op = reactive(&#123;
op: 1,
test: 2
&#125;)

watchEffect(() => &#123;
console.log(op.test, 'op.test');
&#125;)

op.test = 5;
// -> 2 'op.test'
// -> 5 'op.test'

<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            