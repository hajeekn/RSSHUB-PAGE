
---
title: 'Vue3 新特性理解'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=3213'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 20:09:41 GMT
thumbnail: 'https://picsum.photos/400/300?random=3213'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">前言</h1>
<p>vue3 已经出来了有一段时间了，作为前端开发人员还是得紧跟时事，抓紧学习，了解新的技术，才不会被这个时代所淘汰。而且vue3 针对 vue2 来说，在性能上肯定是有所提高的，这就说明在后面的技术革新中，vue2可能会被vue3 所取代，当然也不是一时半会的事。所以现在趁热，只要学不死就往死里学吧。</p>
<p>下面就来总结一下我在学习Vue3 的过程中了解的一些特写，写下来加以理解。</p>
<h1 data-id="heading-1">Reactive</h1>
<p>作用：用来给 <strong>引用类型</strong> 做响应式处理,注意这个属性只是给<code>引用类型</code>做响应式处理，<strong>而不是给引用类型的属性做响应式处理</strong>，所以reactive 用于包裹一个对象：</p>
<pre><code class="copyable">const user = reactive(&#123;name:'zhangsan', age:18&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>然后只是<code>user</code>这个对象有响应，并不代表<code>user.name</code> 和<code>user.age</code> 有响应式。所以在<code>setup</code>中返回的时候需要返回整个对象：</p>
<pre><code class="copyable">const user = reactive(&#123;
  name: 'zhangsan',
  age: 18
&#125;)
return &#123;
  user
&#125;
// 无法直接解构 在 template 中使用
// 因为reactive 响应化的是 user ，而不是 user 中的每个属性。 如果要响应user对象里面的每个值 就得使用 toRefs
// return &#123;
//   ...user
// &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>在模板中就是这样使用的：</p>
<pre><code class="copyable"><p>reactive : &#123;&#123; user.name &#125;&#125; - &#123;&#123; user.age &#125;&#125;</p>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>另外关于对象的值的获取和设置，特别说明一下，如下注释解释：</p>
<pre><code class="copyable">// 设置值
setTimeout(() => &#123;
  // 注意：修改 reactive 的值 不需要带.value
  // 只有是 reactive 和 template 使用的时候不需要带.value
  user.age = 21
  // 获取值
  // console.log(user.age)
&#125;, 1500)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>至于原理：来自于vue3 用 <code>proxy</code> 实现，有兴趣的同学可以去了解一下。</p>
<h1 data-id="heading-2">ref</h1>
<p>上面讲述了reactive 是用来做引用类型的响应式的，那么值类型的响应式就需要<code>ref</code>，用法也很简单：</p>
<pre><code class="copyable"><template>
  <div>
    <p>ref，&#123;&#123; age &#125;&#125;</p>
  </div>
</template>

...
const age = ref<number>(10)
return &#123;
  age
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>关于ref 值的设置和获取,下面代码注释也有详细解释（这个时候就需要用到<code>.value</code>）：</p>
<pre><code class="copyable">setTimeout(() => &#123;
  // 这里修改 相当于对引用类型的值的进行修改，修改后 能响应到到原来的对象
  // 类似：
  // const a = &#123; age:11 &#125;
  // const b = a
  // b.age = 12
  // console.log(a.age)  // 12

  // 注意： 修改 ref 的值 需要带 value
  age.value = 13
&#125;, 1500)

// 这样直接修改 age 是无法做到响应
// let age = 10
// setTimeout(() => &#123;
//   age = 15
// &#125;, 1500);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>所以ref 和 reactive 两者的使用就可以包含所有类型的响应式的处理。用于双向绑定 这也是vue 一直以来引以为傲的特性。</p>
<h1 data-id="heading-3">toRef</h1>
<p>作用是将引用类型的某个属性变成响应式，举个栗子：</p>
<pre><code class="copyable">const user = reactive(&#123; name: 'lisi', age: 16 &#125;) // 首先将对象 变成响应式
// 然后把 对象的某个属性变成响应式
const ageToRef = toRef(user, 'age') // 相当于 把这个对象 中的 age 处理成了响应式
return &#123;
  user,
  ageToRef
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这就是为什么我在介绍reactive 的时候一再强调，reactive只是正对引用类型本身做出的响应式，并不包含它本身属性的响应式。有了<code>toRef</code>的加持，现在就可以实现对象属性值的响应式了。</p>
<p>关于 toRef的值的设置与获取：</p>
<pre><code class="copyable">// 修改值
setTimeout(() => &#123;
  ageToRef.value = 18
  // console.log(ageToRef.value)
&#125;, 1500)
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-4">toRefs</h1>
<p>类型与 toRef，但显而易见，<code>toRefs</code>明显是个复数，所以它的作用就是将引用类型的属性都变成响应式：</p>
<pre><code class="copyable">setup() &#123;
    const user = reactive(&#123; name: 'jojo', age: 19 &#125;) // 先将整个对象变成响应式
    const userToRefs = toRefs(user) // 再拆分该对象的每个属性 使之也成为响应式
    const &#123; name, age &#125; = userToRefs
    // 修改值
    setTimeout(() => &#123;
      age.value = 21
    &#125;, 1500)

    return &#123;
      name,
      age
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>既在模板中就可以直接使用属性了：</p>
<pre><code class="copyable"><template>
  <div>
    <p>toRefs: &#123;&#123; name &#125;&#125; - &#123;&#123; age &#125;&#125;</p>
  </div>
</template>
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-5">中途总结</h1>
<ol>
<li>
<p>为什么要使用 ref,reactive:</p>
<p>答：因为 值类型的响应式 需要 ref，引用类型的响应式 需要reactive。</p>
</li>
<li>
<p>为什么要使用 toRef ，toRefs：</p>
<p>答：因为 toRef 显示指定 对象中的值类型 需要变成 响应式，而toRefs 是隐式指定 对象 所有的属性都是响应式。</p>
</li>
<li>
<p>使用 toRefs 可以解构对象，使之返回属性单独可以在 template 中 使用。</p>
</li>
</ol>
<h1 data-id="heading-6">watch</h1>
<p>vue3 中的watch 和vue2 中的watch 在含义上是一直的，无非就是侦听数据的变化，但，vue3 分出了引用类型的响应式（reactive）和值类型的响应式（ref），vue3 中的watch 似乎变得更加不那么一样了，我们先看看用法：</p>
<pre><code class="copyable">setup() &#123;
    const wNumber = ref<number>(100)
    const user = reactive(&#123; name: 'zhangsan', age: 18 &#125;)
    // watch 监听 ref
    watch(wNumber, (newVal, oldVal) => &#123;
      console.log(newVal, oldVal)
    &#125;)

    // watch 监听 reactive
    watch(
      () => user.age,
      (newVal, oldVal) => &#123;
        console.log(newVal, oldVal)
      &#125;
    )

    return &#123;
      wNumber,
      user
    &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>从上面的代码可以看出，正对不同的响应式，在写法上稍有不同。</p>
<h1 data-id="heading-7">watchEffect</h1>
<p>让人没想到的是，vue3 除了在setup 中引用了watch 之外，还引用了<code>watchEffect</code>这个api，其含义无非也是监听的意思。那这有什么不一样呢？</p>
<pre><code class="copyable">setup() &#123;
    const wNumber = ref<number>(100)
    const user = reactive(&#123; name: 'zhangsan', age: 18 &#125;)

    // watchEffect 初始化执行一次 监听回调函数内部所有使用的变量
    watchEffect(() => &#123;
      // 这里自动监听到 wNumber
      console.log(`----$&#123;wNumber.value&#125;-----`)
    &#125;)
    watchEffect(() => &#123;
      // 这里自动监听到 user.name 、user.age
      console.log(`----$&#123;user.name&#125;--$&#123;user.age&#125;---`)
    &#125;)
    
    setTimeout(() => &#123;
      wNumber.value = 200
    &#125;, 1500)

    setTimeout(() => &#123;
      user.age = 20
    &#125;, 2000)

    return &#123;
      wNumber,
      user
    &#125;
 &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如注释写的的样，watchEffect不需要手动监听，而是在setup 初始化的时候，就<strong>提前</strong>执行了一次，而这提前执行了一次之后，watchEffect 就知道了该回调函数内 那些值是需要被侦听的。所以当我们触发修改的时候就自动监听到改变了。虽然不知道什么时候回用到这个属性，但也不得不说，vue3的团队想的也算是很周到了。</p>
<h1 data-id="heading-8">其他特性</h1>
<h2 data-id="heading-9">Proxy</h2>
<p>Proxy 响应式替代了vue2 中的Object.defineProperty，在set新值和delete 值的时候得到了解决，优化了Object.defineProperty中一次性递归监听的问题。Proxy则是根据值的深度来递归，例如：一个对象有5层，获取第三层某个属性的值，则proxy只会递归到第三层的属性。</p>
<h2 data-id="heading-10">PatchFlag</h2>
<p>给动态节点加上标记，动态节点类似于：<span>&#123;&#123; msg &#125;&#125;</span>，编译解析过程中会给动态节点添加标记。这样做有利于diff 算法在对比dom树的时候，省去对比静态节点，直接对比有标记的动态节点。</p>
<h2 data-id="heading-11">hoistStatic</h2>
<p>编译过程中，使静态节点的变量提升到父作用域，使之缓存。其次多个静态节点在一起超过一定数量 会合并成dom 字符串直接解析。</p>
<h2 data-id="heading-12">cacheHandler</h2>
<p>缓存事件，有事件缓存就取，没事件缓存就重新定义。</p>
<h2 data-id="heading-13">SSR优化</h2>
<p>类似hoistStatic 将多个静态节点合并成dom字符串进行优化便于直接解析成真实的dom树。</p>
<h2 data-id="heading-14">tree-sharking</h2>
<p>在编译过程中，对于用到的api 才会导入相应的编译模块。类似于按需加载</p>
<h1 data-id="heading-15">最后</h1>
<p>vue3 无论在性能还是在规范上 对比vue2 还是有了很大的改进，高级特性<code>Composition Api</code> 也是vue 3的亮点。笔者做vue3的理解也只是在使用层面上，后续继续加油挖掘和学习vue3更多的特性。随着技术的迭代更新，vue3 也是大势所趋，加油学习！</p></div>  
</div>
            