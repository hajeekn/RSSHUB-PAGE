
---
title: '英特尔和Arm的CPU再被发现存在重大安全漏洞Spectre-HBB'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/thumb/article/2022/0309/c5b137329c3cf03.jpg'
author: cnBeta
comments: false
date: Wed, 09 Mar 2022 13:38:44 GMT
thumbnail: 'https://static.cnbetacdn.com/thumb/article/2022/0309/c5b137329c3cf03.jpg'
---

<div>   
BHI是一种影响大多数英特尔和Arm CPU的新型投机执行漏洞，它攻击分支全局历史而不是分支目标预测。不幸的是，这些公司以前对Spectre
V2的缓解措施也无法保护BHI的威胁，尽管AMD处理器大多是免疫的。消息传出后，供应商应该很快就会发布安全补丁，而最新得Linux内核已经打了补丁。<br>
  <p><a href="https://static.cnbetacdn.com/article/2022/0309/c5b137329c3cf03.jpg" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2022/0309/c5b137329c3cf03.jpg" title alt="maxresdefault.jpg" referrerpolicy="no-referrer"></a></p><p>VUSec安全研究小组和英特尔周二联合披露了一个新的Spectre类投机执行漏洞，称为分支历史注入（BHI）或Spectre-HBB。</p><p>BHI是对Spectre V2（或Spectre-BTI）类型攻击的概念重新实现的证明。它影响到任何同样易受Spectre V2攻击的CPU，即使Spectre V2的缓解措施已经实施；它可以绕过英特尔的eIBRS和Arm的CSV2缓解措施。这些缓解措施可以保护分支目标注入，而新的漏洞允许攻击者在全局分支历史中注入预测器条目。BHI可以用来泄露任意的内核内存，这意味着像密码这样的敏感信息可以被泄露。</p><p>VUSec对此的解释如下："BHI本质上是Spectre v2的扩展，我们利用全局历史来重新引入跨权限BTI的利用。因此，攻击者的基本原理仍然是Spectre v2，但通过跨权限边界注入历史（BHI），我们可以利用部署新的硬件内缓解措施的系统（即英特尔eIBRS和Arm CSV2）。"</p><p>该漏洞影响到自Haswell以来推出的任何英特尔CPU，包括Ice Lake-SP和Alder Lake。受影响的Arm CPU包括Cortex A15/A57/A65/A72/A73/A75/A76/A77/A78/X1/X2/A710、Neoverse N2/N1/V1和博通Brahma B15。</p><p>Arm的CVE ID是CVE-2022-23960，Intel使用的是CVE-2022-0001和CVE-2022-0002的ID。两家公司都发布了有关其受影响CPU的更多细节：</p><p><a href="https://www.intel.com/content/www/us/en/developer/topic-technology/software-security-guidance/processors-affected-consolidated-product-cpu-model.html" _src="https://www.intel.com/content/www/us/en/developer/topic-technology/software-security-guidance/processors-affected-consolidated-product-cpu-model.html" target="_blank">https://www.intel.com/content/www/us/en/developer/topic-technology/software-security-guidance/processors-affected-consolidated-product-cpu-model.html</a><br></p><p><a href="https://developer.arm.com/support/arm-security-updates/speculative-processor-vulnerability/spectre-bhb" _src="https://developer.arm.com/support/arm-security-updates/speculative-processor-vulnerability/spectre-bhb" target="_blank">https://developer.arm.com/support/arm-security-updates/speculative-processor-vulnerability/spectre-bhb</a><br></p><p>英特尔发布了关于BHI漏洞的以下声明。"正如研究人员所证明的那样，这种攻击以前在大多数Linux发行版中都被默认缓解了。Linux社区已经从Linux内核5.16版本开始实施英特尔的建议，并正在将缓解措施回传到Linux内核的早期版本。英特尔发布了技术文件，描述了那些使用非默认配置的人的进一步缓解方案，以及为什么LFENCE; JMP缓解措施在所有情况下都是不够的"。</p><p>AMD CPU似乎对BHI有免疫力。据Phoronix称，默认使用Retpolines进行Spectre V2缓解的AMD处理器应该是安全的。</p><p>供应商的安全补丁应该很快就会发布。除了安装它们之外，研究人员建议禁用无特权的eBPF支持作为额外的预防措施。Linux已经将安全更新合并到其主线内核中。这些安全缓解措施是否会影响性能尚不清楚。</p><p><strong>VUSec的漏洞的源代码可以在这里找到：</strong></p><p><a href="https://github.com/vusec/bhi-spectre-bhb" _src="https://github.com/vusec/bhi-spectre-bhb" target="_blank">https://github.com/vusec/bhi-spectre-bhb</a><br></p>   
</div>
            