
---
title: 'flex布局小结'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=5256'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 19:56:46 GMT
thumbnail: 'https://picsum.photos/400/300?random=5256'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">前言</h3>
<p>随着时代的发展，人们越来越多的重视前端的用户体验，不论是在 web 端，还是移动端（小程序、H5、RN...），特别是在移动端，因为设备屏幕的不同，就需要前端开发去适配不同的屏幕大小，对布局的就有要求了。</p>
<p>在现在的开发过程中，我们经常会用到 <code>flex</code> 布局，从而去适配不同的屏幕大小。</p>
<p>今天，从的使用经验中去谈一下 flex。</p>
<h3 data-id="heading-1">什么是<code>flex</code>布局？</h3>
<p>flex 布局 又叫 <strong>弹性布局</strong>，我们可以想象在一个盒子容器中有多个子元素，当我们去改变”盒子“的大小的时候，<strong>弹性布局</strong>为我们提供了一种子元素在盒子中的布局规则</p>
<h3 data-id="heading-2"><code>flex</code>布局的属性</h3>
<h4 data-id="heading-3">父容器的属性</h4>
<ul>
<li>
<p><code>display: flex</code></p>
<p>设置容器使用弹性布局</p>
</li>
<li>
<p><code>flex-direction</code></p>
<p>设置主轴的排列方式 （子元素的排列方向）</p>

























<table><thead><tr><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td><code>row</code></td><td>主轴横向，子元素从左到右排列</td></tr><tr><td><code>column</code></td><td>主轴纵向，子元素自上而下排列</td></tr><tr><td><code>row-reverse</code></td><td>主轴横向反转，子元素从右到左排列（与row相反）</td></tr><tr><td><code>column-reverse</code></td><td>主轴纵向反转，子元素自下而上排列（与<code>column</code>相反）</td></tr></tbody></table>
</li>
<li>
<p><code>justify-content</code></p>
<p>设置子元素在<strong>主轴方向</strong>的对齐规则</p>





























<table><thead><tr><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td><code>flex-start</code></td><td><em>默认值</em>，子元素从主轴的开始方向到结束方向依次排列，与主轴的开始方向对齐（左对齐）</td></tr><tr><td><code>flex-end</code></td><td>子元素从主轴的结束方向到开始方向依次排列（与<code>flex-start</code>相反），与主轴的结束方向对齐（右对齐）</td></tr><tr><td><code>center</code></td><td>子元素以主轴的中间方向居中对齐</td></tr><tr><td><code>space-around</code></td><td>两端对齐，子元素两侧的间隔相等，子元素之间的间隔是头尾子元素与边框的间隔的两倍</td></tr><tr><td><code>space-between</code></td><td>两端对齐，每个子元素的间隔相等</td></tr></tbody></table>
</li>
<li>
<p><code>align-items</code></p>
<p>设置子元素在<strong>交叉轴方向</strong>（和主轴垂直交叉的辅助轴）的对齐规则</p>





























<table><thead><tr><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td><code>flex-start</code></td><td>交叉轴的起点对齐</td></tr><tr><td><code>flex-end</code></td><td>交叉轴的终点对齐</td></tr><tr><td><code>center</code></td><td>交叉轴的中间对齐</td></tr><tr><td><code>baseline</code></td><td>子元素的第一行文字的基线对齐</td></tr><tr><td><code>stretch</code></td><td><em>默认值</em>，子元素未设置高度或者高度为auto，将占满整个容器的高度</td></tr></tbody></table>
</li>
<li>
<p><code>align-content</code></p>
<p>设置纵轴在内容项之间和周围分配空间（多跟轴线），<strong>子元素只有一行时无效生效</strong></p>





































<table><thead><tr><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td><code>flex-start</code></td><td>从起始点开始放置flex元素</td></tr><tr><td><code>flex-end</code></td><td>从终止点开始放置flex元素</td></tr><tr><td><code>center</code></td><td>将项目放置在中点 与交叉轴的中间对齐</td></tr><tr><td><code>space-between</code></td><td>均匀分布项目，第一项与起始点齐平，最后一项与终止点齐平</td></tr><tr><td><code>space-around</code></td><td>均匀分布项目，项目在两端有一半大小的空间</td></tr><tr><td><code>space-evenly</code></td><td>均匀分布项目,项目周围有相等的空间</td></tr><tr><td><code>stretch</code></td><td><em>默认值</em>，均匀分布项目，拉伸‘自动’-大小的项目以充满容器</td></tr></tbody></table>
</li>
<li>
<p><code>flex-wrap</code></p>
<p>指定 flex 元素单行显示还是多行显示 。如果允许换行，这个属性允许你控制行的堆叠方向</p>





















