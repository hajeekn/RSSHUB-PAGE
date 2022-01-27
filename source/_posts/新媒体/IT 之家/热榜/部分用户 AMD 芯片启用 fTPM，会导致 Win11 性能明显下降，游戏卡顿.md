
---
title: '部分用户 AMD 芯片启用 fTPM，会导致 Win11 性能明显下降，游戏卡顿'
categories: 
 - 新媒体
 - IT 之家
 - 热榜
headimg: 'https://img.ithome.com/newsuploadfiles/2022/1/cb001304-8f23-4356-81f7-2a24f50055fd.jpg@s_2,w_820,h_462'
author: IT 之家
comments: false
date: Wed, 26 Jan 2022 04:25:40 GMT
thumbnail: 'https://img.ithome.com/newsuploadfiles/2022/1/cb001304-8f23-4356-81f7-2a24f50055fd.jpg@s_2,w_820,h_462'
---

<div>   
<p data-vmark="c5ba"><a class="s_tag" href="https://www.ithome.com/" target="_blank">IT之家</a> 1 月 26 日消息，在 <a class="s_tag" href="https://win11.ithome.com/" target="_blank">Windows 11</a> 中，微软不仅放弃了对许多具备一定性能的处理器的支持，而且还将操作系统限制在具有 TPM 2.0（可信平台模块 2.0）的硬件上。</p><p data-vmark="22ad">与有争议的处理器要求不同，TPM 2.0 授权对大多数用户来说其实不是什么大事，因为绝大多数现代设备都有这个安全功能。</p><p data-vmark="bcdd">在 AMD 系统上，TPM 也被称为“fTPM”，这是一种在系统固件中实现的安全模块，而不是专用芯片。fTPM 在 AMD 系统上很容易启用，但对于某些配置来说，启用这一功能似乎会导致性能问题。</p><p data-vmark="9a08" style="text-align: center;"><img src="https://img.ithome.com/newsuploadfiles/2022/1/cb001304-8f23-4356-81f7-2a24f50055fd.jpg@s_2,w_820,h_462" w="1210" h="681" alt="AMD 芯片启用 fTPM" title="部分用户 AMD 芯片启用 fTPM，会导致 Win11 性能明显下降，游戏卡顿" srcset="https://img.ithome.com/newsuploadfiles/2022/1/cb001304-8f23-4356-81f7-2a24f50055fd.jpg 2x" width="1210" height="462" referrerpolicy="no-referrer"></p><p data-vmark="990a">TPM 的实现很直接，大量的英特尔用户正在使用它，但 AMD 的实现有一些问题，最明显的是音频故障和游戏帧率卡顿的问题。</p><p data-vmark="60a0">有趣的是，这个问题似乎是由于 AMD 的 fTPM 和 Windows 之间的兼容性问题，而不是新操作系统中的错误导致的。</p><h3 data-vmark="7cc3">Windows 11 fTPM 错误导致卡顿</h3><p data-vmark="5ad4">正如一些用户调查并分析得出，启用 fTPM 可能会削弱设备的性能，导致你在 <a class="s_tag" href="https://win10.ithome.com/" target="_blank">Windows 10</a> 或 Windows 11 上玩游戏时出现卡顿。</p><p data-vmark="3081">这个问题已经被用户记录在反馈中心、Reddit 和其他论坛上。</p><p data-vmark="17dd">“我也有同样的问题，我运行的是 Ryzen 5 1600AF，有时在随机的时间内出现随机的停顿和音频噼啪声，”一位用户在 Reddit 帖子中指出。</p><p data-vmark="e327">“我可以确认我在这里也有同样的问题--Ryzen 3900X 在 MSI MEG X570 ACE 上使用 fTPM。像其他人提到的那样，除非我有音乐播放，否则我一般不会注意到卡顿的情况。这与其他人描述的情况相同。我使用的是最新的主板 BIOS，驱动程序等都是完全最新的。Windows 11 Pro 完全是最新的发布版本。”另一位用户说。</p><p data-vmark="d27f">这个错误并不影响所有从 Windows 10 升级到 Windows 11 的电脑，似乎出现在某些特定设备上。根据报告，这个问题不会让你的设备无法使用，因为这些卡顿只持续几秒钟，而且是随机发生的。</p><h3 data-vmark="aa4d">如何解决 Windows 11 上由 fTPM 引起的卡顿问题</h3><p data-vmark="c4be">建议卸载 Windows 11 并关闭 Windows 10 上的 fTPM，看看是否能解决卡顿问题。虽然你也可以在 Windows 11 上关闭 fTPM，但它可能会产生不利影响，因为一些游戏如拳头《Valorant》不会在没有 TPM 的新操作系统上运行。</p><p data-vmark="ca81">还有一种可能性是，Windows 11 中的一个错误 Bug 导致了该问题，所以如果你在玩游戏时出现卡顿，你应该考虑重新安装 Windows 10，或者等待微软和 AMD 回应，并且推出更新的修复补丁。</p>
          
</div>
            