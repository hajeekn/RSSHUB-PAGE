
---
title: 'MaxCompute非事务表如何更新数据'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=9846'
author: 掘金
comments: false
date: Thu, 15 Jul 2021 18:08:38 GMT
thumbnail: 'https://picsum.photos/400/300?random=9846'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p><strong>简介：</strong> 本文主要讲解如何通过insert overwrite更新数据</p>
<h1 data-id="heading-0">背景</h1>
<p>对于大数据中的大多数存储格式，支持随机更新非常复杂。它需要扫描大型文件，MaxCompute推出了最新的功能Transactional表可以支持update和delete语句，但是update和delete功能不适用于高频更新、删除数据或实时写入目标表场景，同时对于非Transactional表无法执行update和delete。本文主要讲解如何通过insert overwrite更新数据。</p>
<h1 data-id="heading-1">1.建表插入数据</h1>
<pre><code class="copyable">create table update_table(ID int,
 tranValue string,
 last_update_user string) PARTITIONED by(dt STRING ) LIFECYCLE 1;
INSERT INTO update_table PARTITION (dt="20210510") VALUES
(1, 'value_01', 'creation'),
(2, 'value_02', 'creation'),
(3, 'value_03', 'creation'),
(4, 'value_04', 'creation'),
(5, 'value_05', 'creation'),
(6, 'value_06', 'creation'),
(7, 'value_07', 'creation'),
(8, 'value_08', 'creation'),
(9, 'value_09', 'creation'),
(10, 'value_10','creation');
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-2">2.更新一条数据</h1>
<p>当id是1的时候更新成value_011</p>
<pre><code class="copyable">--更新一条数据
INSERT OVERWRITE TABLE update_table PARTITION( dt)
SELECT  id
        ,CASE    WHEN id=1 THEN "value_011" 
                 ELSE TranValue 
         END TranValue
        ,last_update_user
        ,dt
FROM    update_table
WHERE   dt = "20210510"
;
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-3">3.更新多条数据</h1>
<p>根据增量表更新,首先创建增量表插入数据</p>
<pre><code class="copyable">create table update_table_inc(ID int,
 TranValue string,
 last_update_user string) LIFECYCLE 1;
INSERT INTO update_table_inc VALUES 
(5, 'value_11', 'creation'),
(6, NULL, '20170410'),
(7, 'value22', '20170413');
<span class="copy-code-btn">复制代码</span></code></pre>
<p>id是5和7更新TranValue，由于6的TranValue是null不更新</p>
<pre><code class="copyable">INSERT OVERWRITE TABLE update_table PARTITION( dt)
SELECT  a.id
        ,CASE    WHEN a.id=b.id  and b.TranValue is not null THEN b.TranValue 
                 ELSE a.TranValue 
         END TranValue
        ,CASE    WHEN a.id=b.id and b.TranValue is not null THEN b.last_update_user 
                 ELSE a.last_update_user 
         END last_update_user
         ,dt
FROM    update_table a
LEFT JOIN update_table_inc b
ON      a.id = b.id
WHERE   a.dt = "20210510"
;
<span class="copy-code-btn">复制代码</span></code></pre>
<h1 data-id="heading-4">4.删除数据</h1>
<pre><code class="copyable">--删除数据

INSERT OVERWRITE TABLE update_table PARTITION( dt)
SELECT *
       
FROM    update_table
WHERE   dt = "20210510" and id !=4
;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><a href="https://link.juejin.cn/?target=http%3A%2F%2Fclick.aliyun.com%2Fm%2F1000284196%2F" target="_blank" rel="nofollow noopener noreferrer" title="http://click.aliyun.com/m/1000284196/" ref="nofollow noopener noreferrer">原文链接</a></p>
<p>本文为阿里云原创内容，未经允许不得转载。</p></div>  
</div>
            