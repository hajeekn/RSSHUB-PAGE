
---
title: 'Intel打算进一步限制12代酷睿的AVX-512，接下来会从硬件上屏蔽这指令集'
categories: 
 - 新媒体
 - ZAKER
 - channel
headimg: 'https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202203/622094668e9f09225234932e_1024.jpg'
author: ZAKER
comments: false
date: Thu, 03 Mar 2022 05:23:19 GMT
thumbnail: 'https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202203/622094668e9f09225234932e_1024.jpg'
---

<div>   
<p>关于 Intel 第 12 代酷睿处理器对 AVX-512 指令集的支持情况，其实挺让人迷惑的，Alder Lake 处理器里面有 Golden Cove 和 Gracemont 两种内核，其中 Golden Cove 在硬件上是支持 AVX-512 的，虽然 Intel 官方一直否认 Alder Lake 支持 AVX-512，但开发人员指南上给出的解决方法是开启 E-Core 后 AVX-512 会被禁用，而 AVX-512 的开关则交给板厂决定怎么处理。</p><p></p><div class="img_box" id="id_imagebox_0" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_0" data-original="http://zkres2.myzaker.com/202203/622094668e9f09225234932e_1024.jpg" data-height="607" data-width="1080" src="https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202203/622094668e9f09225234932e_1024.jpg" referrerpolicy="no-referrer"></div></div>结果就是首发的时候所有板厂的 Z690 都可以通过关闭 E-Core 来开启 AVX-512，这显然让 Intel 很不满，他们在新固件中已经把 AVX-512 禁用了，实际上现在许多 B660 都无法启用 AVX-512，但对于 Z690 来说，用户可以通过刷旧的 BIOS 绕开这一限制，要彻底解决这问题，Intel 决定从硬件上下手，他们告诉 TomsHardware，他们没有在早期的 Alder Lake 在硬件上禁用 AVX-512，但 Intel 计划在未来的 Alder Lake 从硬件上彻底屏蔽 AVX-512。<p></p><p>如果从硬件上切割的话，无论板厂想用什么方法绕开固件的限制都无法再启用 AVX-512 了，如果想用 Intel 最新的处理器并启用 AVX-512 的话，你就只能选择昂贵的 Xeon，有趣的是，传闻 AMD 准备在 Zen 4 架构上加入对 AVX-512 的支持，Intel 反而把这指令从自家处理器上除去，这真是个有趣的现象。</p><div id="recommend_bottom"></div><div id="article_bottom"></div>  
</div>
            