
---
title: 'react-redux'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43cffc0bf3474c49ac804dcd08503734~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Wed, 14 Jul 2021 19:47:58 GMT
thumbnail: 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43cffc0bf3474c49ac804dcd08503734~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>1.create-react-app reactredux(项目名称)</p>
<p>2.cd .\reactredux\ (进入项目目录)</p>
<p>3.npm i react-redux
npm i redux-thunk
npm i redux-devtools-extension
npm i axios</p>
<p>4.项目目录结构</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43cffc0bf3474c49ac804dcd08503734~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>源码---------------------------------------------------------------------------------：</p>
<p>App.js</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> React <span class="hljs-keyword">from</span> <span class="hljs-string">'react'</span>
<span class="hljs-keyword">import</span> &#123; Provider &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'react-redux'</span>
<span class="hljs-keyword">import</span> store <span class="hljs-keyword">from</span> <span class="hljs-string">'./redux/store'</span>
<span class="hljs-keyword">import</span> WithList <span class="hljs-keyword">from</span> <span class="hljs-string">'./container/WithList'</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">App</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-keyword">return</span> (
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">Provider</span> <span class="hljs-attr">store</span>=<span class="hljs-string">&#123;store&#125;</span>></span>
      <span class="hljs-tag"><<span class="hljs-name">WithList</span>></span><span class="hljs-tag"></<span class="hljs-name">WithList</span>></span>
    <span class="hljs-tag"></<span class="hljs-name">Provider</span>></span></span>
  )
&#125;

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> App

<span class="copy-code-btn">复制代码</span></code></pre>
<p>index.js</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> React <span class="hljs-keyword">from</span> <span class="hljs-string">'react'</span>;
<span class="hljs-keyword">import</span> ReactDOM <span class="hljs-keyword">from</span> <span class="hljs-string">'react-dom'</span>;
<span class="hljs-keyword">import</span> App <span class="hljs-keyword">from</span> <span class="hljs-string">'./App'</span>;

ReactDOM.render(
  <span class="xml"><span class="hljs-tag"><<span class="hljs-name">React.StrictMode</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">App</span> /></span>
  <span class="hljs-tag"></<span class="hljs-name">React.StrictMode</span>></span></span>,
  <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'root'</span>)
);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>constants.js</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> GET_DATA = <span class="hljs-string">'GET_DATA'</span>
<span class="hljs-keyword">export</span> &#123; GET_DATA &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>reducer.js</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> &#123; GET_DATA &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'./constants'</span>
<span class="hljs-keyword">let</span> initState = &#123;
  <span class="hljs-attr">list</span>: [],
&#125;

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">fn</span>(<span class="hljs-params">state = initState, action</span>) </span>&#123;
  <span class="hljs-keyword">switch</span> (action.type) &#123;
    <span class="hljs-keyword">case</span> GET_DATA:
      <span class="hljs-keyword">return</span> &#123;
        ...state,
        <span class="hljs-attr">list</span>: action.data,
      &#125;
    <span class="hljs-attr">default</span>:
      <span class="hljs-keyword">return</span> state
  &#125;
&#125;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> fn

<span class="copy-code-btn">复制代码</span></code></pre>
<p>action.js</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> axios <span class="hljs-keyword">from</span> <span class="hljs-string">'axios'</span>
<span class="hljs-keyword">import</span> &#123; GET_DATA &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'./constants'</span>

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getData</span>(<span class="hljs-params">data</span>) </span>&#123;
  <span class="hljs-keyword">return</span> &#123; <span class="hljs-attr">type</span>: GET_DATA, data &#125;
&#125;

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getDataAsync</span>(<span class="hljs-params"></span>) </span>&#123;
  <span class="hljs-keyword">return</span> <span class="hljs-keyword">async</span> (dispatch) => &#123;
    <span class="hljs-keyword">let</span> res = <span class="hljs-keyword">await</span> axios(&#123;
      <span class="hljs-attr">method</span>: <span class="hljs-string">'GET'</span>,
      <span class="hljs-attr">url</span>: <span class="hljs-string">'http://127.0.0.1:5000/test'</span>,
    &#125;)
    <span class="hljs-comment">// console.log(res)</span>
    dispatch(getData(res.data))
  &#125;
&#125;

<span class="hljs-keyword">export</span> &#123; getDataAsync &#125;

<span class="copy-code-btn">复制代码</span></code></pre>
<p>store.js</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> &#123; createStore, applyMiddleware &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'redux'</span>
<span class="hljs-keyword">import</span> &#123; composeWithDevTools &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'redux-devtools-extension'</span>
<span class="hljs-keyword">import</span> thunk <span class="hljs-keyword">from</span> <span class="hljs-string">'redux-thunk'</span>
<span class="hljs-keyword">import</span> reducer <span class="hljs-keyword">from</span> <span class="hljs-string">'./reducer'</span>

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> createStore(
  reducer,
  process.env.NODE_ENV === <span class="hljs-string">'development'</span>
    ? composeWithDevTools(applyMiddleware(thunk))
    : applyMiddleware(thunk)
)

<span class="copy-code-btn">复制代码</span></code></pre>
<p>List.jsx</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> React <span class="hljs-keyword">from</span> <span class="hljs-string">'react'</span>
<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">List</span>(<span class="hljs-params">props</span>) </span>&#123;
  <span class="hljs-built_in">console</span>.log(props.list)
  <span class="hljs-keyword">return</span> (
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span>></span>
      <span class="hljs-tag"><<span class="hljs-name">button</span>
        <span class="hljs-attr">onClick</span>=<span class="hljs-string">&#123;()</span> =></span> &#123;
          props.getDataAsync()
        &#125;&#125;>
        按钮
      <span class="hljs-tag"></<span class="hljs-name">button</span>></span>
      <span class="hljs-tag"><<span class="hljs-name">ul</span>></span>
        &#123;props.list.map((item, index) => &#123;
          return (
            <span class="hljs-tag"><<span class="hljs-name">li</span> <span class="hljs-attr">key</span>=<span class="hljs-string">&#123;index&#125;</span>></span>
              <span class="hljs-tag"><<span class="hljs-name">h3</span>></span>&#123;item.name&#125;<span class="hljs-tag"></<span class="hljs-name">h3</span>></span>
              <span class="hljs-tag"><<span class="hljs-name">p</span>></span>&#123;item.age&#125;<span class="hljs-tag"></<span class="hljs-name">p</span>></span>
              <span class="hljs-tag"><<span class="hljs-name">p</span>></span>&#123;item.info&#125;<span class="hljs-tag"></<span class="hljs-name">p</span>></span>
            <span class="hljs-tag"></<span class="hljs-name">li</span>></span>
          )
        &#125;)&#125;
      <span class="hljs-tag"></<span class="hljs-name">ul</span>></span>
    <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
  )
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>WhitList.jsx</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">import</span> &#123; connect &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'react-redux'</span>
<span class="hljs-keyword">import</span> List <span class="hljs-keyword">from</span> <span class="hljs-string">'../components/List'</span>
<span class="hljs-keyword">import</span> &#123; getDataAsync &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'../redux/action'</span>

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> connect(
  <span class="hljs-function">(<span class="hljs-params">state</span>) =></span> (&#123;
    <span class="hljs-attr">list</span>: state.list,
  &#125;),
  &#123; getDataAsync &#125;
)(List)

<span class="copy-code-btn">复制代码</span></code></pre>
<p>项目接口文件
<a href="https://juejin.cn/post/6984991228307701774/" target="_blank" title="https://juejin.cn/post/6984991228307701774/">juejin.cn/post/698499…</a></p></div>  
</div>
            