
---
title: 'React项目性能优化'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=6738'
author: 掘金
comments: false
date: Wed, 14 Jul 2021 19:48:31 GMT
thumbnail: 'https://picsum.photos/400/300?random=6738'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">优化目标：减少组件不必要的diff和重渲染</h3>
<hr>
<ul>
<li>使用mobx observer <em><code>组件状态发生改变，以该组件为根节点的组件树上的所有子孙组件都会进入diff，使用了oberser的组件只有在状态改变时才会diff，否则跳过diff</code></em></li>
</ul>
<pre><code class="hljs language-js copyable" lang="js"> @observer Component or observer(Component)
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>函数组件内联函数props使用useCallback， <strong>要合理使用</strong>  <a href="https://link.juejin.cn/?target=https%3A%2F%2Fwww.cnblogs.com%2FQooo%2Fp%2F13705897.html" target="_blank" rel="nofollow noopener noreferrer" title="https://www.cnblogs.com/Qooo/p/13705897.html" ref="nofollow noopener noreferrer">参考文章</a></li>
</ul>
<pre><code class="hljs language-js copyable" lang="js"><div>
    <span class="xml"><span class="hljs-tag"><<span class="hljs-name">ClickBtn</span>
        <span class="hljs-attr">onClick</span>=<span class="hljs-string">&#123;useCallback(()</span> =></span> &#123;
            console.log("parent");
            setCount((val) => val + 1);
        &#125;, [])&#125;
    /></span>
</div>
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>函数组件使用React.memo(Component, areEqual)并设置props比较方法来减少不必要的渲染</li>
<li>useMemo 细粒度优化，对于某些高开销的计算，设置缓存，只有在依赖发生变化时才会重新计算，比如项目中多层级树的数据初始化</li>
<li>pureComponent</li>
<li>shouldComponentUpdate()</li>
</ul></div>  
</div>
            