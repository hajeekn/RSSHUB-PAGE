
---
title: 'vue2.x VS vue3.x的自定义指令实现简单的v-model指令'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4cb4166fcc94d8e909876d6d402dd8d~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 19:06:40 GMT
thumbnail: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4cb4166fcc94d8e909876d6d402dd8d~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>这是我参与新手入门的第3篇文章</p>
<blockquote>
<p>这个篇是新手入门最后一次做的作业了，虽然是最后的作业，但不是最后的一篇博客。十分感谢推荐官，帮我把前两篇都推荐到了首页，嘿嘿。</p>
</blockquote>
<h1 data-id="heading-0">什么是指定义指令</h1>
<p>因为vue有了常用的内置指令(v-model、v-bind和v-on等)，但是在项目需求你会有多个地方使用到同一个功能，例如：项目需求输入一个月的天数，我们知道1-31所以需要限制最大最小还不能有小数点，当然有些需求是要小数点后保留几位如金额等等(想不到了，你懂得！)。这些功能你也是可以使用方法实现的，但是使用到了自定义指令会让你的代码看上去更加的简洁易懂。</p>
<h1 data-id="heading-1">正文</h1>
<h2 data-id="heading-2">vue2.x</h2>
<p>这里我们先了解下自定义指定的生命周期：</p>
<ul>
<li><code>bind</code>：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。</li>
<li><code>inserted</code>：被绑定元素插入父节点时调用。</li>
<li><code>update</code>：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新。</li>
<li><code>componentUpdated</code>：指令所在组件的 VNode 及其子 VNode 全部更新后调用。</li>
<li><code>unbind</code>：只调用一次，指令与元素解绑时调用。</li>
</ul>
<p>这里是复制官网的显的专业些。下面我自己的理解：<br>
bind相当就是vue的created，inserted感觉像mounted，它两的区别在于bind在inserted之前当组件渲染dom树触发父节点是null，inserted有父节点。然后就是update和componentUpdated的区别，update是组件新前，componentUpdated是组件更新后，最后在是unbind就是结束嘛（到了vue3.x的这些生命周期更加的好理解了）。</p>
<p><code>总结</code>：bind >> inserted >> update >> componentUpdated >> unbind (小菜鸡的我只用inserted)</p>
<p>下面说他们都用如下的参数:</p>
<ul>
<li><code>el</code>：指令所绑定的元素，可以用来直接操作 DOM。</li>
<li><code>binding</code>：一个对象，包含以下 property：</li>
</ul>
<p>name：指令名，不包括 v- 前缀。<br>
value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。<br>
oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。<br>
expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。<br>
arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。<br>
modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 &#123; foo: true, bar: true &#125;。</p>
<ul>
<li><code>vnode</code>：Vue 编译生成的虚拟节点。移步 VNode API 来了解更多详情。</li>
<li><code>oldVnode</code>：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。</li>
</ul>
<p>这里也是官网复制来的。</p>
<p><code>总结</code>：我就简单说说el就是你把指令写在那个标签元素上了，binding这个就是你需要绑定值啥啥等等就是上面说的。然后vnode就是vue把组件的data、method、子父组件一起打包产生一个object对象。</p>
<p>终于开始写代码了，这里是简单实现v-model的功能。</p>
<pre><code class="hljs language-js copyable" lang="js"><template>
  <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">input</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"text"</span> <span class="hljs-attr">v-myModel</span>=<span class="hljs-string">"value"</span> /></span>
    &#123;&#123; value &#125;&#125;
    <span class="hljs-tag"><<span class="hljs-name">input</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"checkbox"</span> <span class="hljs-attr">v-myModel</span>=<span class="hljs-string">"checked"</span>></span>
    &#123;&#123;checked&#125;&#125;
  <span class="hljs-tag"></<span class="hljs-name">div</span>></span>
<span class="hljs-tag"></<span class="hljs-name">template</span>></span></span>

