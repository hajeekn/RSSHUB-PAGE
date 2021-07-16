
---
title: 'Svelte系列 --- props'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=6606'
author: 掘金
comments: false
date: Thu, 15 Jul 2021 06:16:26 GMT
thumbnail: 'https://picsum.photos/400/300?random=6606'
---

<div>   
<div class="markdown-body"><style>@charset "UTF-8";.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:14px;overflow-x:hidden;color:#353535&#125;.markdown-body h1&#123;padding-bottom:4px;font-size:30px&#125;.markdown-body h1,.markdown-body h2&#123;margin-top:36px;margin-bottom:10px;line-height:1.5;color:#005bb7&#125;.markdown-body h2&#123;position:relative;padding-left:16px;padding-right:10px;padding-bottom:10px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h2:before&#123;content:"「";position:absolute;top:-6px;left:-10px&#125;.markdown-body h2:after&#123;content:"」";position:absolute;top:6px;right:auto&#125;.markdown-body h3&#123;position:relative;padding-bottom:0;margin-top:30px;margin-bottom:10px;font-size:20px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body h3:before&#123;content:"»";padding-right:6px;color:#2196f3&#125;.markdown-body h4&#123;margin-top:24px;font-size:16px&#125;.markdown-body h4,.markdown-body h5&#123;padding-bottom:0;margin-bottom:10px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body h5&#123;margin-top:18px;font-size:14px&#125;.markdown-body h6&#123;padding-bottom:0;margin-top:12px;margin-bottom:10px;font-size:12px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body p&#123;line-height:inherit;margin-top:16px;margin-bottom:16px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;position:relative;width:98%;height:1px;margin-top:32px;margin-bottom:32px;background-image:linear-gradient(90deg,#007fff,rgba(255,0,0,.3),hsla(0,0%,100%,.1),rgba(255,0,0,.3),#007fff);border-width:0;overflow:visible&#125;.markdown-body hr:after&#123;content:"";position:absolute;margin:auto;left:0;right:0;bottom:0;top:0;display:inline-block;width:60px;height:20px;background:#fff;background-image:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAgCAYAAABgrToAAAADoklEQVRYR82XTYgcRRTHf2933Q1RjAa9eFO8JHoJ8RQVBQ2iBwXBET0YEUTXNVmNQtTpmeqaWV0XNRq/o4KoECSCEPSg4CF+BYUkIIiCoCJCPIhC/Ihh2Z0nVV27VnZnenumW9i6ddV7//frV69fVQurfMgq56NawFTPAU6QyomqXrw6wIZeyhCPebA5buNR+akKyGoAjd6BshthnYdSjqNcRVuOlIUsD2j0SuA94IwuMHdh5ZUykOUBXfSGbmKI54EtAeYIHSZoy5dl4JxvNYBOKdW1KE8BQ8AkVk6WhasWsAiN0TX9gveXQaPP+Aytpc4u+bMI06JNohsYYYYOR2lJWtS3OKDRfcAtQfgDoI6Vo4UCGb0OmAEuDvZvYmVbEd/igC3dzDz7gQu8sPA9kJDK27mBmjqBeLjTg90PDFOjWawFFQd06kZHEfaj3LAIpTRpSXsZ5E06zEYP9sDimnAApYaV2SLZG/wjMeqAkijwW4xQJ5Gf/ZzRC8OW3hiBTGGlURRswW55Bh/Ssxljrwew8l1PQaM14GngvGDzBUKdDsMeTtgU5o8B92PFlUf3YXUrHa7Fys6lBqcCGnX15YQ2A18FyPd7Crd1A3M8C1wdbH4DD3hWeP6IEXbQkG97ajR1HPFnuPP5jFFq1OWX7hl8WM9l1AO648uNfwLk7tytMeogty+xeQ4rO3r6bdcx1nuwOGsHmaXGtPzae4uzGnLH1kQkvpdZGrHjssBZJrL+pqS05KWc8tgITAPXRzYvYOXe/C2OV43eDcRBDtIhoS2f9wzc0Cv8Wls+zoFzUC5zF0U241h5uZtPfptp6OUM8wbK+cH5GEpCS17P3fJei0Z3+npTxryJ8CPzbKMtn/ZyWbkPGl0PuFPkmkjkcb4h4R2ZLwRq1H0ALmvjkf2HwK1Y+T1PY2XABe/sHJ6MxN5lnoSpnC/UGbsTaI5phK2R7x6s3Ffk5YoDOrWm3onwJHBmEP86bPmBrsGaenNoIdnxCH+gPEhLXi0Cl1VBvyPVLSh7gEuC62yAfOIUqabWEaaiucMIk6RyqJ+Q/QM69V26jjW86Gvov/EaoyT8zRCn+Xq7PVrbx0nuYUaO9wM3WAbjCE1NEUw09Um4UV+2OKfYfu5/S19gsAzGKqm6LE5FrShbdS0ku465DjDwKA/oQht19ejqbaEVuRbiLhuHByYLjtUAZpDutzP7cYdHsPJXWbjyNVgFwQoa1WXwf4Jd9YD/Ap80+yE7+u9aAAAAAElFTkSuQmCC);background-repeat:no-repeat;background-size:auto 100%;background-position-x:center&#125;.markdown-body code&#123;padding:.065em .4em;font-size:.87em;color:#c2185b;word-break:break-word;overflow-x:auto;background-color:#fff4f4;border-radius:2px&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;display:block;padding:16px 12px;margin:0;font-size:12px;color:#333;word-break:normal;overflow-x:auto;background:#f8f8f8&#125;.markdown-body pre>code::-webkit-scrollbar&#123;width:4px;height:4px&#125;.markdown-body pre>code::-webkit-scrollbar-track&#123;background-color:#bedcff&#125;.markdown-body pre>code::-webkit-scrollbar-thumb&#123;background-color:#2196f3;border-radius:10px&#125;.markdown-body a&#123;position:relative;text-decoration:none;color:#3da8f5;border-bottom:1px solid #bedcff&#125;.markdown-body a:hover&#123;color:#007fff;border-bottom-color:#007fff&#125;.markdown-body a:active&#123;color:#007fff&#125;.markdown-body a:after&#123;position:absolute;content:"";top:100%;left:0;width:100%;opacity:0;border-bottom:1px solid #bedcff;transition:top .3s,opacity .3s;transform:translateZ(0)&#125;.markdown-body a:hover:after&#123;top:0;opacity:1;border-bottom-color:#007fff&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #c3e0fd;border-spacing:0;border-collapse:collapse&#125;.markdown-body table thead&#123;color:#000;text-align:left;font-size:14px;background:#f6f6f6&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f7fbff&#125;.markdown-body table tr:hover&#123;background-color:#e0edf7&#125;.markdown-body table td,.markdown-body table th&#123;padding:12px 8px;line-height:24px;border:1px solid #c3e0fd&#125;.markdown-body table th&#123;color:#005bb7;background-color:#dff0ff&#125;.markdown-body table td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#8c8c8c;border-left:4px solid #2196f3;background-color:#f0fdff;padding:1px 20px;margin:22px 0&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body b,.markdown-body blockquote>b,.markdown-body blockquote>strong,.markdown-body strong&#123;color:#2196f3&#125;.markdown-body em,.markdown-body i&#123;color:#4fc3f7&#125;.markdown-body del&#123;color:#ccc&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:4px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body details>summary&#123;outline:none;color:#005bb7;font-size:20px;font-weight:bolder;border-bottom:1px solid #bedcff;cursor:pointer&#125;.markdown-body details>p&#123;padding:10px 20px;margin:10px 0 0;color:#666;background-color:#f0fdff;border:2px dashed #2196f3&#125;.markdown-body h1::selection,.markdown-body h2::selection,.markdown-body h3::selection,.markdown-body h4::selection,.markdown-body h5::selection,.markdown-body h6::selection&#123;color:#005bb7;background-color:rgba(160,200,255,.15)&#125;.markdown-body p::selection&#123;color:#c80000&#125;.markdown-body a::selection,.markdown-body b::selection,.markdown-body del::selection,.markdown-body em::selection,.markdown-body i::selection,.markdown-body strong::selection&#123;background-color:transparent&#125;.markdown-body code::selection&#123;background-color:#ffeaeb&#125;.markdown-body pre>code::selection&#123;background-color:rgba(160,200,255,.25)&#125;.markdown-body ol ::selection,.markdown-body ul ::selection&#123;background-color:rgba(160,200,255,.15)&#125;.markdown-body .contains-task-list&#123;padding-left:14px;list-style:none&#125;.markdown-body .contains-task-list input[type=checkbox]&#123;position:relative&#125;.markdown-body .contains-task-list input[type=checkbox]:before&#123;content:"";position:absolute;top:0;left:0;right:0;bottom:0;width:inherit;height:inherit;background:#f0f8ff;border:1px solid #add6ff;border-radius:2px;box-sizing:border-box;z-index:1&#125;.markdown-body .contains-task-list input[type=checkbox]:checked:after&#123;content:"✓";position:absolute;top:-12px;left:0;right:0;bottom:0;width:0;height:0;color:#f55;font-size:20px;font-weight:700;z-index:2&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><blockquote>
<p>在任何实际的应用程序中，都需要将数据从一个组件传递到其子组件(父子组件通信)。</p>
<p>为此，我们需要为组件声明 <em>属性(properties)</em>，通常缩写为 'props'。</p>
</blockquote>
<h3 data-id="heading-0">基本使用</h3>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-comment"><!-- 父组件 App.svelte --></span>
<span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
  <span class="hljs-keyword">import</span> Nested <span class="hljs-keyword">from</span> <span class="hljs-string">'./Nested.svelte'</span>;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-comment"><!-- 
