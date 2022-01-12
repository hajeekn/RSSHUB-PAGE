
---
title: '微软发布补丁 修复HTTP协议堆栈远程执行代码漏洞'
categories: 
 - 新媒体
 - cnBeta
 - 最新
headimg: 'https://static.cnbetacdn.com/thumb/article/2022/0112/3aa1b0c858e0894.png'
author: cnBeta
comments: false
date: Wed, 12 Jan 2022 03:22:58 GMT
thumbnail: 'https://static.cnbetacdn.com/thumb/article/2022/0112/3aa1b0c858e0894.png'
---

<div>   
<strong>针对近期曝光的 Windows 桌面和服务器高危漏洞，微软在本月的补丁星期二活动日中发布了一个补丁。</strong>该漏洞存在于 HTTP 协议栈（HTTP.sys）中，只需向利用 HTTP 协议栈（http.sys）处理数据包的目标服务器发送一个特制的数据包就可以被利用。攻击者甚至不需要经过认证。<br>
 <p style="text-align:center"><a href="https://static.cnbetacdn.com/article/2022/0112/3aa1b0c858e0894.png" target="_blank"><img src="https://static.cnbetacdn.com/thumb/article/2022/0112/3aa1b0c858e0894.png" alt="QQ截图20220112111723.png" referrerpolicy="no-referrer"></a></p><p style="text-align: left;">幸运的是，目前还没有 <a href="https://msrc.microsoft.com/update-guide/vulnerability/CVE-2022-21907" target="_blank">CVE-2022-21907</a> 的概念验证代码被发布，而且也没有证据表明该漏洞已经被黑客利用。在 <a data-link="1" href="https://microsoft.pvxt.net/x9Vg1" target="_blank">Windows</a> Server 2019 和 Windows 10 Version 1809 版本中，包含该漏洞的 HTTP Trailer Support 功能默认不激活。必须配置以下注册表键，以引入漏洞条件。</p><p style="text-align: left;">HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters\</p><p style="text-align: left;">"EnableTrailerSupport"=dword:00000001</p><p style="text-align: left;">这一缓解措施不适用于其他受影响的版本。尽管如此，<a data-link="1" href="https://c.duomai.com/track.php?site_id=242986&euid=&t=https://www.microsoftstore.com.cn/" target="_blank">微软</a>建议IT人员优先对受影响的服务器进行修补。</p>   
</div>
            