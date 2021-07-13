
---
title: 'git操作笔记（一）git安装与最常用命令'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f71dbfbeaf6e467a8994e63d5797275e~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 05:12:31 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f71dbfbeaf6e467a8994e63d5797275e~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">git概述</h3>
<p>Git是一个分布式版本控制系统。</p>
<h3 data-id="heading-1">git工作机制</h3>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f71dbfbeaf6e467a8994e63d5797275e~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-2">git和代码托管中心</h3>
<p>代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为<strong>远程库</strong>。</p>
<ul>
<li>局域网
<ul>
<li>GitLab</li>
</ul>
</li>
<li>互联网
<ul>
<li>GitHub（外网）</li>
<li>Gitee码云（国内网站）</li>
</ul>
</li>
</ul>
<h3 data-id="heading-3">git安装</h3>
<p>官网地址： <a href="https://link.juejin.cn/?target=https%3A%2F%2Fgit-scm.com%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://git-scm.com/" ref="nofollow noopener noreferrer">git-scm.com/</a></p>
<p>查看git版本：<code>git --version</code></p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e8e108efc5de48b18a11a6c5c080dac4~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>选择 Git 安装位置，要求是非中文并且没有空格的目录，然后下一步。
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/133d25ef0f51482499e0ee2dbad7bdb2~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>Git选项配置，推荐默认设置，然后下一步。
<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9d8be61ff7ce4d73ac43f406eee32fe7~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>Git安装目录名，不用修改，直接点击下一步。
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3222e0bd22a848058961726bbf09225a~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>Git 的默认编辑器，建议使用默认的 Vim 编辑器，然后点击下一步。
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6a949141886e498a897f799de1dd81ff~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>默认分支名设置，选择让 Git 决定，分支名默认为 master，下一步
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7e15d92192724d6d8113add9bee1fd26~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>修改 Git 的环境变量，选第一个，不修改环境变量，只在 Git Bash 里使用 Git。
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8241c6f6f02e469da24b9f952c3b996e~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>选择后台客户端连接协议，选默认值 OpenSSL，然后下一步。
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71f50a16117540a58bafc0502b3bfb9c~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>配置 Git 文件的行末换行符，Windows 使用 CRLF，Linux 使用 LF，选择第一个自动转换，然后继续下一步。
<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/44235bcd637f433caf9d1bfdbcaf574e~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>选择 Git 终端类型，选择默认的 Git Bash 终端，然后继续下一步。
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b7d2c2d5ddd24ce68689505525de3008~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>选择 Git pull 合并的模式，选择默认，然后下一步。
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/90745a2d32184c1a850b06e54762ad8b~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>选择 Git 的凭据管理器，选择默认的跨平台的凭据管理器，然后下一步。
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e728eb5c126f4883a1f77a87b14724e7~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>其他配置，选择默认设置，然后下一步。
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1f10fa6e606e4506a22861b825fa24f1~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>实验室功能，技术还不成熟，有已知的 bug，不要勾选，然后点击右下角的 Install
按钮，开始安装 Git。
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bc58aad4a9414765822174aae2a82dd4~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>点击 Finsh 按钮，Git 安装成功！
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4b3d00acbea74702bff34e829d70ac03~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-4">git常用命令</h3>













































