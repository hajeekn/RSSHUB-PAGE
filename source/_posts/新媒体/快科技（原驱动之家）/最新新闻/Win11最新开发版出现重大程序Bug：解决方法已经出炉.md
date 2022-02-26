
---
title: 'Win11最新开发版出现重大程序Bug：解决方法已经出炉'
categories: 
 - 新媒体
 - 快科技（原驱动之家）
 - 最新新闻
headimg: 'https://img1.mydrivers.com/img/20220226/s_55faa4d4a286460c81c37dd7e3cfb5a3.png'
author: 快科技（原驱动之家）
comments: false
date: Sat, 26 Feb 2022 16:56:24 GMT
thumbnail: 'https://img1.mydrivers.com/img/20220226/s_55faa4d4a286460c81c37dd7e3cfb5a3.png'
---

<div>   
<p>近日，微软面向Dev频道推送了Windows 11 Build 22563版本更新，<strong>但有用户反馈，此次更新后，出现了较为严重的程序崩溃Bug。</strong></p>
<p>据悉，在Build 22563版本中，当用户用右键单机开始按钮，或使用Win+X快捷键调出菜单时，系统的资源管理器“explorer.exe”会崩溃并重启。</p>
<p align="center"><a href="https://img1.mydrivers.com/img/20220226/55faa4d4a286460c81c37dd7e3cfb5a3.png" target="_blank"><img alt="Win11最新开发版出现重大程序Bug：解决方法已经出炉" h="337" src="https://img1.mydrivers.com/img/20220226/s_55faa4d4a286460c81c37dd7e3cfb5a3.png" style="border: black 1px solid;" w="600" referrerpolicy="no-referrer"></a></p>
<p>从反馈情况来看，该Bug有较高的触发概率，但好在已经有用户发现了解决这一Bug的方法。</p>
<p>在此次更新中，<span style="color:#ff0000;"><strong>微软为Win11加入了新的可折叠式任务栏，开启后即可解决资源管理器的崩溃问题。</strong></span></p>
<p align="center"><a href="https://img1.mydrivers.com/img/20220226/315e80957740431591cffd59e80605f7.png" target="_blank"><img alt="Win11最新开发版出现重大程序Bug：解决方法已经出炉" h="383" src="https://img1.mydrivers.com/img/20220226/s_315e80957740431591cffd59e80605f7.png" style="border: black 1px solid;" w="600" referrerpolicy="no-referrer"></a></p>
<p>用户可以在ViveTool中，通过输入<strong>“vivetool addconfig 26008830 2”</strong>命令行来开启该任务栏，而想要回到旧版则需输入“vivetool delconfig 26008830 2”。</p>
<p>目前，该Bug的具体原因尚不清楚，但有观点认为，这个能够解决Bug的新版任务栏，就是导致程序崩溃的“罪魁祸首”。</p>
<p>有网友分析后认为，此次更新后，右键单击或Win+X调出菜单时，系统会监测任务栏是否进行折叠，<strong>但旧版任务栏不存在折叠功能，这会导致空指针引用，继而导致程序崩溃。</strong></p>
<p>不过目前，这一推断尚未得到微软官方的承认或回应。</p>
<p align="center"><a href="https://img1.mydrivers.com/img/20220226/61adc3a4be774695be57a08a6549cc82.jpg" target="_blank"><img alt="Win11最新开发版出现重大程序Bug：解决方法已经出炉" h="399" src="https://img1.mydrivers.com/img/20220226/s_61adc3a4be774695be57a08a6549cc82.jpg" style="border: black 1px solid;" w="600" referrerpolicy="no-referrer"></a></p>

           
           
<p class="end"><img src="https://icons.mydrivers.com/news/end_article.png" referrerpolicy="no-referrer"></p> 
<div style="overflow: hidden;font-size:14px;">
           <p class="zhuanzai"><strong>如需转载请务必注明出处：快科技</strong></p>  
          <p class="url"><span style="color:#666">责任编辑：乃河</span><a href="javascript:;" class="jiucuo" id="leftjiucuo">文章纠错</a></p>
        </div>
        <div class="page_article" id="bnext">
 
</div>
<p class="bqian">话题标签：<a href="https://news.mydrivers.com/tag/bug.htm">Bug</a><a href="https://news.mydrivers.com/tag/windows_11.htm">Windows 11</a>  </p>
        
</div>
            