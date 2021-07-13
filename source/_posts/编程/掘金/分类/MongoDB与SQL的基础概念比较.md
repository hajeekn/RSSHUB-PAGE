
---
title: 'MongoDB与SQL的基础概念比较'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a833052b663a4850a7e121276b3822da~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 08:15:36 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a833052b663a4850a7e121276b3822da~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">前言</h1>
<ul>
<li>在学习MongoDB数据库的操作命令前，首先需要对其中的基础概念进行一个大致的理解才能有利于后续学习。</li>
<li>鉴于SQL和NoSQL中存在着的相对关系，不妨可以将MongoDB和SQL中的概念对应起来一起理解，一方面可以在短时间内上手MongoDB，另一方面也有利于加深记忆，面试时也就不需要死记硬背概念，顺着自己的理解和思维逻辑也能讲出个大概。看了很多教程和帖子也都是以这个思路讲解的，我也将沿用这个学习模式。</li>
<li>因此，在学MongoDB前最好能够花一个星期的时间学习一下关系型数据库，理解SQL的基础概念及简单的增删改查语句，再着手MongoDB，相信会对两种数据库有更深刻的理解。后续我也会补充MySQL的复习笔记，有兴趣的可以关注一波<(￣ˇ￣)/</li>
</ul>
<h1 data-id="heading-1">1 数据库（Database）</h1>
<p>MongoDB的数据库概念和SQL基本一致，单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限。通过<code>show dbs</code>命令可以显示所有数据库。</p>
<pre><code class="copyable">> show dbs
admin        0.000GB
config       0.000GB
local        0.000GB
<span class="copy-code-btn">复制代码</span></code></pre>
<p>可以看到有三个默认的数据库，各有其特定功能，了解即可：</p>
<ul>
<li>admin： 从权限的角度来看，这是root数据库。若将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限，一些特定的服务器端命令也只能从这个数据库运行。</li>
<li>local: 这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合。</li>
<li>config: 当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。</li>
</ul>
<h1 data-id="heading-2">2 集合（Collection）</h1>
<p>集合就是MongoDB文档组，类似于关系型数据库中的表，集合没有固定的结构，可以对集合可以插入不同格式和类型的数据，但通常情况下插入集合的数据都会有一定的关联性。</p>
<h1 data-id="heading-3">3 元数据</h1>
<p>元数据，我个人把它理解为特殊的集合，但是使用了系统的命名空间：<code>dbname.system.*</code>，具体有如下几个，包括名字空间、索引、概要信息、用户和服务器信息和状态，暂时先了解即可。</p>
<pre><code class="copyable">dbname.system.namespaces
dbname.system.indexes
dbname.system.profile
dbname.system.users
dbname.local.sources
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-4">4 文档（Document）</h1>
<p>文档是一组键值对，类似Json。MongoDB 的文档不需要设置相同的字段，并且相同的字段不需要相同的数据类型，但通常情况下插入集合的数据都会有一定的关联性。这也SQL与NoSQL的重要区别之一。</p>
<h2 data-id="heading-5">4.1 举个栗子</h2>
<p>创建一个名字为<em>socialmeida</em>的数据库<code>use socialmeida</code>，然后创建一个名字为<em>douyin</em>的集合，并向其中插入4个文档：</p>
<pre><code class="copyable">db.douyin.insert(&#123;"aweme_id":"115615646865","aweme_name":"蜜雪冰城甜蜜蜜","likes":555,"follower":3&#125;)
db.douyin.insert(&#123;"aweme_id":11561564565,"aweme_name":"105度的热爱","follower":24&#125;)
db.douyin.insert(&#123;"aweme_name":"三句话让男人为我花18w","follower":"abc"&#125;)
db.douyin.insert(&#123;"aweme_name":"套马杆","likes":666&#125;)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>再用navicat看看此时的集合中的数据：</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a833052b663a4850a7e121276b3822da~tplv-k3u1fbpfcp-watermark.image" alt="屏幕截图 2021-07-10 224355.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>类Json的形式看着不舒服？没关系，先来个看得懂的形式过度一下~</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/969edc0944a149d581fb28a38876b648~tplv-k3u1fbpfcp-watermark.image" alt="屏幕截图 2021-07-10 224627.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>可以发现同一个字段中可以出现多个数据类型，SQL做得到吗？突出一个为所欲为︿(￣︶￣)︿</p>
<h2 data-id="heading-6">4.2 ObjectId</h2>
<p>如果细心观察可以发现，集合中平白无故多出来了一个_id字段，这个字段的数据类型为ObjectId，类似SQL中的唯一主键，其包含12bytes，具体含义如下：</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eb0970a8cab44989a12dd9b5bd65d0d7~tplv-k3u1fbpfcp-watermark.image" alt="屏幕截图 2021-07-10 231439.png" loading="lazy" referrerpolicy="no-referrer"></p>
<ul>
<li>前4个字节表示创建unix时间戳</li>
<li>接下来的3个字节是机器标识码</li>
<li>紧接的两个字节由进程id组成PID</li>
<li>最后三个字节是随机数</li>
</ul>
<p>其目的就是为了保证唯一性，MongoDB中存储的文档必须有一个_id字段，默认数据类型是ObjectId，由于 ObjectId中保存了创建的时间戳，所以不需要再像SQL另外创建一个时间戳字段，可以通过<code>getTimestamp</code>函数来获取文档的创建时间，我们正好来查一下刚刚输入的第一条文档是什么时候创建的：</p>
<pre><code class="copyable">> ObjectId("60e9b1b1da4c0000b9005b88").getTimestamp()
2021-07-10 14:41:53.000
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-7">5 总结</h1>
<p>最后，将上面提到的基础概念以表格的形式进行总结：</p>



































<table><thead><tr><th>基础概念</th><th>MongoDB</th><th>SQL</th><th>备注</th></tr></thead><tbody><tr><td>数据库</td><td>database</td><td>database</td><td>两者一致</td></tr><tr><td>集合/表</td><td>collection</td><td>table</td><td>MongoDB集合非结构化</td></tr><tr><td>文档/行</td><td>document</td><td>row</td><td>MongoDB文档以类Json格式存储数据</td></tr><tr><td>唯一主键</td><td>primary key</td><td>primary key</td><td>MongoDB主键_id自动生成且包含时间戳</td></tr></tbody></table></div>  
</div>
            