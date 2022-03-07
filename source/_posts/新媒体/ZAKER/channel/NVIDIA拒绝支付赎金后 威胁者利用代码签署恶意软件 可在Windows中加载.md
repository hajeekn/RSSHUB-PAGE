
---
title: 'NVIDIA拒绝支付赎金后 威胁者利用代码签署恶意软件 可在Windows中加载'
categories: 
 - 新媒体
 - ZAKER
 - channel
headimg: 'https://cors.zfour.workers.dev/?http://zkres1.myzaker.com/202203/62256ff3b15ec046d2678e8f_1024.jpg'
author: ZAKER
comments: false
date: Sun, 06 Mar 2022 20:42:00 GMT
thumbnail: 'https://cors.zfour.workers.dev/?http://zkres1.myzaker.com/202203/62256ff3b15ec046d2678e8f_1024.jpg'
---

<div>   
<p><strong>利用窃取过来的 NVIDIA 代码，威胁者利用签名证书来签署恶意软件，使其看起来值得信赖，并允许在 Windows 中加载恶意驱动程序。</strong></p><p>本周，NVIDIA 公司证实，他们遭受了一次网络攻击，使威胁者得以窃取员工的证书和专有数据。</p><p></p><div class="img_box" id="id_imagebox_0" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_0" data-original="http://zkres1.myzaker.com/202203/62256ff3b15ec046d2678e8f_1024.jpg" data-height="819" data-width="1366" src="https://cors.zfour.workers.dev/?http://zkres1.myzaker.com/202203/62256ff3b15ec046d2678e8f_1024.jpg" referrerpolicy="no-referrer"></div></div>对本次泄露事件负责的勒索集团 Lapsus$ 表示，他们已经窃取了 1TB 的数据，并在 NVIDIA 拒绝与他们谈判后开始在网上泄露这些数据。泄漏的数据包括 2 份被盗的代码签名证书，这些证书是 NVIDIA 开发人员用来签署其驱动程序和可执行文件的。<p></p><p></p><div class="img_box" id="id_imagebox_1" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_1" data-original="http://zkres2.myzaker.com/202203/62256ff3b15ec046d2678e90_1024.jpg" data-height="640" data-width="567" src="https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202203/62256ff3b15ec046d2678e90_1024.jpg" referrerpolicy="no-referrer"></div></div>代码签名证书允许开发人员对可执行文件和驱动程序进行数字签名，以便 Windows 和终端用户能够验证文件的所有者，以及它们是否被第三方篡改过。为了提高 Windows 的安全性，微软还要求内核模式的驱动程序在操作系统加载之前必须进行代码签名。<p></p><p></p><div class="img_box" id="id_imagebox_2" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_2" data-original="http://zkres1.myzaker.com/202203/62256ff3b15ec046d2678e91_1024.jpg" data-height="884" data-width="655" src="https://cors.zfour.workers.dev/?http://zkres1.myzaker.com/202203/62256ff3b15ec046d2678e91_1024.jpg" referrerpolicy="no-referrer"></div></div><div class="img_box" id="id_imagebox_3" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_3" data-original="http://zkres2.myzaker.com/202203/62256ff3b15ec046d2678e92_1024.jpg" data-height="642" data-width="536" src="https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202203/62256ff3b15ec046d2678e92_1024.jpg" referrerpolicy="no-referrer"></div></div>在 Lapsus$ 泄露了英伟达的代码签名证书后，安全研究人员很快发现，这些证书被用来签署恶意软件和威胁者使用的其他工具。根据上传到 VirusTotal 恶意软件扫描服务的样本，被盗的证书被用来签署各种恶意软件和黑客工具，如 Cobalt Strike 信标、Mimikatz、后门和远程访问木马。<p></p><p>例如，一个威胁者用该证书签署了一个 Quasar 远程访问特洛伊木马 [ VirusTotal ] ，而另一个人用该证书签署了一个 Windows 驱动程序 [ VirusTotal ] 。虽然这 2 个被盗的英伟达证书都已过期，但 Windows 仍然允许在操作系统中加载用这些证书签名的驱动程序。</p><div id="recommend_bottom"></div><div id="article_bottom"></div>  
</div>
            