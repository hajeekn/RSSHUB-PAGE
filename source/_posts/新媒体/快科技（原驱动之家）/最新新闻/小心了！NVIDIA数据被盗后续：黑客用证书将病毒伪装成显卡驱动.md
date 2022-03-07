
---
title: '小心了！NVIDIA数据被盗后续：黑客用证书将病毒伪装成显卡驱动'
categories: 
 - 新媒体
 - 快科技（原驱动之家）
 - 最新新闻
headimg: 'https://img1.mydrivers.com/img/20220307/1d117b66-5c93-424c-bfa1-d548d43163a3.png'
author: 快科技（原驱动之家）
comments: false
date: Mon, 07 Mar 2022 14:08:51 GMT
thumbnail: 'https://img1.mydrivers.com/img/20220307/1d117b66-5c93-424c-bfa1-d548d43163a3.png'
---

<div>   
<p>英伟达机密数据被盗，让广大网友吃了不少瓜。</p>
<p>但从现在起，每个人都要小心了，别只顾着吃瓜了。</p>
<p>因为黑客们正在用被盗数据制造能骗过系统的病毒。</p>
<p><strong>这次泄漏的数据中，包括英伟达开发人员用于签署驱动程序和可执行文件的两个签名证书。</strong></p>
<p style="text-align: center"><img alt="NVIDIA数据被盗后续：黑客用证书将病毒伪装成显卡驱动" h="157" src="https://img1.mydrivers.com/img/20220307/1d117b66-5c93-424c-bfa1-d548d43163a3.png" style="border: black 1px solid" w="368" referrerpolicy="no-referrer"><br>
△ 黑客获得的签名证书之一</p>
<p><strong>拿到证书后，黑客就可以把恶意程序伪装成英伟达开发的软件，比如显卡驱动，从而骗过系统。</strong></p>
<p>在线查毒平台VirusTotal显示，黑客已经开始尝试用证书给远程访问木马签名了。安全人员也注意到了这一点。</p>
<p style="text-align: center"><a href="https://img1.mydrivers.com/img/20220307/ec644299-a312-43bc-8d4c-56e569fcf2be.png" target="_blank"><img alt="NVIDIA数据被盗后续：黑客用证书将病毒伪装成显卡驱动" h="809" src="https://img1.mydrivers.com/img/20220307/Sec644299-a312-43bc-8d4c-56e569fcf2be.png" style="border: black 1px solid" w="600" referrerpolicy="no-referrer"></a></p>
<p>现在黑客和安全人员正在进行着一场攻防大战。</p>
<p>黑客们将打包好的病毒上传到VirusTotal，这里几乎集成了市面上所有杀毒软件。</p>
<p>如果没被杀毒软件查出来，那就说明恶意代码比较安全，可以投放使用了。</p>
<p style="text-align: center"><a href="https://img1.mydrivers.com/img/20220307/42d434c8-07d6-4471-a791-ea88f3b1317b.png" target="_blank"><img alt="NVIDIA数据被盗后续：黑客用证书将病毒伪装成显卡驱动" h="362" src="https://img1.mydrivers.com/img/20220307/S42d434c8-07d6-4471-a791-ea88f3b1317b.png" style="border: black 1px solid" w="600" referrerpolicy="no-referrer"></a></p>
<p>除了上面所说的木马外，还有人用证书对Windows驱动程序进行签名。</p>
<p>虽然用于签名的证书已经过期，但仍然会对Windows系统造成风险。</p>
<p>因为Windows系统为了保证向下兼容性，防止系统无法启动，在某些情况下会接受2015年7月29日之前证书签发的驱动程序。</p>
<p>所以用着过期证书，病毒也一样能伪装成合法的英伟达驱动程序。</p>
<p style="text-align: center"><strong><img alt="NVIDIA数据被盗后续：黑客用证书将病毒伪装成显卡驱动" h="642" src="https://img1.mydrivers.com/img/20220307/59552808-0c99-4a0e-965d-3e2c02eb6ae2.png" style="border: black 1px solid" w="536" referrerpolicy="no-referrer"></strong></p>
<p><strong>那用户应该怎么办，才能防止中毒呢？</strong></p>
<p>微软企业和操作系统安全总监David Weston在Twitter上给出了对策：<strong>以管理员身份配置Windows Defender应用程序控制策略，这样就能控制可以加载哪些驱动程序，防止病毒被加载到系统中。</strong></p>
<p><strong>然而，使用这种方法比较复杂，并不适合电脑小白</strong>。</p>
<p>有人建议微软撤销对这两个英伟达过期证书的许可，但这又有可能导致真的英伟达驱动程序被阻止。</p>
<p>微软真的有点难办。</p>
<p>不过好消息是，虽然系统自带反病毒软件不好使，但由VirusTotal的扫描结果显示，现在的杀毒软件很多能发现伪装的病毒，事情可能并没有想象的那么糟。</p>

           
           
<p class="end"><img src="https://icons.mydrivers.com/news/end_article.png" referrerpolicy="no-referrer"></p> 
<div style="overflow: hidden;font-size:14px;">
             
          <p class="url"><span style="color:#666">责任编辑：朝晖</span><a href="javascript:;" class="jiucuo" id="leftjiucuo">文章纠错</a></p>
        </div>
        <div class="page_article" id="bnext">
 
</div>
<p class="bqian">话题标签：<a href="https://news.mydrivers.com/tag/nvidia.htm">NVIDIA</a><a href="https://news.mydrivers.com/tag/xianka.htm">显卡</a><a href="https://news.mydrivers.com/tag/bingdu.htm">病毒</a>  </p>
        
</div>
            