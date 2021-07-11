
---
title: 'JS循环大总结， for, forEach，for in，for of, map区别'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=9662'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 07:18:20 GMT
thumbnail: 'https://picsum.photos/400/300?random=9662'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">map（数组方法）：</h2>
<h3 data-id="heading-1">特性：</h3>
<ol>
<li>map不改变原数组但是会 返回新数组</li>
<li>可以使用break中断循环，可以使用return返回到外层函数</li>
</ol>
<h3 data-id="heading-2">实例：</h3>
<pre><code class="hljs language-let copyable" lang="let">let newarr=arr.map(i=>&#123;
return i+=1;
console.log(i);
&#125;)
console.log(arr)//1,3,4---不会改变原数组
console.log(newarr)//[2,4,5]---返回新数组
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-3">forEach（数组方法）：</h2>
<h3 data-id="heading-4">特性：</h3>
<ol>
<li>便利的时候更加简洁，效率和for循环相同，不用关心集合下标的问题，减少了出错的概率。</li>
<li>没有返回值</li>
<li>不能使用break中断循环，不能使用return返回到外层函数</li>
</ol>
<h3 data-id="heading-5">实例：</h3>
<pre><code class="hljs language-let copyable" lang="let">let newarr=arr.forEach(i=>&#123;
 i+=1;
console.log(i);//2,4,5
&#125;)
console.log(arr)//[1,3,4]
console.log(newarr)//undefined
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-6">注意：</h3>
<ol>
<li>forEach() 对于空数组是不会执行回调函数的。</li>
<li>for可以用continue跳过循环中的一个迭代，forEach用continue会报错。</li>
<li>forEach() 需要用 return 跳过循环中的一个迭代，跳过之后会执行下一个迭代。</li>
</ol>
<h2 data-id="heading-7">for in(大部分用于对象)：</h2>
<p>用于循环遍历数组或对象属性</p>
<h3 data-id="heading-8">特性：</h3>
<p>可以遍历数组的键名，遍历对象简洁方便
###实例：</p>
<pre><code class="hljs language-//首先遍历对象 copyable" lang="//首先遍历对象">   let person=&#123;name:"小白",age:28,city:"北京"&#125;
   let text=""
   for (let i in person)&#123;
      text+=person[i]
   &#125;
   输出结果为：小白28北京
//其次在尝试一些数组
   let arry=[1,2,3,4,5]
   for (let i in arry)&#123;
        console.log(arry[i])
    &#125;
//能输出出来，证明也是可以的
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-9">for of（不能遍历对象）：</h2>
<h3 data-id="heading-10">特性：</h3>
<ol>
<li>（可遍历map，object,array,set string等）用来遍历数据，比如组中的值</li>
<li>避免了for in的所有缺点，可以使用break,continue和return，不仅支持数组的遍历，还可以遍历类似数组的对象。</li>
</ol>
<pre><code class="hljs language-//遍历数组 copyable" lang="//遍历数组">   let arr=["nick","freddy","mike","james"];
    for (let item of arr)&#123;
        console.log(item)
    &#125;
//暑促结果为nice freddy mike james
//遍历对象
   let person=&#123;name:"老王",age:23,city:"唐山"&#125;
   for (let item of person)&#123;
        console.log(item)
    &#125;
//我们发现它是不可以的
//但是它和forEach有个解决方法，结尾介绍

<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-11">总结：</h2>
<ul>
<li>forEach 遍历列表值,不能使用 break 语句或使用 return 语句</li>
<li>for in 遍历对象键值(key),或者数组下标,不推荐循环一个数组</li>
<li>for of 遍历列表值,允许遍历 Arrays（数组）, Strings（字符串）, Maps（映射）, Sets（集合）等可迭代的数据结构等.在 ES6 中引入的 for of 循环，以替代 for in 和 forEach() ，并支持新的迭代协议。</li>
<li>for in循环出的是key，for of循环出的是value；</li>
<li>for of是ES6新引入的特性。修复了ES5的for in的不足；</li>
<li>for of不能循环普通的对象，需要通过和Object.keys()搭配使用。</li>
</ul></div>  
</div>
            