<table><thead><tr><th>命令名称</th><th>作用</th></tr></thead><tbody><tr><td>git config --global user.name 用户名</td><td>设置用户签名</td></tr><tr><td>git config --global user.email 邮件</td><td>设置用户签名</td></tr><tr><td>git init</td><td>初始化本地库</td></tr><tr><td>git status</td><td>查看本地库状态</td></tr><tr><td>git add 文件名</td><td>添加到暂存区</td></tr><tr><td>git commit -m "日志信息" 文件名</td><td>提交到本地库</td></tr><tr><td>git reflog</td><td>查看历史记录</td></tr><tr><td>git reset --hard 版本号</td><td>版本穿梭</td></tr><tr><td>git config --global credential.helper store</td><td>输入该命令后再次输入用户名/密码便可记住</td></tr></tbody></table>
<h4 data-id="heading-5">1. 设置用户签名</h4>
<ol>
<li>
<p>基本语法</p>
<pre><code class="hljs language-js copyable" lang="js">git config --<span class="hljs-built_in">global</span> user.name 用户名
git config --<span class="hljs-built_in">global</span> user.email 邮箱
<span class="copy-code-btn">复制代码</span></code></pre>
</li>
<li>
<p>实操案例</p>
</li>
</ol>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6c07b1b001884e2d92eb0b906256dbd5~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>说明：</p>
<p>签名作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看到，以此确认本次提交是谁做的。git首次安装必须设置一下用户签名，否则无法提交代码。</p>
<p><strong>注意：</strong> 这里设置用户签名和将来登录 GitHub (或其他代码托管中心)的账号没有任何关系。</p>
<h4 data-id="heading-6">2. 初始化本地库</h4>
<ol>
<li>
<p>基本语法</p>
<p>git init</p>
</li>
<li>
<p>案例实操</p>
</li>
<li>
<p>结果查看</p>
<p>文件夹下出现<code>.git</code>文件夹</p>
</li>
</ol>
<h4 data-id="heading-7">3. 查看本地库状态</h4>
<ol>
<li>
<p>基本语法</p>
<p>git status</p>
</li>
<li>
<p>案例实操</p>
<ul>
<li>
<p>首次查看（工作区没有任何文件）</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c7a1e7f1d228483fa9e178c51d5fbe35~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
<li>
<p>新增文件（hello.txt）</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e8423a5d195d410e902d60fa96e0775f~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
<li>
<p>再次查看（检测到未追踪的文件）</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/22359b9474d54a7185281395dcca4497~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
</ul>
</li>
</ol>
<h4 data-id="heading-8">4. 添加暂存区</h4>
<h5 data-id="heading-9">4.1 将工作区的文件添加到暂存区</h5>
<ol>
<li>
<p>基本语法</p>
<p>git add 文件名</p>
</li>
<li>
<p>案例实操</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ebf08147818643f2aa0c7ad1f3bface8~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
</ol>
<h4 data-id="heading-10">5. 提交本地库</h4>
<h5 data-id="heading-11">5.1 将暂存区的文件提交到本地库</h5>
<ol>
<li>
<p>基本语法</p>
<p>git commit -m "日志信息" 文件名</p>
</li>
<li>
<p>案例实操</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8088bbc5a3a24200ab94b3d9ad82188f~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
</ol>
<h4 data-id="heading-12">6. 修改文件（hello.txt）</h4>
<pre><code class="copyable">vim hello.txt
<span class="copy-code-btn">复制代码</span></code></pre>
<h5 data-id="heading-13">6.1 查看状态（检测到工作区有文件被修改）</h5>
<pre><code class="copyable">git status
<span class="copy-code-btn">复制代码</span></code></pre>
<h5 data-id="heading-14">6.2 将修改的文件再次添加暂存区</h5>
<pre><code class="copyable">git add hello.txt
<span class="copy-code-btn">复制代码</span></code></pre>
<h5 data-id="heading-15">6.3 查看状态（工作区的修改添加到了暂存区）</h5>
<pre><code class="copyable">git status
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-16">7. 历史版本</h4>
<h5 data-id="heading-17">7.1 查看历史版本</h5>
<ol>
<li>
<p>基本语法</p>
<p>git reflog查看版本信息</p>
<p>git log查看版本详细信息</p>
</li>
<li>
<p>案例实操</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/677dcfe8ac514a7abf3781b2a57c9698~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
</ol>
<h5 data-id="heading-18">7.2 版本穿梭</h5>
<ol>
<li>
<p>基本语法</p>
<p>git reset --hard 版本号</p>
</li>
<li>
<p>案例实操</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a0b9df5e6ddb4a458821350a13a72026~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
</li>
</ol>
<p>Git切换版本，底层其实移动的 HEAD 指针，具体原理如下图所示。</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5da86b74f6f142749db04750b73a1a88~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h4 data-id="heading-19">8. git SSL certificate problem: unable to get local issuer certificate</h4>
<p>这个问题是由于没有配置信任的服务器HTTPS验证。默认，cURL被设为不信任任何CAs，就是说，它不信任任何服务器验证。</p>
<p>执行以下命令：</p>
<pre><code class="copyable">git config --global http.sslVerify false
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-20">9. 记住用户名和密码</h4>
<pre><code class="copyable">git config --global credential.helper store
<span class="copy-code-btn">复制代码</span></code></pre>
<p>输入完该命令后再次输入用户名密码即可</p>
<h4 data-id="heading-21">10. 查看分支</h4>
<pre><code class="copyable">git branch// 查看本地所有分支

git branch -r// 查看远程所有分支

git branch -a// 查看本地和远程的所有分支

git branch <branchname>// 新建分支

git branch -d <branchname>// 删除本地分支

git branch -d -r <branchname>// 删除远程分支，删除后还需推送到服务器
git push origin:<branchname>// 删除后推送至服务器

git branch -m <oldbranch> <newbranch>// 重命名本地分支

/**
* 重命名远程分支：
* 1. 删除远程待修改分支
* 2. push本地新分支到远程服务器
*/
// git中一些选项解释：

-d
--delete: 删除

-D
--delete --force的快捷键

-f
--force: 强制

-m
--move: 移动或重命名

-M
--move --force的快捷键

-r
--remote：远程

-a
--all: 所有
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-22">11. git fetch用法</h4>
<pre><code class="copyable">git fetch <远程主机名>// 这个命令将某个远程主机的更新全部取回本地
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如果只想取回特定分支的更新，可以指定分支名：</p>
<pre><code class="copyable">git fetch <远程主机名> <分支名>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>最常见的命令如取回origin主机的master分支</p>
<pre><code class="copyable">git fetch origin master
<span class="copy-code-btn">复制代码</span></code></pre>
<p>取回更新后，会返回一个FETCH_HEAD，指的是某个branch在服务器上的最新状态，我们可以在本地通过它查看刚取会的更新信息：</p>
<pre><code class="copyable">git log -p FETCH_HEAD
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-23">12. git pull 用法</h4>
<p>git pull 的过程可以理解为：</p>
<pre><code class="hljs language-js copyable" lang="js">git fetch origin master<span class="hljs-comment">// 从远程主机的master分支拉取最新内容</span>
git merge FETCH_HEAD<span class="hljs-comment">// 将拉取下来的最新内容合并到当前所在的分支中</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>即将远程主机的某个分支的更新取回，并与本地指定的分支合并，完整格式可表示为：</p>
<pre><code class="copyable">git pull <远程主机名> <远程分支名>:<本地分支名>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>如果远程分支是与当前分支合并，则冒号后面的部分可以省略：</p>
<pre><code class="copyable">git pull origin next
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-24">13. 创建本地分支</h4>
<p><code>git checkout 分支名</code>切换到本地分支</p>
<p><code>git checkout -b 分支名</code>创建本地分支并切换</p>
<p><code>git push origin 本地分支名</code></p>
<h4 data-id="heading-25">14. 删除远程分支</h4>
<p><code>git push --delete origin dev </code></p>
<p>删除本地分支：<code>git branch -d dev</code></p></div>  
</div>
            