<span class="xml"><span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> &#123;
  <span class="hljs-attr">directives</span>: &#123;
    <span class="hljs-attr">myModel</span>: &#123;
      <span class="hljs-function"><span class="hljs-title">inserted</span>(<span class="hljs-params">el, binding, vnode</span>)</span> &#123;
        <span class="hljs-keyword">if</span> ((<span class="hljs-keyword">typeof</span> binding.value) == <span class="hljs-string">'undefined'</span>) &#123;
          <span class="hljs-keyword">return</span> <span class="hljs-built_in">console</span>.error(<span class="hljs-string">'v-myModel未赋值'</span>)
        &#125;
        <span class="hljs-comment">// 这里是获取input上type属性值</span>
        <span class="hljs-keyword">const</span> type = vnode.data.attrs.type
        <span class="hljs-keyword">let</span> event = <span class="hljs-string">''</span>
        <span class="hljs-keyword">let</span> targetValue = <span class="hljs-string">''</span>
        <span class="hljs-comment">// 就是不同的类型有对应的事件和事件下获得的值</span>
        <span class="hljs-keyword">switch</span> (type) &#123;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'text'</span>:
            event = <span class="hljs-string">'input'</span>
            targetValue = <span class="hljs-string">'value'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'textarea'</span>:
            event = <span class="hljs-string">'input'</span>
            targetValue = <span class="hljs-string">'value'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'checkbox'</span>:
            event = <span class="hljs-string">'change'</span>
            targetValue = <span class="hljs-string">'checked'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'radio'</span>:
            event = <span class="hljs-string">'change'</span>
            targetValue = <span class="hljs-string">'checked'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'select'</span>:
            event = <span class="hljs-string">'change'</span>
            targetValue = <span class="hljs-string">'value'</span>
            <span class="hljs-keyword">break</span>;

        &#125;
        <span class="hljs-comment">// binding.value就是给v-myModel的值,这里为1和false给页面渲染使用</span>
        el.value = binding.value
        <span class="hljs-comment">// 这里的监听就是给组件上的data赋值</span>
        el.addEventListener(event, <span class="hljs-function">(<span class="hljs-params">e</span>) =></span> &#123;
          vnode.context[binding.expression] = e.target[targetValue]
        &#125;)
      &#125;,
    &#125;
  &#125;,
  <span class="hljs-function"><span class="hljs-title">data</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">return</span> &#123;
      <span class="hljs-attr">value</span>: <span class="hljs-string">'1'</span>,
      <span class="hljs-attr">checked</span>: <span class="hljs-literal">false</span>
    &#125;
  &#125;
&#125;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span></span>

<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4cb4166fcc94d8e909876d6d402dd8d~tplv-k3u1fbpfcp-watermark.image" alt="v-myModel.gif" loading="lazy" referrerpolicy="no-referrer"></p>
<p>这里我是使用了组件下面的directives选项，当然也是可以使用全局组成使用Vue.directive('指令名', 对象/函数)函数与对象的区别？自己去查哈哈。</p>
<h2 data-id="heading-3">vue3.x</h2>
<p>先来波自定义指令的生命周期：</p>
<ul>
<li><code>created</code> - 新的！在元素的 attribute 或事件侦听器应用之前调用。</li>
<li><code>bind</code> → beforeMount</li>
<li><code>inserted</code> → mounted</li>
<li><code>beforeUpdate</code>：新的！这是在元素本身更新之前调用的，很像组件生命周期钩子。</li>
<li><code>update</code> → 移除！有太多的相似之处要更新，所以这是多余的，请改用 updated。</li>
<li><code>componentUpdated</code> → updated</li>
<li><code>beforeUnmount</code>：新的！与组件生命周期钩子类似，它将在卸载元素之前调用。</li>
<li><code>unbind</code> -> unmounted</li>
</ul>
<p>每个生命周期还是vue2.x的那4个参数。</p>
<p>直接上代码：</p>
<pre><code class="hljs language-js copyable" lang="js"><template>
  <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
    vue3.x
    <span class="hljs-tag"><<span class="hljs-name">input</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"text"</span> <span class="hljs-attr">v-myModel:value</span>=<span class="hljs-string">"value"</span> /></span>
    &#123;&#123; value &#125;&#125;
    <span class="hljs-tag"><<span class="hljs-name">input</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"checkbox"</span> <span class="hljs-attr">v-myModel:checked</span>=<span class="hljs-string">"checked"</span> /></span>
    &#123;&#123; checked &#125;&#125;
  <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
</template>

<span class="xml"><span class="hljs-tag"><<span class="hljs-name">script</span> <span class="hljs-attr">lang</span>=<span class="hljs-string">'ts'</span>></span><span class="javascript">
<span class="hljs-keyword">import</span> &#123; ref &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'vue'</span>
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> &#123;
  <span class="hljs-attr">directives</span>: &#123;
    <span class="hljs-attr">myModel</span>: &#123;
      <span class="hljs-function"><span class="hljs-title">mounted</span>(<span class="hljs-params">el, binding, vnode</span>)</span> &#123;
        <span class="hljs-keyword">if</span> ((<span class="hljs-keyword">typeof</span> binding.value) == <span class="hljs-string">'undefined'</span>) &#123;
          <span class="hljs-keyword">return</span> <span class="hljs-built_in">console</span>.error(<span class="hljs-string">'v-myModel未赋值'</span>)
        &#125;
        <span class="hljs-comment">// 获得组件的实例对象</span>
        <span class="hljs-keyword">let</span> vm = binding.instance
        <span class="hljs-comment">// 这里是获取input上type属性值</span>
        <span class="hljs-keyword">const</span> type = vnode.props.type
        <span class="hljs-keyword">let</span> event = <span class="hljs-string">''</span>
        <span class="hljs-keyword">let</span> targetValue = <span class="hljs-string">''</span>
        <span class="hljs-keyword">switch</span> (type) &#123;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'text'</span>:
            event = <span class="hljs-string">'input'</span>
            targetValue = <span class="hljs-string">'value'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'textarea'</span>:
            event = <span class="hljs-string">'input'</span>
            targetValue = <span class="hljs-string">'value'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'checkbox'</span>:
            event = <span class="hljs-string">'change'</span>
            targetValue = <span class="hljs-string">'checked'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'radio'</span>:
            event = <span class="hljs-string">'change'</span>
            targetValue = <span class="hljs-string">'checked'</span>
            <span class="hljs-keyword">break</span>;
          <span class="hljs-keyword">case</span> <span class="hljs-string">'select'</span>:
            event = <span class="hljs-string">'change'</span>
            targetValue = <span class="hljs-string">'value'</span>
            <span class="hljs-keyword">break</span>;
        &#125;
        el.value = binding.value
        <span class="hljs-comment">// 给元素添加监听的事件</span>
        el.addEventListener(event, <span class="hljs-function">(<span class="hljs-params">e</span>) =></span> &#123;
          <span class="hljs-comment">// binding.arg 为v-myModel:value的value、v-myModel:checked的checked,为了修改组件实例下面的value和checked。</span>
          vm[binding.arg] = e.target[targetValue]
        &#125;)
      &#125;
    &#125;
  &#125;,
  <span class="hljs-function"><span class="hljs-title">setup</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">const</span> value = ref(<span class="hljs-string">'11'</span>)
    <span class="hljs-keyword">const</span> checked = ref(<span class="hljs-literal">false</span>)
    <span class="hljs-keyword">return</span> &#123;
      value,
      checked
    &#125;
  &#125;,
&#125;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3aa90489404a42868f30ae30bc459a0c~tplv-k3u1fbpfcp-watermark.image" alt="v-myModelv3.gif" loading="lazy" referrerpolicy="no-referrer"></p>
<p>其实这里有一个问题如v-myModel:value="value"如果不传:value在vm中是不知道修改哪个值，在vue官方介绍这个:value是有其他作用的,我查找了许多，未找到解决方法，如果有大佬知道求指教。</p>
<h1 data-id="heading-4">总结</h1>
<ul>
<li>vue2.x自定义指令生命周期 <code>bind</code> >> <code>inserted</code> >> <code>update</code> >> <code>componentUpdated</code> >> <code>unbind</code></li>
<li>vue3.x自定义指令生命周期 <code>created</code> >> <code>beforeMount</code> >> <code>mounted</code> >> <code>beforeUpdate</code> >> <code>updated</code> >> <code>beforeUnmount</code> >> <code>unmounted</code></li>
<li>都拥有的参数：<code>el</code>、<code>binding</code>、<code>vnode</code>、<code>oldVnode</code>。常用的为前三个。</li>
</ul></div>  
</div>
            