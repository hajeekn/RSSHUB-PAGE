
---
title: '用Docker来解决LetsEncrypt证书失效'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4ca06706f2640e7aadc5160a82a178d~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 09:28:59 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4ca06706f2640e7aadc5160a82a178d~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>起因是因为 <code>Let's Encrypt</code> 的管理证书协议 <code>ACMEv1</code> 要在今年废弃掉，导致一台老服务器上的 <code>https</code> 失效。<code>Let's Encrypt</code> 官方推荐的方法是更新到支持 <code>ACMEv2</code> 的 <code>certbot</code> 版本。服务器是Ubuntu 14.04，支持<code>ACMEv2</code>的客户端需要更新到Ubuntu 16.04 ，因为更新系统的不确定性，所以想到了使用 Docker 去解决这个问题。</p>
<p>项目结构大概是这样</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4ca06706f2640e7aadc5160a82a178d~tplv-k3u1fbpfcp-watermark.image" alt="3B751CEB-020F-4EF2-ABC6-27D54F7BB405.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>Nginx 做 Node Server 的反向代理，Certbot 用来获取并更新 Nginx 的 ssl 证书。</p>
<p>我们的目的是用容器将三个服务整合在一起。</p>
<h2 data-id="heading-0">构建 Node Server 的镜像</h2>
<p>首先是要将 Node Server 进行Docker 化，直接在项目中加入 Dockerfile。
</p>
<pre><code class="hljs language-yaml copyable" lang="yaml"><span class="hljs-string">FROM</span> <span class="hljs-string">node:6.17.1</span>

<span class="hljs-string">ENV</span> <span class="hljs-string">NODE_ENV=production</span>
<span class="hljs-string">WORKDIR</span>  <span class="hljs-string">/server</span>

<span class="hljs-string">COPY</span> [<span class="hljs-string">"package.json"</span>, <span class="hljs-string">"package-lock.json*"</span>, <span class="hljs-string">"yarn.lock"</span>, <span class="hljs-string">"npm-shrinkwrap.json*"</span>, <span class="hljs-string">"./"</span>]

<span class="hljs-string">RUN</span> <span class="hljs-string">yarn</span> <span class="hljs-string">--silent</span> <span class="hljs-string">--production</span>
<span class="hljs-string">COPY</span> <span class="hljs-string">.</span> <span class="hljs-string">.</span>
<span class="hljs-string">EXPOSE</span> <span class="hljs-number">3000</span>
<span class="hljs-string">RUN</span> <span class="hljs-string">yarn</span> <span class="hljs-string">global</span> <span class="hljs-string">add</span> <span class="hljs-string">gulp</span>

<span class="hljs-string">CMD</span> [<span class="hljs-string">"yarn"</span>, <span class="hljs-string">"deploy"</span>]
<span class="copy-code-btn">复制代码</span></code></pre>
<p>环境是直接用 node 官方的 <code>v6.17.1</code>，WORKDIR 是之后命令的工作目录，安装依赖，暴露 3000 端口，执行部署命令。</p>
<p>中途遇到了个小问题，因为deploy 命令后面是用 gulp 执行的，容器中局部依赖安装 gulp 找不到该命令，这里找到一篇文章来讨论这个问题<a href="https://link.juejin.cn/?target=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F22115400%2Fwhy-do-we-need-to-install-gulp-globally-and-locally" target="_blank" rel="nofollow noopener noreferrer" title="https://stackoverflow.com/questions/22115400/why-do-we-need-to-install-gulp-globally-and-locally" ref="nofollow noopener noreferrer">Why do we need to install gulp globally and locally?</a>
这里我只是按最无脑的方法解决了，也可以使用 <code>npm link</code> 或者
<code>alias node_modules/.bin/gulp</code> 的方式去处理。</p>
<p>Dockerfile 完成之后，用 <code>docker build . -t nodeapp</code> 来构建 docker image。</p>
<h2 data-id="heading-1">Nginx + Certbot</h2>
<p>在思考如何才能解决证书问题的时候，看到 certbot 的官网上有 Docker 的安装方式，但是因为容器间的通讯问题，certbot 虽然能自动获取证书，但需要手动去安装到 nginx 上。</p>
<p>大体的思路如下：</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/023d711aa23d42c28aea2e54723edc02~tplv-k3u1fbpfcp-watermark.image" alt="2BAF68A4-C638-40F8-B5E4-17B47C38C27E.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>按照这个思路做的时候，发现已经有人造过轮子了。
<a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fwmnnd%2Fnginx-certbot" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/wmnnd/nginx-certbot" ref="nofollow noopener noreferrer">Boilerplate for nginx with Let’s Encrypt on docker-compose</a>
他的处理方式是通过 <code>docker-compose</code> 来将 Nginx 和 certbot 两个容器通过上图的方式建立联系。</p>
<p>这里有个鸡生蛋蛋生鸡的问题，LetsEncrypt 的验证方式是访问域名中的一个 <code>/.well-known/acme-challenge/xxx</code> 地址来进行验证，返回的数据是由 certbot 来提供。但如果一开始不提供证书的话，nginx 就不能启动。作者的方法是先生成一个假证书来启动 nginx，然后用获取到的真证书替换掉假证书。</p>
<p>因为在上面 Boilerplate 中已经有一个脚本来处理，就不重复造轮子了。</p>
<p>nginx 的配置文件如下</p>
<pre><code class="hljs language-conf copyable" lang="conf">server &#123;
    listen 80;
    server_name example.org;
    server_tokens off;

    location /.well-known/acme-challenge/ &#123;
        root /var/www/certbot;
    &#125;

    location / &#123;
        return 301 https://$host$request_uri;
    &#125;
