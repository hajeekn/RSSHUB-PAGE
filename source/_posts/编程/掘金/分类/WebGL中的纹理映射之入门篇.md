
---
title: 'WebGL中的纹理映射之入门篇'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/82dcf69f830b4f89a93c59eb567bfc5e~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 05:13:24 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/82dcf69f830b4f89a93c59eb567bfc5e~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h2 data-id="heading-0">概念</h2>
<p>纹理映射能为图像添加上皮肤，将一张图片或者图像映射到几何图形上，其作用是根据纹理图像，为之前光栅化的每个片元涂上颜色 (组成纹理图像的像素又被称为纹素)</p>
<h2 data-id="heading-1">纹理坐标系(左) 与 图片坐标系(右)</h2>
<p>在纹理坐标系中，向上为y轴的正方向，图片坐标系则相反</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/82dcf69f830b4f89a93c59eb567bfc5e~tplv-k3u1fbpfcp-watermark.image" alt="截屏2021-07-12 下午7.49.12.png" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>纹理坐标系是理想状态，实际渲染纹理时 webgl 使用的图片坐标系。因此在向缓冲区对象中传递几何图形的点位和纹理图像的点位时，应该使用图片坐标系作为参考。</p>
</blockquote>
<h2 data-id="heading-2">取样器类型</h2>
<p>取样器只能是 uniform 变量，唯一能给取样器变量赋值的是纹理单元编号，必须使用 gl.uniform1i()赋值</p>
<ul>
<li>sampler2D - 2维平面取样器</li>
<li>samplerCube - 3维取样器</li>
</ul>
<pre><code class="hljs language-glsl copyable" lang="glsl">    <span class="hljs-comment">/* fragmentShader */</span>
    <span class="hljs-keyword">precision</span> <span class="hljs-keyword">mediump</span> <span class="hljs-type">float</span>;
    <span class="hljs-keyword">uniform</span> <span class="hljs-type">sampler2D</span> u_sampler;
    <span class="hljs-keyword">varying</span> <span class="hljs-type">vec2</span> v_textureCoord;
    <span class="hljs-type">void</span> main() &#123;
        <span class="hljs-built_in">gl_FragColor</span> = <span class="hljs-built_in">texture2D</span>(u_sampler, v_textureCoord);
    &#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h2 data-id="heading-3">纹理单元</h2>
<p>webgl通过一种叫纹理单元的机制来同时使用多个纹理，每个纹理单元有一个单元编号来管理一张纹理图像。即使当前程序只需要一个纹理，也需要为其指定一个纹理单元。</p>
<p>系统支持的纹理单元数取决于硬件和浏览器的webgl实现，默认情况下webgl支持8个纹理单元，一些其他系统支持的更多。内置变量 gl.TEXTURE0, gl.TEXTURE1, gl.TEXTURE2..., gl.TEXTURE7各表示一个纹理单元</p>
<h2 data-id="heading-4">纹理类型</h2>
<ul>
<li>gl.TEXTURE_2D (二维纹理)</li>
<li>gl.TEXTURE_CUBE_MAP (立方体纹理)</li>
</ul>
<h2 data-id="heading-5">纹理数据的数据格式</h2>

























<table><thead><tr><th>格式</th><th>描述</th></tr></thead><tbody><tr><td>gl.UNSIGNED_BYTE</td><td>无符号整型，每个颜色分量占1字节</td></tr><tr><td>gl.UNSIGNED_SHORT_5_6_5</td><td>RGB：每个分量分别占 5，6，5 比特</td></tr><tr><td>gl.UNSIGNED_SHORT_4_4_4_4</td><td>RGBA：每个分量分别占 4，4，4，4 比特</td></tr><tr><td>gl.UNSIGNED_SHORT_5_5_5_1</td><td>RGBA：每个分量分别占 5，5，5，1 比特</td></tr></tbody></table>
<h2 data-id="heading-6">webgl API</h2>



































