
---
title: '入门 React Hooks 实战解析'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=1875'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 17:32:45 GMT
thumbnail: 'https://picsum.photos/400/300?random=1875'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>最近在学习React，并使用 React + TypeScript 实现了一个记账应用。在本文中会总结一些 React Hooks 入门的技巧。</p>
<h2 data-id="heading-0">useState</h2>
<p><code>useState</code> 可以返回两个数据，第一个数据为初始变量，第二个数据为修改变量的方法。然后再传入一个初始值，即可完成一个 <code>useState</code>。</p>
<p>比如我定义一个变量 <code>tags</code>，同时也需要定义一个 <code>setTags</code> ，方便后续对 <code>tags</code> 进行修改。这里的初始值是 <code>[]</code>，一个空数组。<code>useState</code> 结合TS语法，需要在后面加上 <code><></code> 声明数据类型，即以下代码中的 <code>&#123; id: number, name: string &#125;[]</code>。</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> [tags, setTags] = useState<&#123; <span class="hljs-attr">id</span>: <span class="hljs-built_in">number</span>, <span class="hljs-attr">name</span>: <span class="hljs-built_in">string</span> &#125;[]>([]);

<span class="hljs-comment">//把 tags 和 setTags 暴露出去</span>
<span class="hljs-keyword">return</span> &#123;tags, setTags&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>我们还可以使用 <code>return</code> 析构语法把 <code>tags</code> 和 <code>setTags</code> 暴露到外部，方便其他组件使用。项目中，需要写一个根据标签ID来确定标签的功能，就使用到了 <code>useState</code> 中的 <code>tags</code>。</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> findTag = <span class="hljs-function">(<span class="hljs-params">id: <span class="hljs-built_in">number</span></span>) =></span> tags.filter(<span class="hljs-function"><span class="hljs-params">tag</span> =></span> tag.id === id)[<span class="hljs-number">0</span>];
<span class="copy-code-btn">复制代码</span></code></pre>
<p>在制作“添加标签”功能时，使用到了 <code>setTags</code> 来更改 <code>tags</code> 的值：</p>
<pre><code class="hljs language-ts copyable" lang="ts">    <span class="hljs-keyword">const</span> addTag = <span class="hljs-function">() =></span> &#123;
        <span class="hljs-keyword">const</span> tagName = <span class="hljs-built_in">window</span>.prompt(<span class="hljs-string">'请输入标签名'</span>);
        <span class="hljs-keyword">if</span> (tagName !== <span class="hljs-literal">null</span> && tagName !== <span class="hljs-string">''</span>) &#123;
            setTags([...tags, &#123;<span class="hljs-attr">id</span>: createId(), <span class="hljs-attr">name</span>: tagName&#125;]);
        &#125;
    &#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>useState</code> 中的两个返回值，也可以结合到 <code>useEffect</code> 中使用：</p>
<pre><code class="hljs language-ts copyable" lang="ts">    useEffect(<span class="hljs-function">() =></span> &#123;
        <span class="hljs-keyword">let</span> localTags = <span class="hljs-built_in">JSON</span>.parse(<span class="hljs-built_in">window</span>.localStorage.getItem(<span class="hljs-string">'tags'</span>) || <span class="hljs-string">'[]'</span>);
        <span class="hljs-keyword">if</span> (localTags.length === <span class="hljs-number">0</span>) &#123;
            localTags = [
                &#123;<span class="hljs-attr">id</span>: createId(), <span class="hljs-attr">name</span>: <span class="hljs-string">'衣服'</span>&#125;,
                &#123;<span class="hljs-attr">id</span>: createId(), <span class="hljs-attr">name</span>: <span class="hljs-string">'食物'</span>&#125;,
                &#123;<span class="hljs-attr">id</span>: createId(), <span class="hljs-attr">name</span>: <span class="hljs-string">'住房'</span>&#125;,
                &#123;<span class="hljs-attr">id</span>: createId(), <span class="hljs-attr">name</span>: <span class="hljs-string">'交通'</span>&#125;
            ];
        &#125;
        setTags(localTags)
    &#125;, []);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>在这个 <code>useEffect</code> 中，依赖值留空，可以实现在进入页面后马上渲染出数据。以上代码首先在 <code>LocalStorage</code> 中对标签数据进行读取，判断标签数据是否存在，如存在则在渲染UI后使用 <code>setTags</code> 写入数据。</p>
<h2 data-id="heading-1">useReducer</h2>
<p><code>useReducer</code> 可以理解成 <code>useState</code> 的高级版。</p>
<p>使用步骤主要为以下4步：</p>
<p>第一步：创建一个初始值 <code>initialState</code></p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> initial = &#123;
  <span class="hljs-attr">n</span>: <span class="hljs-number">0</span>
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>第二步：创建对数据的所有操作，以下代码可以对数字实现 <code>+1</code> 和 <code>*2</code> 功能：</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> reducer = <span class="hljs-function">(<span class="hljs-params">state, action</span>) =></span> &#123;
  <span class="hljs-keyword">if</span> (action.type === <span class="hljs-string">"add"</span>) &#123;
    <span class="hljs-keyword">return</span> &#123; <span class="hljs-attr">n</span>: state.n + action.number &#125;;
  &#125; <span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> (action.type === <span class="hljs-string">"multi"</span>) &#123;
    <span class="hljs-keyword">return</span> &#123; <span class="hljs-attr">n</span>: state.n * <span class="hljs-number">2</span> &#125;;
  &#125; <span class="hljs-keyword">else</span> &#123;
    <span class="hljs-keyword">throw</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">"unknown type"</span>);
  &#125;
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>第三步：将创建的 <code>reducer</code> 传给 <code>useReducer</code> 得到读写API，<code>useReducer</code> 接受两个参数，一个是 <code>reducer</code>，一个是 <code>initial</code>。返回两个参数，一个是 <code>state</code> 保存值，另一个是 <code>dispatch</code>。以下代码中 <code>state</code> 的 <code>n</code> 就是上面 <code>initial</code> 的 <code>n</code>。</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> [state, dispatch] = useReducer(reducer, initial);
<span class="hljs-keyword">const</span> &#123; n &#125; = state;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>使用 <code>dispatch</code> 来调用之前写好的 <code>add</code>，数字即可+1，跟 <code>useState</code> 中的 <code>setX</code> 一样的效果。此时的 <code>onClick</code> 方法非常简单，对数据的操作都被集成到 <code>reducer</code> 中，<code>onClick</code> 只触发 <code>dispatch</code>，然后调用相应的 <code>reducer</code> 即可。</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> onClick = <span class="hljs-function">() =></span> &#123;
    dispatch(&#123; <span class="hljs-attr">type</span>: <span class="hljs-string">"add"</span>, <span class="hljs-attr">number</span>: <span class="hljs-number">1</span> &#125;);
&#125;;
<span class="hljs-keyword">const</span> onClick2 = <span class="hljs-function">() =></span> &#123;
    dispatch(&#123; <span class="hljs-attr">type</span>: <span class="hljs-string">"multi"</span>, <span class="hljs-attr">number</span>: <span class="hljs-number">2</span> &#125;);
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-2">useEffect</h2>
<p>在 React 的官方文档中，<code>useEffect</code> 可以理解成 <code>componentDidMount</code>、<code>componentDidUpdate</code>和<code>componentWiilUnmount</code> 的结合体。<code>useEffect</code> 接收一个函数，这个函数会在组件渲染之后才执行，返回的方式有两种。要么返回一个能清除副作用的函数，要么不返回任何内容。</p>
<p>一般的用法如下：</p>
<pre><code class="hljs language-ts copyable" lang="ts">useEffect(<span class="hljs-function">() =></span> &#123;
<span class="hljs-comment">// 函数</span>
&#125;, [<span class="hljs-comment">//更新依赖]);</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>useEffect</code> 接受两个参数。第一个是函数，放入异步操作的代码。第二个参数是依赖项数组，只要数组有变化，<code>useEffect</code> 就会执行。</p>
<pre><code class="hljs language-ts copyable" lang="ts"> useEffect(<span class="hljs-function">() =></span> &#123;
        <span class="hljs-keyword">if</span> (count.current > <span class="hljs-number">1</span>) &#123;
            fn();
        &#125;
    &#125;, [fn, dependency]);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>上面代码中，只要 <code>fn</code> 或 <code>dependency</code> 发生变化，<code>useEffect</code> 就会执行。组件在第一次渲染时，<code>useEffect</code> 也会执行，如果渲染后依赖项发生变化，就会执行两次。</p>
<h2 data-id="heading-3">useContext</h2>
<p>如果需要组件之间共享状态，可以使用 <code>useContext</code>。一般用于同级之间的组件通信。</p>
<p>使用 <code>useContext</code> 只需3步：</p>
<p>首先使用 <code>React.createContext()</code> 创建一个 <code>context</code>：</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> Context1 = React.createContext(<span class="hljs-literal">null</span>)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>使用 <code><Context1.Provider></code> 圈定作用域：</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">App</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-keyword">const</span> [n, setN] = useState(<span class="hljs-number">0</span>)
  <span class="hljs-keyword">return</span> (
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">Context1.Provider</span> <span class="hljs-attr">value</span>=<span class="hljs-string">&#123;&#123;n,setN&#125;&#125;</span>></span>
      <span class="hljs-tag"><<span class="hljs-name">div</span> <span class="hljs-attr">className</span>=<span class="hljs-string">"App"</span>></span>
        <span class="hljs-tag"><<span class="hljs-name">Dad</span>/></span>
      <span class="hljs-tag"></<span class="hljs-name">div</span>></span>
    <span class="hljs-tag"></<span class="hljs-name">Context1.Provider</span>></span></span>
  );
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>作用域内使用 <code>useContext(Context1)</code> 来使用上下文：</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Dad</span>(<span class="hljs-params"></span>)</span>&#123;
  <span class="hljs-keyword">return</span>(
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
      我是爸爸
      <span class="hljs-tag"><<span class="hljs-name">Child</span>/></span>
    <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
  )
&#125;

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Child</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-keyword">const</span> &#123; n, setN &#125; = useContext(C);
  <span class="hljs-keyword">const</span> onClick=<span class="hljs-function">()=></span>&#123;
    setN(<span class="hljs-function"><span class="hljs-params">i</span>=></span>i+<span class="hljs-number">1</span>)
  &#125;
  <span class="hljs-keyword">return</span>(
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>我是儿子 我得到的n: &#123;n&#125;
      <span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">onClick</span>=<span class="hljs-string">&#123;onClick&#125;</span>></span>+1<span class="hljs-tag"></<span class="hljs-name">button</span>></span>
    <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
  )
&#125;

<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-4">封装自定义 hook</h2>
<p>记账软件需要对用户输入的标签进行增、删、改、查等操作，可以把这些操作都封装到一个 <code>useTags</code> 组件中，方便共享。</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> useTags = <span class="hljs-function">() =></span> &#123;
    <span class="hljs-keyword">const</span> [tags, setTags] = useState<&#123; <span class="hljs-attr">id</span>: <span class="hljs-built_in">number</span>, <span class="hljs-attr">name</span>: <span class="hljs-built_in">string</span> &#125;[]>([]);
    <span class="hljs-keyword">const</span> findTag = <span class="hljs-function">(<span class="hljs-params">id: <span class="hljs-built_in">number</span></span>) =></span> tags.filter(<span class="hljs-function"><span class="hljs-params">tag</span> =></span> tag.id === id)[<span class="hljs-number">0</span>];
    <span class="hljs-keyword">const</span> updateTag = <span class="hljs-function">(<span class="hljs-params">id: <span class="hljs-built_in">number</span>, obj: &#123; name: <span class="hljs-built_in">string</span> &#125;</span>) =></span> &#123;
        setTags(tags.map(<span class="hljs-function"><span class="hljs-params">tag</span> =></span> tag.id === id ? &#123;id, <span class="hljs-attr">name</span>: obj.name&#125; : tag));

    &#125;;
    <span class="hljs-keyword">const</span> deleteTag = <span class="hljs-function">(<span class="hljs-params">id: <span class="hljs-built_in">number</span></span>) =></span> &#123;
        setTags(tags.filter(<span class="hljs-function"><span class="hljs-params">tag</span> =></span> tag.id !== id));
    &#125;;
    <span class="hljs-keyword">const</span> addTag = <span class="hljs-function">() =></span> &#123;
        <span class="hljs-keyword">const</span> tagName = <span class="hljs-built_in">window</span>.prompt(<span class="hljs-string">'请输入标签名'</span>);
        <span class="hljs-keyword">if</span> (tagName !== <span class="hljs-literal">null</span> && tagName !== <span class="hljs-string">''</span>) &#123;
            setTags([...tags, &#123;<span class="hljs-attr">id</span>: createId(), <span class="hljs-attr">name</span>: tagName&#125;]);
        &#125;
    &#125;;
    <span class="hljs-keyword">return</span> &#123;tags, setTags, findTag, updateTag, deleteTag, addTag&#125;;
&#125;;

<span class="hljs-keyword">export</span> &#123;useTags&#125;;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>其他组件就可以使用 useTags 中的一些方法：</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> TagsSection: React.FC<Props> = <span class="hljs-function">(<span class="hljs-params">props</span>) =></span> &#123;
  <span class="hljs-comment">// 从useTags中提取出tag和addtag</span>
    <span class="hljs-keyword">const</span> &#123;tags, addTag&#125; = useTags();
    <span class="hljs-keyword">const</span> selectedTagIds = props.value;
  ......
    <span class="hljs-keyword">return</span> (
        <span class="xml"><span class="hljs-tag"><<span class="hljs-name">Wrapper</span>></span>
            <span class="hljs-tag"><<span class="hljs-name">button</span> <span class="hljs-attr">onClick</span>=<span class="hljs-string">&#123;addTag&#125;</span>></span>新增标签<span class="hljs-tag"></<span class="hljs-name">button</span>></span>
        <span class="hljs-tag"></<span class="hljs-name">Wrapper</span>></span></span>
    );
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            