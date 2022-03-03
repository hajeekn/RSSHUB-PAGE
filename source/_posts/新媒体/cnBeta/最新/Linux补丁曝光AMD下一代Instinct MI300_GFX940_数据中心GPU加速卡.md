
---
title: 'Linux补丁曝光AMD下一代Instinct MI300_GFX940_数据中心GPU加速卡'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/thumb/article/2022/0303/fabd9238f055cec.jpg'
author: cnBeta
comments: false
date: Thu, 03 Mar 2022 01:10:03 GMT
thumbnail: 'https://static.cnbetacdn.com/thumb/article/2022/0303/fabd9238f055cec.jpg'
---

<div>   
<strong>在最新的 Linux 补丁中，有眼尖的人们发现其包含了一个未发布的 AMD“GFX940”GPU 项目。</strong>鉴于其具有与 Aldebaran“GFX90a”GPU 相似的指令集架构（ISA），且支持矩阵融合乘加（MFMA）、全速率 FP64 和 FP32 操作、以及专门针对 CPU+GPU 内存空间集成的功能特性，我们推测它很可能用于 AMD 下一代 Instinct MI300 数据中心 GPU 加速卡。<br>
 <p><a href="https://static.cnbetacdn.com/article/2022/0303/fabd9238f055cec.jpg" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2022/0303/fabd9238f055cec.jpg" alt="1.jpg" referrerpolicy="no-referrer"></a></p><p><a href="https://www.coelacanth-dream.com/posts/2022/03/01/llvm-gfx940/" target="_self">Coelacanth-Dream</a> 指出，尽管 GPU ISA 相似，但与 Aldebaran“CDNA 2”GPU 相比，GFX940 仍存在一些差异。</p><p>此前有传闻称，<a data-link="1" href="https://c.duomai.com/track.php?site_id=242986&euid=&t=https://amd-cpu.jd.com/" target="_blank">AMD</a>Instinct MI300 将采用基于全新的 CDNA 3 架构的 4-GCD 设计。</p><p><img src="https://static.cnbetacdn.com/article/2022/0303/fc8fd0cd43a46ba.png" alt="2.png" referrerpolicy="no-referrer"></p><p>而即将面世的 Instinct MI200，早期消息称每个芯片配备了 128 组计算单元（CU）。但自上周传出以来，新消息已改为 110 组计算单元（总计 220 CU / 14080 核心）。</p><p>若将确切的数字 ×4（Instinct MI300 上的 GCD 数量），可算出 440 CU / 疯狂的 28160 核心。</p><p><img src="https://static.cnbetacdn.com/article/2022/0303/32e3f7192625c55.png" alt="34.png" referrerpolicy="no-referrer"></p><p>Komachi 发现，近日更新的 AMD ROCm 开发工具证实了最初 4 组 MCM 的多芯片 GPU 设计，但以及仅针对“Aldebaran”SKU 。</p><p>至于 Instinct 加速卡，预计至少有 4 组 CDNA 2，且相关 SKU 的唯一设备 ID 如下所示：</p><blockquote><p>● 0x7408</p><p>● 0x740C</p><p>● 0x740F</p><p>● 0x7410</p></blockquote><p><a href="https://static.cnbetacdn.com/article/2022/0303/53351836e6e8b12.png" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2022/0303/53351836e6e8b12.png" alt="5.png" referrerpolicy="no-referrer"></a></p><p>结合最新爆料，AMD 应该不会在从 CDNA 2 迁移至 CDNA 3 时不包含任何更改。预计 CDNA 3 会用上一个修订后的新架构，而不是 Arcturus 或 Aldebaran 的又一个 Vega 衍生品。</p><p>最后，新 GPU 架构有望采纳类似于新 RDNA 3 GPU 的新 WGP 工作组 / SE 渲染引擎设计，或者为 HPC 高性能计算市场提供量身定制的全新设计。不过可以肯定的是，这些四 MCM GPU 不会很快出现在我们面前。</p>   
</div>
            