<table><thead><tr><th>名称</th><th>参数</th><th>描述</th></tr></thead><tbody><tr><td>createTexture</td><td>无</td><td>创建纹理对象</td></tr><tr><td>activeTexture</td><td>texUnit - 指定纹理单元</td><td>激活纹理单元</td></tr><tr><td>bindTexture</td><td>target - 纹理类型 <br> texture - 绑定的纹理单元</td><td>绑定纹理对象</td></tr><tr><td>texParameteri</td><td>target <br> pname <br> param</td><td>配置纹理图像</td></tr><tr><td>texImage2D</td><td>target <br> level <br> internalformat <br> format <br> type <br> image</td><td>将纹理图像分配给纹理对象</td></tr></tbody></table>
<h2 data-id="heading-7">实现纹理映射的大致过程</h2>
<ul>
<li>准备纹理图像 - new Image()</li>
<li>配置纹理映射方式 - 将纹理图像如何放置在图形上</li>
<li>加载纹理图像，并对其配置，以在webgl中使用</li>
<li>在片元着色器中将相应的纹素从纹理中取出，并将纹素的颜色赋给片元</li>
</ul>
<h2 data-id="heading-8">纹理映射实现</h2>
<h3 data-id="heading-9">效果</h3>
<p>首先实现一个矩形</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6f1e902f77d04629b46babec8a9dd04a~tplv-k3u1fbpfcp-watermark.image" alt="截屏2021-07-12 下午8.59.57.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>添加纹理映射</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/37ff430554ef4da7acaa03ca2f8cf089~tplv-k3u1fbpfcp-watermark.image" alt="截屏2021-07-12 下午8.59.57.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-10">shader & js Code</h3>
<pre><code class="hljs language-glsl copyable" lang="glsl"><span class="hljs-comment">/*
    顶点着色器
    a_pointPosition: 顶点坐标
    a_textureCoord: 纹理坐标
    u_canvasSize: canvas画布大小
    v_textureCoord: 传递给片元着色器的纹理坐标
*/</span>
<span class="hljs-keyword">attribute</span> <span class="hljs-type">vec2</span> a_pointPosition;
<span class="hljs-keyword">attribute</span> <span class="hljs-type">vec2</span> a_textureCoord;
<span class="hljs-keyword">uniform</span> <span class="hljs-type">vec2</span> u_canvasSize;
<span class="hljs-keyword">varying</span> <span class="hljs-type">vec2</span> v_textureCoord;
<span class="hljs-type">void</span> main() &#123;
    <span class="hljs-type">float</span> x = a_pointPosition.x;
    <span class="hljs-type">float</span> y = a_pointPosition.y;

    x = x / u_canvasSize.x * <span class="hljs-number">2.0</span> - <span class="hljs-number">1.0</span>;
    y = <span class="hljs-number">1.0</span> - y / u_canvasSize.y * <span class="hljs-number">2.0</span>;

    <span class="hljs-built_in">gl_PointSize</span> = <span class="hljs-number">10.0</span>;
    <span class="hljs-built_in">gl_Position</span> = <span class="hljs-type">vec4</span>(x, y, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>);

    v_textureCoord = a_textureCoord;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-glsl copyable" lang="glsl"><span class="hljs-comment">/*
    片元着色器
    u_sampler: 取样器
    v_textureCoord: 纹理坐标
*/</span>
<span class="hljs-keyword">precision</span> <span class="hljs-keyword">mediump</span> <span class="hljs-type">float</span>;
<span class="hljs-keyword">uniform</span> <span class="hljs-type">sampler2D</span> u_sampler;
<span class="hljs-keyword">varying</span> <span class="hljs-type">vec2</span> v_textureCoord;
<span class="hljs-type">void</span> main() &#123;
    <span class="hljs-built_in">gl_FragColor</span> = <span class="hljs-built_in">texture2D</span>(u_sampler, v_textureCoord);
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-comment">// js主要逻辑</span>
<span class="hljs-keyword">import</span> WebGLProgram <span class="hljs-keyword">from</span> <span class="hljs-string">'../gl/base.js'</span>
<span class="hljs-keyword">import</span> defineVertexShaderSource <span class="hljs-keyword">from</span> <span class="hljs-string">'./shader/vertexShader.js'</span>;
<span class="hljs-keyword">import</span> defineFragmentShaderSource <span class="hljs-keyword">from</span> <span class="hljs-string">'./shader/fragmentShader.js'</span>;

<span class="hljs-keyword">import</span> &#123; getRandomColor &#125; <span class="hljs-keyword">from</span> <span class="hljs-string">'../utils/index.js'</span>

<span class="hljs-keyword">const</span> glProgram = <span class="hljs-keyword">new</span> WebGLProgram(&#123;
    <span class="hljs-attr">id</span>: <span class="hljs-string">'root'</span>,
    defineVertexShaderSource,
    defineFragmentShaderSource
&#125;);
<span class="hljs-keyword">const</span> &#123; gl, program &#125; = glProgram;

<span class="hljs-keyword">const</span> root = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'root'</span>);