1. svelte中的组件，引入后既可直接使用，不需要像vue一样需要先引入后注册
2. 组件名一般首字母要求大写，以便于区分普通html标签和组件元素
--></span>
<span class="hljs-tag"><<span class="hljs-name">Nested</span> <span class="hljs-attr">answer</span>=<span class="hljs-string">&#123;42&#125;/</span>></span>


<span class="hljs-comment"><!-- 子组件 Nested.svelte --></span>
<span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
  <span class="hljs-comment">// 我们使用export关键字来接收父组件传入的对应props</span>
  <span class="hljs-keyword">export</span> <span class="hljs-keyword">let</span> answer;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"><<span class="hljs-name">p</span>></span>The answer is &#123;answer&#125;<span class="hljs-tag"></<span class="hljs-name">p</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-1">默认值</h3>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-comment"><!-- 在子组件中 --></span>
<span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
  <span class="hljs-comment">// 我们为接收的props赋值的时候，所赋的值就是props的默认值</span>
  <span class="hljs-keyword">export</span> <span class="hljs-keyword">let</span> answer = <span class="hljs-string">'a mystery'</span>; 
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-comment"><!-- 在父组件中 --></span>
<span class="hljs-tag"><<span class="hljs-name">Nested</span> <span class="hljs-attr">answer</span>=<span class="hljs-string">&#123;42&#125;/</span>></span> <span class="hljs-comment"><!-- 子组件的answer的值为42 --></span>
<span class="hljs-tag"><<span class="hljs-name">Nested</span>/></span> <span class="hljs-comment"><!-- 子组件 answer的值使用默认值 即'a mystery' --></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-2">展开props</h3>
<blockquote>
<p>如果你的对象拥有很多属性，你可以 ‘展开’ 它们到组件中，无需逐个指定</p>
</blockquote>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
<span class="hljs-keyword">import</span> Info <span class="hljs-keyword">from</span> <span class="hljs-string">'./Info.svelte'</span>;