<table><thead><tr><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td>nowrap</td><td><em>默认值</em> 不换行。<code>flex</code> 的子元素被摆放到到一行，这可能导致溢出 <code>flex</code> 容器</td></tr><tr><td>wrap</td><td>换行，第一行在上方。</td></tr><tr><td>wrap-reverse</td><td>换行，第一行在下方。和<code>wrap</code>相反</td></tr></tbody></table>
</li>
<li>
<p><code>flex-flow</code></p>
<p><code>flex-flow</code> 属性是 <code>flex-direction</code> 和 <code>flex-wrap</code> 的简写，默认值是 <code>row nowrap</code></p>
<pre><code class="copyable">flex-flow: <flex-direction> || <flex-wrap>;
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
</ul>
<h4 data-id="heading-4">子元素的属性</h4>
<ul>
<li>
<p><code>flex-grow</code></p>
<p>设置元素的放大比例（flex增长系数），负值无效，默认为 0。</p>
</li>
<li>
<p><code>flex-shrink</code></p>
<p>设置元素的收缩规则，<code>flex</code> 元素仅在默认宽度之和大于容器的时候才会发生收缩，负值无效，默认为 1。</p>
</li>
<li>
<p><code>flex-basis</code></p>
<p>设置元素在主轴方向上的初始大小。如果不使用 <code>box-sizing</code> 改变盒模型的话，那么这个属性就决定了 <code>flex</code> 元素的内容盒（content-box）的尺寸。默认为<code>auto</code>，即是元素的本来大小</p>
<blockquote>
<p>当一个元素同时被设置了 flex-basis (除值为 auto 外) 和 width (或者在 flex-direction: column 情况下设置了height) , flex-basis 具有更高的优先级.</p>
</blockquote>
</li>
<li>
<p><code>flex</code></p>
<p>设置了弹性项目如何增大或缩小以适应其弹性容器中可用的空间。是<code>flex-grow</code>, <code>flex-shrink</code> 和 <code>flex-basis</code>的简写，默认值为<code>0 1 auto</code></p>
<p>它可以使用<strong>一个</strong>，<strong>两个</strong>或<strong>三个</strong>值来指定 flex属性</p>
<ol>
<li>单值语法(<strong>一个</strong>)</li>
</ol>
<ul>
<li>
<p>一个无单位数(<code>number</code>): 它会被当作<code>flex:<number> 1 0</code>; <code>flex-shrink</code>的值被假定为<code>1</code>，然后<code>flex-basis</code> 的值被假定为 <code>0</code>。</p>
<p><strong>常见用法:</strong> <em><strong>flex: 1</strong></em>。</p>
</li>
<li>
<p>一个有效的宽度(<code>width</code>)值: 它会被当作 <code>flex-basis</code> 的值。</p>
</li>
<li>
<p>关键字 <code>none (1 1 auto) </code>，<code>auto (0 0 auto)</code>.</p>
</li>
</ul>
<ol start="2">
<li>双值语法(<strong>两个</strong>)</li>
</ol>
<p><strong>第一个值</strong>必须为<em>一个无单位数</em>，并且它会被当作 <code>flex-grow</code> 的值</p>
<p><strong>第二个值</strong>有以下两种格式：</p>
<ul>
<li><em>一个无单位数</em>: 它会被当作 <code>flex-shrink</code> 的值。</li>
<li><em>一个有效的宽度值</em>: 它会被当作 <code>flex-basis</code> 的值。</li>
</ul>
</li>
<li>
<p><code>align-self</code></p>
<p>设置当前元素的对齐方式，覆盖已有的 <code>align-items</code> 的值。</p>

































<table><thead><tr><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td><code>auto</code></td><td><em>默认值</em>，设置为父元素的 <code>align-items</code> 值，如果没有父元素，则等同于stretch</td></tr><tr><td><code>flex-start</code></td><td>交叉轴的起点对齐</td></tr><tr><td><code>flex-end</code></td><td>交叉轴的终点对齐</td></tr><tr><td><code>center</code></td><td>交叉轴的中间对齐</td></tr><tr><td><code>baseline</code></td><td>子元素的第一行文字的基线对齐</td></tr><tr><td><code>stretch</code></td><td>子元素未设置高度或者高度为auto，将占满整个容器的高度</td></tr></tbody></table>
</li>
</ul>
<p>以上就是常用的<code>flex</code>布局常用的属性，如有错误，请纠结。</p>
<p>附参考：</p>
<ul>
<li><a href="https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2FCSS_Flexible_Box_Layout%2FBasic_Concepts_of_Flexbox" target="_blank" rel="nofollow noopener noreferrer" title="https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox" ref="nofollow noopener noreferrer">flex 布局</a></li>
<li><a href="https://link.juejin.cn/?target=http%3A%2F%2Fwww.ruanyifeng.com%2Fblog%2F2015%2F07%2Fflex-grammar.html" target="_blank" rel="nofollow noopener noreferrer" title="http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html" ref="nofollow noopener noreferrer">阮一峰 Flex 布局教程：语法篇</a></li>
</ul></div>  
</div>
            