<span class="hljs-comment">// 获取glsl变量的内存地址</span>
<span class="hljs-keyword">const</span> positionLocation = gl.getAttribLocation(program, <span class="hljs-string">'a_pointPosition'</span>);
<span class="hljs-keyword">const</span> textureCoordLocation = gl.getAttribLocation(program, <span class="hljs-string">'a_textureCoord'</span>)
<span class="hljs-keyword">const</span> sizeLocation = gl.getUniformLocation(program, <span class="hljs-string">'u_canvasSize'</span>);
<span class="hljs-keyword">const</span> samplerLocation = gl.getUniformLocation(program, <span class="hljs-string">'u_sampler'</span>);

<span class="hljs-comment">// 将 canvas 画布大小传入到 顶点着色器中</span>
gl.uniform2f(sizeLocation, root.width, root.height);

<span class="hljs-comment">// 创建缓冲区对象</span>
<span class="hljs-keyword">const</span> buffer = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, buffer);
<span class="hljs-comment">// 创建缓冲区索引对象</span>
<span class="hljs-keyword">const</span> indexBuffer = gl.createBuffer();
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, indexBuffer);

<span class="hljs-keyword">const</span> img = <span class="hljs-keyword">new</span> Image();
img.src = <span class="hljs-string">'./image/01.jpeg'</span>;

img.onload = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-comment">// 创建纹理对象</span>
    <span class="hljs-keyword">const</span> texture = gl.createTexture();
    <span class="hljs-comment">// 激活纹理单元</span>
    gl.activeTexture(gl.TEXTURE0);
    <span class="hljs-comment">// 将纹理对象绑定到 webgl 系统中</span>
    gl.bindTexture(gl.TEXTURE_2D, texture);
    <span class="hljs-comment">// 配置纹理图像 映射到 图形上的（放大，缩小，拉伸）方式</span>
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.NEAREST);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
    <span class="hljs-comment">// 将纹理图像分配到纹理对象上</span>
    gl.texImage2D(gl.TEXTURE_2D, <span class="hljs-number">0</span>, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, img);
    <span class="hljs-comment">// 向片元着色器传递纹理单元的编号</span>
    gl.uniform1i(samplerLocation, <span class="hljs-number">0</span>);

    render();
&#125;

<span class="hljs-comment">// 渲染函数</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">render</span>(<span class="hljs-params"></span>) </span>&#123;
    <span class="hljs-comment">// 向顶点缓冲区填充数据</span>
    gl.bufferData(
        gl.ARRAY_BUFFER,
        <span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>([
            <span class="hljs-number">50</span>, <span class="hljs-number">50</span>, <span class="hljs-number">0</span>, <span class="hljs-number">0</span>,
            <span class="hljs-number">50</span>, <span class="hljs-number">300</span>, <span class="hljs-number">0</span>, <span class="hljs-number">1</span>,
            <span class="hljs-number">400</span>, <span class="hljs-number">300</span>, <span class="hljs-number">1</span>, <span class="hljs-number">1</span>,
            <span class="hljs-number">400</span>, <span class="hljs-number">50</span>, <span class="hljs-number">1</span>, <span class="hljs-number">0</span>,
        ]),
        gl.STATIC_DRAW
    );

    <span class="hljs-comment">// 向索引缓冲区填充数据</span>
    gl.bufferData(
        gl.ELEMENT_ARRAY_BUFFER,
        <span class="hljs-keyword">new</span> <span class="hljs-built_in">Uint16Array</span>([
            <span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>
        ]),
        gl.STATIC_DRAW
    )
    <span class="hljs-comment">// 指定缓冲区对象中 数据 与 顶点变量 的映射关系</span>
    gl.vertexAttribPointer(positionLocation, <span class="hljs-number">2</span>, gl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">4</span> * <span class="hljs-number">4</span>, <span class="hljs-number">0</span>);
    <span class="hljs-comment">// 指定缓冲区对象中 数据 与 纹理变量 的映射关系</span>
    gl.vertexAttribPointer(textureCoordLocation, <span class="hljs-number">2</span>, gl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">4</span> * <span class="hljs-number">4</span>, <span class="hljs-number">4</span> * <span class="hljs-number">2</span>);
    <span class="hljs-comment">// 启用变量</span>
    gl.enableVertexAttribArray(positionLocation);
    gl.enableVertexAttribArray(textureCoordLocation);
    <span class="hljs-comment">// 用三角带扇绘制矩形</span>
    gl.drawElements(gl.TRIANGLE_STRIP, <span class="hljs-number">4</span>, gl.UNSIGNED_SHORT, <span class="hljs-number">0</span>);
&#125;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            