
---
title: '传英伟达Hopper GH100 GPU采用5nm工艺 晶体管超1400亿'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/thumb/article/2022/0208/42efc58ce280627.png'
author: cnBeta
comments: false
date: Tue, 08 Feb 2022 01:11:09 GMT
thumbnail: 'https://static.cnbetacdn.com/thumb/article/2022/0208/42efc58ce280627.png'
---

<div>   
几周前，有传闻称用于下一代数据中心的英伟达 Hopper GH100 芯片将采用 5nm 工艺、且尺寸接近 900 m㎡，使之成为有史以来最大的 GPU 。<strong>近日，ChipHell 上又冒出了新的传闻，指出 Hopper GH100 可能具有超过 1400 亿个晶体管。</strong><br>
 <p><a href="https://static.cnbetacdn.com/article/2022/0208/42efc58ce280627.png" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2022/0208/42efc58ce280627.png" alt="1.png" referrerpolicy="no-referrer"></a></p><p style="text-align: center;">（图 via <a href="https://wccftech.com/nvidia-hopper-gh100-gpu-140-billion-transistors-massive-5nm-package-rumor/" target="_self">WCCFTech</a>）</p><p>作为参考，当前的旗舰数据中心芯片 —— 英伟达自家的 A100（基于 Ampere GA100）和竞争对手 <a data-link="1" href="https://c.duomai.com/track.php?site_id=242986&euid=&t=https://amd-cpu.jd.com/" target="_blank">AMD</a> 家的 Instinct MI200 系列（基于 Aldebaran GPU）—— 分别为 542 / 582 亿个晶体管，而 Hopper GH100 是它们的 2.5 倍左右</p><p>换算成密度的话，Ampere A100 约为 6560 万个晶体管 / 平方毫米，Aldebaran GPU（基于推测的 790 m㎡ 芯片尺寸）约为 7360 万个晶体管 / 平方毫米。</p><p><a href="https://static.cnbetacdn.com/article/2022/0208/fd17bb009227778.png" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2022/0208/fd17bb009227778.png" alt="2.png" referrerpolicy="no-referrer"></a></p><p>而 Hopper GH100 有望在 5nm 工艺加持下，轻松超越 1.5 亿个晶体管 / 平方毫米（翻一倍多）。遗憾的是，这些都只是传闻中的数据，且仅适用于单芯片封装的版本。</p><p>另有消息称，英伟达会在这一代 GPU 产品线中尝试多芯片封装（MCM），但它可能以完全独立的 SKU 出现（比如 GH102 GPU）。</p><p><img src="https://static.cnbetacdn.com/article/2022/0208/4ff3c6eefcc401d.png" alt="3.png" referrerpolicy="no-referrer"></p><p>参考之前的传闻，英伟达为 GH100 选用了台积电 5nm 工艺、辅以俩 GPU 模组，总计为 288 个 SM 单元（每组 CUDA 数暂不得而知）。</p><p>若沿用每组 SM / 64 核心的规格，那总计 CUDA 数为 18432 个（约为 GA100 满血核心的 2.25 倍），并且塞下更多的 FP64 / FP16 和 Tensor Core 。</p><p><img src="https://static.cnbetacdn.com/article/2022/0208/79e7ccccb5a1260.png" alt="4.png" referrerpolicy="no-referrer"></p><p style="text-align: center;">截图（来自：<a href="https://www.chiphell.com/thread-2390985-1-1.html" target="_self">ChipHell</a>）</p><p>最终配置可能在每个 GPU 模块上 144 组 SM 单元中的 134 个，但若未启用 GPU Sparsity，英伟达又不大可能达成与 AMD Instinct MI200 竞品相当的 FP32 / FP64 数据。</p><p>不过英伟达可能藏了一手，那就是基于 COPA 的 GPU 实现。其中一款适用于高性能计算（HPC）、另一款则主打深度学习（DL）细分市场。</p><p>显存方面，Hopper GPU 或具有高达 960 / 1920 MB 的末级缓存（LLC）、233 GB 的 HBM2e 显存、以及高达 6.3 TB/s 的带宽。</p><div class="article-relation"><p><strong>相关文章:</strong></p><p><a href="https://www.cnbeta.com/articles/tech/1231577.htm" target="_blank">英伟达新一代GH100 Hopper GPU芯片面积或达到创纪录的1000m㎡</a></p></div>   
</div>
            