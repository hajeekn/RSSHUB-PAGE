
---
title: '无法使用？版本号是三位数的Chrome自带_bug_'
categories: 
 - 新媒体
 - ZAKER
 - channel
headimg: 'https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202112/61cd5f60b15ec003115e0def_1024.jpg'
author: ZAKER
comments: false
date: Thu, 30 Dec 2021 03:01:00 GMT
thumbnail: 'https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202112/61cd5f60b15ec003115e0def_1024.jpg'
---

<div>   
<p>据报道，于 2008 年推出的 Chrome 浏览器将在明年年初迎来版本号为 100 的更新。然而，这个版本在正式测试的过程中出现了 bug，一些网站可能无法在这个版本的浏览器中打开。</p><p></p><div class="img_box" id="id_imagebox_0" onclick><div class="content_img_div perview_img_div"><img class="lazy opacity_0 " id="img_0" data-original="http://zkres2.myzaker.com/202112/61cd5f60b15ec003115e0def_1024.jpg" data-height="683" data-width="1024" src="https://cors.zfour.workers.dev/?http://zkres2.myzaker.com/202112/61cd5f60b15ec003115e0def_1024.jpg" referrerpolicy="no-referrer"></div></div>据了解，Chrome 100 版本没有重大变化或革命性的新功能。然而，通过 Chrome 100 浏览网站，有些网站可能会无法正常识别浏览器版本，导致用户无法正常使用网页。谷歌表示这一问题主要出现在利用 Duda 开发的网站，并已经开始进行修复。<p></p><p>这一问题的原因其实非常简单，大部分的网站都是通过检查 User Agent string（用户代理字符串）来确定用户的浏览器版本。Duda 的问题在于，其开发者选择只读取前两位数字，因此 "Chrome / 96" 将是 96，而 "Chrome / 100" 将被视为 10。不仅如此，Duda 会自动阻止任何低于 40 版本的 Chrome 浏览器。由于这个原因，Chrome 100 将被视为 Chrome 10，并将被网页设计工具包自动屏蔽，使得使用它创建的网站无法正确显示。</p><p>其实谷歌已经早就意识到这一版本更新可能会导致旧网站出现问题，曾在 11 月发表的一篇博文中开始警告用户和网站所有者潜在的问题。</p><p>谷歌曾提出一个解决方案：可以将 Chrome 的主要版本锁定为 99，而版本号则放在次要位置，这样在用户代理字符串中表达版本号的内容就会以 "Chrome/99.100.X.X" 的方式呈现，从而解决识别问题。</p><p>而根据最新消息，在 Duda 发布的一份声明中，该公司明确表示，他们的网页设计工具包已更新，这个问题已经解决，远远早于 Chrome 100 的计划发布时间。使用 Duda 制作的所有网站在 Chrome 100 发布后将继续正常运行。</p><div id="recommend_bottom"></div><div id="article_bottom"></div>  
</div>
            