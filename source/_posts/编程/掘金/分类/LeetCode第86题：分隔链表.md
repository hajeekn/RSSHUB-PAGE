
---
title: 'LeetCode第86题：分隔链表'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fd8b0c130d8f421aa1a42f88b4dc6f1c~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 22:53:51 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fd8b0c130d8f421aa1a42f88b4dc6f1c~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">题干</h2>
<p>给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。</p>
<p>你应当 保留 两个分区中每个节点的初始相对位置。</p>
<p><strong>实例1</strong></p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fd8b0c130d8f421aa1a42f88b4dc6f1c~tplv-k3u1fbpfcp-zoom-1.image" alt="img" loading="lazy" referrerpolicy="no-referrer"></p>
<pre><code class="copyable">输入：head = [1,4,3,2,5,2], x = 3
输出：[1,2,2,4,3,5]
<span class="copy-code-btn">复制代码</span></code></pre>
<p><strong>示例 2：</strong></p>
<pre><code class="copyable">输入：head = [2,1], x = 2
输出：[1,2]
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-1">解法:合成链表</h2>
<p>我们定义两个链表分别为目标数的左边和右边。然后进行一次循环判断，向两个链表中加加节点即可。最后再将两个链表连接形成我们的结果链表：</p>
<p>代码实现：</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">/**
 * Definition for singly-linked list.
 * function ListNode(val, next) &#123;
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * &#125;
 */</span>
<span class="hljs-comment">/**
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;ListNode&#125;</span> <span class="hljs-variable">head</span></span>
 * <span class="hljs-doctag">@param <span class="hljs-type">&#123;number&#125;</span> <span class="hljs-variable">x</span></span>
 * <span class="hljs-doctag">@return <span class="hljs-type">&#123;ListNode&#125;</span></span>
 */</span>
<span class="hljs-keyword">var</span> partition = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">head, x</span>) </span>&#123;
    <span class="hljs-keyword">let</span> left = <span class="hljs-keyword">new</span> ListNode(-<span class="hljs-number">1</span>)
    <span class="hljs-keyword">let</span> right = <span class="hljs-keyword">new</span> ListNode(-<span class="hljs-number">1</span>)
    <span class="hljs-keyword">let</span> currentLeft = left;
    <span class="hljs-keyword">let</span> currentRight = right;
    <span class="hljs-keyword">while</span> (head != <span class="hljs-literal">null</span>) &#123;
        <span class="hljs-keyword">if</span> (head.val >= x) &#123;
            <span class="hljs-keyword">let</span> node1 = <span class="hljs-keyword">new</span> ListNode(head.val)
            currentRight.next = node1
            currentRight = currentRight.next;
        &#125; <span class="hljs-keyword">else</span> &#123;
            <span class="hljs-keyword">let</span> node2 = <span class="hljs-keyword">new</span> ListNode(head.val)
            currentLeft.next = node2
            currentLeft = currentLeft.next;
        &#125;
        head = head.next
    &#125;
    currentLeft.next=right.next;
    <span class="hljs-keyword">return</span> left.next
&#125;;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            