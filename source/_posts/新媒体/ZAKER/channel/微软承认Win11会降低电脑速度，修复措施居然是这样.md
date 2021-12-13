
---
title: '微软承认Win11会降低电脑速度，修复措施居然是这样'
categories: 
 - 新媒体
 - ZAKER
 - channel
headimg: 'https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202112/61b718bb8e9f0912a478dd24_1024.jpg'
author: ZAKER
comments: false
date: Mon, 13 Dec 2021 03:24:51 GMT
thumbnail: 'https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202112/61b718bb8e9f0912a478dd24_1024.jpg'
---

<div>   
<p>在 12 月 10 日的时候，微软公开承认，Win 11 会降低 PC 的速度。究其原因是因为 Win 11 上存在一个 Bug，其影响了所有磁盘（NVMe、SSD、硬盘）的性能，即当一个名为 "NTFS USN 日志 " 的功能被启用时，Windows 11 的性能问题就会发生。不过微软表示，在 Win11 上，该功能默认只在 C: 磁盘上启用，其余分区或驱动器不受影响。按照目前用户的反馈看，在大多数情况下，Windows 11 的速度差异是不太明显的。但是当系统磁盘被用于安装大型应用程序或者传输大型文件的时候，就会明显感受到性能问题。在极少数情况下，Windows 11 可能会降低驱动器的写入速度，最高可达 45%。因此，Windows 11 将无法即时加载应用程序或打开文件夹。</p><p></p><div class="img_box" id="id_imagebox_0" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_0" data-original="http://zkres2.myzaker.com/202112/61b718bb8e9f0912a478dd24_1024.jpg" data-height="434" data-width="712" src="https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202112/61b718bb8e9f0912a478dd24_1024.jpg" referrerpolicy="no-referrer"></div></div>其实上述问题在今年 8 月份就被发现，但是微软一直对它迟迟不动，随着问题愈演愈烈，现在官方终于表示，将会在近期以补丁形式对性能进行修复，预计最快是本月中旬。<p></p><p>让人没想到的是，微软已经悄悄推送了新的更新，也确实解决了上述问题，不过解决方式太过于无语了。微软悄然更新了 Windows 11 Build 22000.348（KB5007262）累积更新的日志，现在引入了 "NVME、SSD、hard disk" 等术语，而之前更新日志提到的是 "NTFS"。此前的更新日志写道：" 修复了当你启用更新序列号（USN）日志时影响 NTFS 的问题。NTFS 每次执行写操作时都会执行不必要的操作，这影响了 I/O 性能。"</p><p>现在更新的日志写道：" 修复了一个问题，即每次发生写操作时执行不必要的操作，会影响 Windows 11 上所有磁盘（NVMe、SSD、硬盘）的性能。这个问题只在启用 NTFS USN 日 志时发生。注意，USN 日志总是在 C：磁盘上启用。" 那么微软真的解决问题了吗，并没有。科技媒体 NeoWin 在 WD SN520 测试了推荐版本 22000.348，但问题依然存在。</p><p><strong>· END<strong>·</strong></strong></p><div id="recommend_bottom"></div><div id="article_bottom"></div>  
</div>
            