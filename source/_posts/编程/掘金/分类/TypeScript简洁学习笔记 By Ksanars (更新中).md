
---
title: 'TypeScript简洁学习笔记 By Ksanars (更新中)'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=1254'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 19:12:20 GMT
thumbnail: 'https://picsum.photos/400/300?random=1254'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>前排提醒：作者只是一个在校大学生，文章内容大部分来自于自己看书看视频后的总结以及自己的推断和思考，可能会有不严谨的地方，望指正。</p>
<p>一句话简单暴力理解TS：<br>
<strong>TypeScript就是在你声明的变量的后面加一个“：”，冒号后面写你限定的类型，将动态类型语言js规范为一个静态类型语言ts，使其在编译期间就发现可能存在的错误，减少后续因类型原因导致的错误</strong></p>
<p>TypeScript的安装：</p>
<p><code>npm install -g typescript </code><br>
从npm全局安装ts</p>
<p><code>tsc -v</code><br>
通过tsc查看当前安装的ts版本</p>
<p>hello函数 by ts</p>
<pre><code class="copyable">const hello = (name : string) => &#123;
  console.log(`hello $&#123;name&#125;`)
&#125;

hello('kasnars')
<span class="copy-code-btn">复制代码</span></code></pre>
<p>undefined是所有类型的子类型，所有类型都可以被赋值为undefined</p>
<pre><code class="copyable">let num : number = undefined
<span class="copy-code-btn">复制代码</span></code></pre>
<p>将变量设为any 可以任意改变类型和调用方法  但是频繁使用any会丧失ts本身的意义，并且any类型无法触发ide的方法提示</p>
<pre><code class="copyable">let anydata : any  = 4
anydata = 'is string'
anydata = true
<span class="copy-code-btn">复制代码</span></code></pre>
<p>联合类型：将变量声明为多种类型，不再为单一类型。用 ' | ' 分隔多种类型</p>
<pre><code class="copyable">let unitype : number | string  = 123
unitype = 'string'
<span class="copy-code-btn">复制代码</span></code></pre>
<p>定义数组类型，对数组内的内容进行限制，例如下例将数组内容限制为number</p>
<pre><code class="copyable">let arrnum : number[] = [1,2,3]
arrnum.push(4)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>Tuple元组：类似于将限定了类型的多个数组组合到一起（参考pytho元组）限定几个就只能写几个，下列限定了两个数据，如果出现了第三个数据则会报错</p>
<pre><code class="copyable">let userinfo : [string, number] = ['kasnars', 20]
userinfo = ['lyx', 18]
<span class="copy-code-btn">复制代码</span></code></pre>
<p>interface接口：<br>
1.对对象形状进行描述<br>
2.对类进行抽象<br>
类似与事先规定好了一种类型，可以在定义类的时候直接调用这个接口来声明类型，而不用再去声明string之类</p>
<pre><code class="copyable">interface Person&#123;
    name: string;
    age: number;
&#125;

let kasnars : Person = &#123;
    name: 'kasnars',
    age: '20'
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><em>注意：interface的声明中用分号分隔，不是对象中的逗号</em><br>
一般情况下interface定义了几个类型，调用这个interface的对象也得有几个类型，除非在某一个类型的后面加上问号，加上问号后在调用这个接口进行定义时，有问号的类型为可选项，例如</p>
<pre><code class="copyable">interface Person&#123;
    name: string;
    age?: number;
&#125;

let kasnars : Person = &#123;
    name: 'kasnars'
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>对接口里的属性添加readonly属性可以将这个属性变为只读，在初次被赋值后不可再被修改，类似与一个const常量，但是const是用于限制一个变量的，readonly用于限制对象里的一个属性。</p>
<pre><code class="copyable">interface Person&#123;
    readonly id : number;
    name：string;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            