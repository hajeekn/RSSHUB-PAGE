
---
title: '「✍ React Hook 封装一个Modal _」'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=2238'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 08:53:56 GMT
thumbnail: 'https://picsum.photos/400/300?random=2238'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">背景</h1>
<p>最近在和同事合作一个需求，其中很多模块都需要一个相同风格的简单弹窗组件，而项目中引入的antd-mobile无法直接满足需求，最后决定由我来做一次二次封装。</p>
<h1 data-id="heading-1">开始</h1>
<p>一开始我的理解是封装一层样式，新增一些特有的属性，其他的<code>props</code>透传就完事了，于是有了下面的组件
<code>CommonModal</code></p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">import</span> React <span class="hljs-keyword">from</span> <span class="hljs-string">'react'</span>
<span class="hljs-keyword">import</span> Modal, &#123; ModalProps &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'antd-mobile'</span>

<span class="hljs-keyword">interface</span> IProps <span class="hljs-keyword">extends</span> ModalProps &#123;
  <span class="hljs-attr">content</span>: <span class="hljs-built_in">string</span>
  commonModalClassName?: <span class="hljs-built_in">string</span>
&#125;

<span class="hljs-keyword">const</span> CommonModal: React.FC<IProps> = <span class="hljs-function">(<span class="hljs-params">props</span>) =></span> &#123;
  <span class="hljs-keyword">const</span> &#123; commonModalClassName = <span class="hljs-string">''</span>, content = <span class="hljs-string">''</span>, ...resProps&#125; = props
  <span class="hljs-keyword">return</span> (
     <span class="xml"><span class="hljs-tag"><<span class="hljs-name">div</span> <span class="hljs-attr">className</span>=<span class="hljs-string">&#123;</span>`<span class="hljs-attr">common-modal</span> $&#123; <span class="hljs-attr">commonModalClassName</span> &#125;`&#125;></span>
       <span class="hljs-tag"><<span class="hljs-name">Modal</span> &#123;<span class="hljs-attr">...resProps</span>&#125;></span>
         <span class="hljs-tag"><<span class="hljs-name">p</span> <span class="hljs-attr">className</span>=<span class="hljs-string">"common-modal-content"</span>></span>&#123; content &#125;<span class="hljs-tag"></<span class="hljs-name">p</span>></span>
       <span class="hljs-tag"></<span class="hljs-name">Modal</span>></span>
     <span class="hljs-tag"></<span class="hljs-name">div</span>></span></span>
  )
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>看起来简单粗暴没毛病。</p>
<h1 data-id="heading-2">使用Hook优化</h1>
<p>功能已经实现，但同事用的时候反馈，作为一个简单的弹窗，每次用的时候还需要定义好<code>state</code>，还要引入<code>CommonModal</code>组件, 比较麻烦</p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> [visible, setVisible] = useState(<span class="hljs-literal">false</span>)
<span class="hljs-keyword">const</span> [content, setContent] = useState(<span class="hljs-literal">false</span>
...
<span class="copy-code-btn">复制代码</span></code></pre>
<p>这时我想起来<code>antd-mobile</code>的<code>Modal</code>可以直接调用<code>Modal.alert</code>来唤起弹窗，对于多处复用的弹窗，像这样封装一个可执行的方法是不错的。先看看<code>antd-mobile</code>的实现。</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">alert</span>(<span class="hljs-params"></span>)</span>&#123;
  <span class="hljs-keyword">const</span> div: any = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'div'</span>);
  <span class="hljs-built_in">document</span>.body.appendChild(div);

  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">close</span>(<span class="hljs-params"></span>) </span>&#123;
    ReactDOM.unmountComponentAtNode(div);
    <span class="hljs-keyword">if</span> (div && div.parentNode) &#123;
      div.parentNode.removeChild(div);
    &#125;
  &#125;
  
  ReactDOM.render(
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">Modal</span>
      <span class="hljs-attr">visible</span>
      <span class="hljs-attr">transparent</span>
      <span class="hljs-attr">title</span>=<span class="hljs-string">&#123;title&#125;</span>
      <span class="hljs-attr">transitionName</span>=<span class="hljs-string">"am-zoom"</span>
      <span class="hljs-attr">closable</span>=<span class="hljs-string">&#123;false&#125;</span>
      <span class="hljs-attr">maskClosable</span>=<span class="hljs-string">&#123;false&#125;</span>
      <span class="hljs-attr">footer</span>=<span class="hljs-string">&#123;footer&#125;</span>
      <span class="hljs-attr">maskTransitionName</span>=<span class="hljs-string">"am-fade"</span>
      <span class="hljs-attr">platform</span>=<span class="hljs-string">&#123;platform&#125;</span>
      <span class="hljs-attr">wrapProps</span>=<span class="hljs-string">&#123;&#123;</span> <span class="hljs-attr">onTouchStart:</span> <span class="hljs-attr">onWrapTouchStart</span> &#125;&#125;
    ></span>
      <span class="hljs-tag"><<span class="hljs-name">div</span> <span class="hljs-attr">className</span>=<span class="hljs-string">&#123;</span>`$&#123;<span class="hljs-attr">prefixCls</span>&#125;<span class="hljs-attr">-alert-content</span>`&#125;></span>&#123;message&#125;<span class="hljs-tag"></<span class="hljs-name">div</span>></span>
    <span class="hljs-tag"></<span class="hljs-name">Modal</span>></span></span>,
    div,
  );
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>贴了部分核心代码，其实就是用ReactDOM来渲染弹窗，用dom.parentNode.removeChild来卸载弹窗。</p>
<p>用Hook实现</p>
<p><code>useCommonModal</code></p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">import</span> React <span class="hljs-keyword">from</span> <span class="hljs-string">'react'</span>
<span class="hljs-keyword">import</span> ReactDOM <span class="hljs-keyword">from</span> <span class="hljs-string">'react-dom'</span>
<span class="hljs-keyword">import</span> CommonModal, &#123; CommonModalProps &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'./CommonModal'</span>