<span class="hljs-keyword">const</span> info = &#123;
<span class="hljs-attr">name</span>: <span class="hljs-string">'Klaus'</span>,
<span class="hljs-attr">age</span>: <span class="hljs-number">23</span>,
<span class="hljs-attr">gender</span>: <span class="hljs-string">'male'</span>,
<span class="hljs-attr">location</span>: <span class="hljs-string">'shanghai'</span>
&#125;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"><<span class="hljs-name">Info</span> <span class="hljs-attr">name</span>=<span class="hljs-string">&#123;info.name&#125;</span> <span class="hljs-attr">age</span>=<span class="hljs-string">&#123;info.age&#125;</span> <span class="hljs-attr">gender</span>=<span class="hljs-string">&#123;info.gender&#125;</span> <span class="hljs-attr">location</span>=<span class="hljs-string">&#123;info.location&#125;/</span>></span>
<span class="hljs-comment"><!-- 等价于 展开props和ES6中的展开运算符 --></span>
<span class="hljs-tag"><<span class="hljs-name">Info</span> &#123;<span class="hljs-attr">...info</span>&#125; /></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-3">$$props</h3>
<blockquote>
<p>在子组件中，有一个特殊变量<code>$$props</code>，这个变量的类型是一个<code>object</code>,默认值是一个<code>空对象</code></p>
<p>这个对象中存储着所有<code>由父组件传递给子组件的props</code>(无论这个prop有没有在子组件中使用export关键字接收)</p>
</blockquote>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
<span class="hljs-keyword">import</span> Info <span class="hljs-keyword">from</span> <span class="hljs-string">'./Info.svelte'</span>;

<span class="hljs-keyword">const</span> pkg = &#123;
<span class="hljs-attr">name</span>: <span class="hljs-string">'svelte'</span>,
<span class="hljs-attr">version</span>: <span class="hljs-number">3</span>,
<span class="hljs-attr">speed</span>: <span class="hljs-string">'blazing'</span>,
<span class="hljs-attr">website</span>: <span class="hljs-string">'https://svelte.dev'</span>
&#125;;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"><<span class="hljs-name">Info</span> <span class="hljs-attr">name</span>=<span class="hljs-string">&#123;pkg.name&#125;</span> <span class="hljs-attr">version</span>=<span class="hljs-string">&#123;pkg.version&#125;</span> <span class="hljs-attr">speed</span>=<span class="hljs-string">&#123;pkg.speed&#125;</span> <span class="hljs-attr">website</span>=<span class="hljs-string">&#123;pkg.website&#125;/</span>></span>
<span class="hljs-comment"><!-- 
此时，子组件Info的$$props的值为:
&#123;
name: 'svelte',
version: 3,
speed: 'blazing',
website: 'https://svelte.dev'
&#125;

tips:一般不推荐直接使用$$props,因为 Svelte 较难优化这种操作，极小数情况下它很有用。
--></span>
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            