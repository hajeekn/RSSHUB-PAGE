
---
title: '西数升级固件解决SSD掉速 PCIe 4.0黑盘满血回归'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/article/2021/0712/5d9026584b53d52.jpg'
author: cnBeta
comments: false
date: Mon, 12 Jul 2021 10:32:50 GMT
thumbnail: 'https://static.cnbetacdn.com/article/2021/0712/5d9026584b53d52.jpg'
---

<div>   
SN850是西数首款消费级PCIe 4.0硬盘，性能很猛，读取速度可以超过7GB/s，写入也可达到5GB/s。然而前不久SN850出现了其他的降速问题，现在官方发布了新固件，性能又满血回归了。<br>
 <p>SN850硬盘的掉速问题有些奇怪，无论是使用哪家厂商或者哪款主板，SN850只要不是连接在锐龙处理器的PCIe 4.0通道中，而是连接到芯片组（比如X570）的PCIe 4.0通道，写入性能都会大幅降低。</p><p>从技术来说，南桥的PCIe 4.0通道比CPU直连的肯定会有延迟，性能降低是正常的，但是SN850的问题在于降幅太大了，<strong>用别家的<a data-link="1" href="https://c.duomai.com/track.php?site_id=242986&euid=&t=https://list.jd.com/list.html?cat=670,677,11303" target="_blank">SSD</a>测试的话性能损失在10%左右，SN850损失可达40%以上，写入速度从5GB/s左右降至3GB/s，远高于其他SSD硬盘。</strong></p><p>对于这个意外，西数官方之前确认了会修复，<strong>表示问题跟最大有效负载MPS设置为128B有关，</strong>后面会取消这个设置。</p><p><img src="https://static.cnbetacdn.com/article/2021/0712/5d9026584b53d52.jpg" referrerpolicy="no-referrer"><br>旧版固件性能</p><p><img src="https://static.cnbetacdn.com/article/2021/0712/fdfdad75e3ff798.jpg" referrerpolicy="no-referrer"><br>新版固件性能</p><p>西数公告的固件是在7月12日发布，不过已经有网友提前升级了，对比旧版固件613000WD，新版固件613200WD中的性能测试中，<strong>写入速度已经从3GB/s以内恢复到5GB/s以上了，性能重新满血了。</strong></p><p><img src="https://static.cnbetacdn.com/article/2021/0712/3b44864c11d97fa.png" referrerpolicy="no-referrer"></p>   
</div>
            