<span class="hljs-keyword">const</span> CommonModal: React.FC<CommonModalProps> = <span class="hljs-function">(<span class="hljs-params">&#123;...props&#125;</span>) =></span> <span class="xml"><span class="hljs-tag"><<span class="hljs-name">CommonModal</span> &#123;<span class="hljs-attr">...props</span>&#125; /></span></span>

<span class="hljs-keyword">type</span> IProps = Pick<CommonModalProps, <span class="hljs-string">'title'</span> | <span class="hljs-string">'content'</span> | <span class="hljs-string">'btnText'</span>>

<span class="hljs-keyword">const</span> ModalClassName = <span class="hljs-string">'hook-modal'</span>

<span class="hljs-keyword">const</span> useCommonModal = <span class="hljs-function">(<span class="hljs-params">props:IProps</span>) =></span> &#123;

  <span class="hljs-keyword">const</span> close = useCallback(<span class="hljs-function">()=></span>&#123;
     <span class="hljs-keyword">let</span> dom = <span class="hljs-built_in">document</span>.getElementByClassName(<span class="hljs-string">'hook-modal'</span>)[<span class="hljs-number">0</span>]
     ReactDOM.unmountComponentAtNode(dom)
     <span class="hljs-keyword">if</span>(dom && dom.parentNode)&#123;
       dom.parentNode.removeChild(dom);
     &#125;
  &#125;,[])
  
  <span class="hljs-keyword">const</span> show = useCallback(<span class="hljs-function">()=></span>&#123;
    <span class="hljs-keyword">const</span> Root = <span class="hljs-built_in">document</span>.body
    <span class="hljs-keyword">let</span> dom = <span class="hljs-built_in">document</span>.getElementByClassName(<span class="hljs-string">'hook-modal'</span>)[<span class="hljs-number">0</span>]
    <span class="hljs-keyword">if</span>(!dom)&#123;
      dom = <span class="hljs-built_in">document</span>.createElement(<span class="hljs-string">'div'</span>)
      dom.className = ModalClassName
      Root.appendChild(dom)
    &#125;
    
    ReactDOM.render(
     <span class="xml"><span class="hljs-tag"><<span class="hljs-name">CommonModal</span> &#123;<span class="hljs-attr">...props</span>&#125;/></span></span>
    , dom)
    <span class="hljs-comment">// 等价于</span>
    <span class="hljs-comment">// const ele = React.createElement(CommonModal, &#123; ...props&#125;, null)</span>
    <span class="hljs-comment">// ReactDOM.render(ele, dom)</span>
  &#125;,[])
  
  <span class="hljs-keyword">return</span> &#123;
    close,
    show
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>使用</code></p>
<pre><code class="hljs language-ts copyable" lang="ts"><span class="hljs-keyword">const</span> &#123; show, close &#125; = useCommonModal(&#123;
  <span class="hljs-attr">title</span>: <span class="hljs-string">''</span>,
  <span class="hljs-attr">content</span>: <span class="hljs-string">''</span>,
  <span class="hljs-attr">btnText</span>: <span class="hljs-string">''</span>,
&#125;)
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            