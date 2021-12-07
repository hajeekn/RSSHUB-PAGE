
---
title: 'Linux 5.17将更好地兼容苹果M1处理器'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/article/2021/1207/d06ae41577c1e0e.jpg'
author: cnBeta
comments: false
date: Tue, 07 Dec 2021 10:19:54 GMT
thumbnail: 'https://static.cnbetacdn.com/article/2021/1207/d06ae41577c1e0e.jpg'
---

<div>   
在Linux下支持苹果M1 SoC的适配工作仍在继续，随着明年v5.17内核的推出，料将会有更多的新增功能出现。在Linux
5.17的驱动合并过程中，有人发现了用于控制电源状态的苹果PMGR驱动。苹果公司在其SoC上的PMGR模块对SoC设备进行了高级别的电源状态控制。<br>
 <p>目前并不是所有的功能都被支持，但对于Linux上的<a data-link="1" href="https://apple.pvxt.net/c/1251234/435400/7639?u=https%3A%2F%2Fwww.apple.com%2Fcn%2Fmusic%2F" target="_blank">苹果</a>M1芯片的电源管理来说，这是重要的一步。</p><p><img src="https://static.cnbetacdn.com/article/2021/1207/d06ae41577c1e0e.jpg" title alt="image.jpg" referrerpolicy="no-referrer"></p><p>在电源管理方面同样重要的是为以前主要的苹果PCIe驱动启用时钟门控。PCI Express的时钟门控对于电源的原因也很重要，这些面向PCI的变化也在Linux 5.17中排队。</p><p>今天早上，内核团队还公布了Linux 5.17的Apple SoC DeviceTree更新。这些工作包括Wi-Fi MAC地址的DT处理、新PMGR驱动的绑定、i2c和cd321x节点以及其他工作。</p><p>这批最新的Linux内核的Apple Silicon补丁是由Hector Martin和Asahi Linux项目提交的。对于那些对在Linux上运行基于ARM的苹果Mac感兴趣的人来说，这项工作一直在持续向前推进，特别是在图形方面是否会有进展是最值得关注的。</p><p>了解更多：</p><p><a href="https://lore.kernel.org/lkml/049f4de9-51be-7be4-1f9a-a59756af88d7@marcan.st/" _src="https://lore.kernel.org/lkml/049f4de9-51be-7be4-1f9a-a59756af88d7@marcan.st/" target="_blank">https://lore.kernel.org/lkml/<span class="__cf_email__" data-cfemail="68585c510e5c0c0d51455d590a0d455f0a0d5c45590e510945095d515f5d5e090e50500c5f2805091a0b0906461b1c">[email protected]</span>/</a><br></p><p><a href="https://git.kernel.org/pub/scm/linux/kernel/git/helgaas/pci.git/commit/?h=next&id=754bb7ad29566b2789cafb6b378b788266d1f131" _src="https://git.kernel.org/pub/scm/linux/kernel/git/helgaas/pci.git/commit/?h=next&id=754bb7ad29566b2789cafb6b378b788266d1f131" target="_blank">https://git.kernel.org/pub/scm/linux/kernel/git/helgaas/pci.git/commit/?h=next&id=754bb7ad29566b2789cafb6b378b788266d1f131</a></p><p><a href="https://lore.kernel.org/lkml/e18b476c-7b1f-de73-53a2-0e21fb5cd283@marcan.st/" _src="https://lore.kernel.org/lkml/e18b476c-7b1f-de73-53a2-0e21fb5cd283@marcan.st/" target="_blank">https://lore.kernel.org/lkml/<span class="__cf_email__" data-cfemail="95f0a4adf7a1a2a3f6b8a2f7a4f3b8f1f0a2a6b8a0a6f4a7b8a5f0a7a4f3f7a0f6f1a7ada6d5f8f4e7f6f4fbbbe6e1">[email protected]</span>/</a><br></p>   
</div>
            