&#125;

server &#123;
    listen 443 ssl;
    server_name example.org;
    server_tokens off;

    ssl_certificate /etc/letsencrypt/live/example.org/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.org/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / &#123;
        proxy_pass  http://example.org;
        proxy_set_header    Host                $http_host;
        proxy_set_header    X-Real-IP           $remote_addr;
        proxy_set_header    X-Forwarded-For     $proxy_add_x_forwarded_for;
    &#125;
&#125;

<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-2">拼装 Node Server + Nginx</h2>
<p>我们现在已经获得了一个有了合法证书的 Nginx 服务器了，将 node server 接在 Nginx 的后面就大功告成了。
我们直接在前面的boilerplate中提供的 <code>docker-compose.yml</code> 进行一些修改。</p>
<pre><code class="hljs language-yaml copyable" lang="yaml"><span class="hljs-attr">version:</span> <span class="hljs-string">"3"</span>

<span class="hljs-attr">services:</span>
  <span class="hljs-attr">nodeapp:</span>
    <span class="hljs-attr">image:</span> <span class="hljs-string">nodeserver:1.0.0</span>
    <span class="hljs-attr">container_name:</span> <span class="hljs-string">nodeapp</span>
    <span class="hljs-attr">restart:</span> <span class="hljs-string">unless-stopped</span>
    <span class="hljs-attr">volumes:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">/data/usersFolder:/server/config</span>
    <span class="hljs-attr">ports:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">"3000:3000"</span>
    <span class="hljs-attr">networks:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">app-network</span>

  <span class="hljs-attr">nginx:</span>
    <span class="hljs-attr">image:</span> <span class="hljs-string">nginx:1.15-alpine</span>
    <span class="hljs-attr">container_name:</span> <span class="hljs-string">nginx_server</span>
    <span class="hljs-attr">restart:</span> <span class="hljs-string">unless-stopped</span>
    <span class="hljs-attr">volumes:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">./data/nginx:/etc/nginx/conf.d</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">./data/certbot/conf:/etc/letsencrypt</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">./data/certbot/www:/var/www/certbot</span>
    <span class="hljs-attr">ports:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">"80:80"</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">"443:443"</span>
    <span class="hljs-attr">networks:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">app-network</span>
    <span class="hljs-attr">command:</span> <span class="hljs-string">'/bin/sh -c '</span><span class="hljs-string">'while :; do sleep 6h & wait $$&#123;!&#125;; nginx -s reload; done & nginx -g "daemon off;"'</span><span class="hljs-string">''</span>

  <span class="hljs-attr">certbot:</span>
    <span class="hljs-attr">image:</span> <span class="hljs-string">certbot/certbot</span>
    <span class="hljs-attr">restart:</span> <span class="hljs-string">unless-stopped</span>
    <span class="hljs-attr">container_name:</span> <span class="hljs-string">certbot_one</span>
    <span class="hljs-attr">volumes:</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">./data/certbot/conf:/etc/letsencrypt</span>
      <span class="hljs-bullet">-</span> <span class="hljs-string">./data/certbot/www:/var/www/certbot</span>
    <span class="hljs-attr">entrypoint:</span> <span class="hljs-string">"/bin/sh -c 'trap exit TERM; while :; do certbot renew; sleep 12h & wait $$&#123;!&#125;; done;'"</span>

<span class="hljs-attr">networks:</span>
  <span class="hljs-attr">app-network:</span>
    <span class="hljs-attr">driver:</span> <span class="hljs-string">bridge</span>
<span class="copy-code-btn">复制代码</span></code></pre>
<p>通过创建一个 network 来让 nginx 直接和 node server 通信，nginx 的conf 也可以写的比较顺滑。以前我记得可以使用 <code>—link</code> 来进行容器间通信，但官方更推荐的做法还是创建一个 network。</p>
<h2 data-id="heading-3">docker-compose up !</h2>
<p>执行 boilerplate 中的脚本启动 nginx 并获取到证书，再通过 <code>docker-compose up</code> 启动 node server。
这样，我们得到了一个带 https 并通过 nginx 作为反向代理的 node server。</p>
<h4 data-id="heading-4">如果有写的不对的地方或者对过程有不明白的地方，欢迎讨论。</h4></div>  
</div>
            