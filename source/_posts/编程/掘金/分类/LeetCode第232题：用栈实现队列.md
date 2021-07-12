
---
title: 'LeetCode第232题：用栈实现队列'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=449'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 22:53:40 GMT
thumbnail: 'https://picsum.photos/400/300?random=449'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">题干：</h2>
<p>请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：</p>
<p>实现 MyQueue 类：</p>
<ul>
<li>void push(int x) 将元素 x 推到队列的末尾</li>
<li>int pop() 从队列的开头移除并返回元素</li>
<li>int peek() 返回队列开头的元素</li>
<li>boolean empty() 如果队列为空，返回 true ；否则，返回 false</li>
</ul>
<p>来源：力扣（LeetCode）
链接：<a href="https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fimplement-queue-using-stacks" target="_blank" rel="nofollow noopener noreferrer" title="https://leetcode-cn.com/problems/implement-queue-using-stacks" ref="nofollow noopener noreferrer">leetcode-cn.com/problems/im…</a>
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。</p>
<h2 data-id="heading-1">解法：</h2>
<p>废话不多说，队列是先进先出，栈是先进后出，刚进来的元素就在栈顶，我们可以使用这一特性定义两个栈s1，s2，在每次push时，先将s2清空，再将数据push到s1上，再将s1依次压栈到s2上，这就实现了栈底元素到队列头。</p>
<p>接着当我们pop队列头时，我们将s2的栈顶删除，这就相当于我们删除了s2队列的首部。但是同时我们还要将s1清空，因为我们需要两个栈保持同步，再将s2依次压栈到s1，这样我们保持了 s1的不变性。</p>
<p>代码实现：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">/**
 * Initialize your data structure here.
 */</span>
<span class="hljs-keyword">var</span> MyQueue = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-built_in">this</span>.stack1 = [];
    <span class="hljs-built_in">this</span>.stack2 = [];
&#125;;

<span class="hljs-comment">/**
 * Push element x to the back of queue. 
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;number&#125;</span> <span class="hljs-variable">x</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;void&#125;</span></span>
 */</span>
MyQueue.prototype.push = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">x</span>) </span>&#123;
    <span class="hljs-built_in">this</span>.stack2 = []
    <span class="hljs-built_in">this</span>.stack1.push(x);
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-built_in">this</span>.stack1.length - <span class="hljs-number">1</span>; i >= <span class="hljs-number">0</span>; i--) &#123;
        <span class="hljs-built_in">this</span>.stack2.push(<span class="hljs-built_in">this</span>.stack1[i])
    &#125;
&#125;;

<span class="hljs-comment">/**
 * Removes the element from in front of queue and returns that element.
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
MyQueue.prototype.pop = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">let</span> pop=<span class="hljs-built_in">this</span>.stack2.pop();
    <span class="hljs-built_in">this</span>.stack1=[]
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-built_in">this</span>.stack2.length - <span class="hljs-number">1</span>; i >= <span class="hljs-number">0</span>; i--) &#123;
        <span class="hljs-built_in">this</span>.stack1.push(<span class="hljs-built_in">this</span>.stack2[i])
    &#125;
    <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.stack1)
    <span class="hljs-keyword">return</span> pop;
&#125;;

<span class="hljs-comment">/**
 * Get the front element.
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;number&#125;</span></span>
 */</span>
MyQueue.prototype.peek = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.stack2[<span class="hljs-built_in">this</span>.stack2.length - <span class="hljs-number">1</span>]
&#125;;

<span class="hljs-comment">/**
 * Returns whether the queue is empty.
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;boolean&#125;</span></span>
 */</span>
MyQueue.prototype.empty = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-keyword">return</span> <span class="hljs-built_in">this</span>.stack2.length == <span class="hljs-number">0</span> ? <span class="hljs-literal">true</span> : <span class="hljs-literal">false</span>
&#125;;

<span class="hljs-comment">/**
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */</span>
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            