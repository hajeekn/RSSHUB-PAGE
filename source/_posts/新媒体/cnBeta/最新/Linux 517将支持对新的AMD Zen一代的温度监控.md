
---
title: 'Linux 5.17将支持对新的AMD Zen一代的温度监控'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/thumb/article/2021/1117/a746ff12470117b.jpg'
author: cnBeta
comments: false
date: Wed, 17 Nov 2021 12:26:34 GMT
thumbnail: 'https://static.cnbetacdn.com/thumb/article/2021/1117/a746ff12470117b.jpg'
---

<div>   
<strong>明年的Linux 5.17内核将支持对"新一代"AMD
Zen处理器的温度监控。虽然AMD在Linux下支持Zen处理器的CPU温度报告方面经常迟到，但很高兴看到他们在下一次发布之前走在前面。</strong>即使在只需要将新的ID添加到k10temp驱动的情况下，不幸的是，内核团队经常在发布新版后才添加这些ID。<br>
 <p><a href="https://static.cnbetacdn.com/article/2021/1117/a746ff12470117b.jpg" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2021/1117/a746ff12470117b.jpg" title alt="image.jpg" referrerpolicy="no-referrer"></a></p><p>最近，<a data-link="1" href="https://c.duomai.com/track.php?site_id=242986&euid=&t=https://amd-cpu.jd.com/" target="_blank">AMD</a>抢先一步，在推出Linux 5.15之前，增加了Yellow Carp（Rembrandt）温度监控。现在，在hwmon-next中为Linux 5.17排队的补丁通过增加对新一代Family 19h处理器的支持继续朝这个方向发展。</p><p>这个补丁添加了Family 19h型号10h-1Fh和A0h-AFh的PCI ID，并指出它是为"新一代"设计的。该补丁使基于k10temp的CPU温度监测对那些新的AMD Family 19h CPU型号起作用。新一代产品使用首次出现在Yellow Carp的0x300 CCD偏移，用于读取热信息。</p><p>这些新的Family 19h型号很有可能是为Zen 4设计的，或者我们会在适当的时候发现，但现在这就是关于这个问题的所有报告，无论如何，看到这些基本的补充在发布前被做出来是件好事。这些补丁在硬件监控子系统的"-next"区域，直到Linux 5.17周期在新的一年开始时启动，该内核将在3月底达到稳定。</p>   
</div>
            