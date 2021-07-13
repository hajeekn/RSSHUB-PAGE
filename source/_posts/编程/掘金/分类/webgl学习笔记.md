
---
title: 'webgl学习笔记'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/accef683c5064c9ea46cf4d26fb16d91~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 19:47:22 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/accef683c5064c9ea46cf4d26fb16d91~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>缓冲区类型
1、顶点缓冲区（ARRAY_BUFFER）
2、索引缓冲区（ELEMENT_ARRAY_BUFFER）
3、纹理
4、帧缓冲（可能包含深度缓冲区）
5、深度缓冲区
6、颜色缓冲区
7、模板缓冲区</p>
<p>矩阵
1、模型矩阵
2、观察矩阵
3、投影矩阵
4、视口</p>
<p>opengl 纯可编程式管线技术
创建main  往main插入代码 然后 编译代码 创建进程 把编译好的main放入进程 链接进程 使用进程</p>
<p>创建一个缓冲区</p>
<pre><code class="hljs language-js copyable" lang="js"><!DOCTYPE html>
<span class="xml"><span class="hljs-tag"><<span class="hljs-name">html</span> <span class="hljs-attr">lang</span>=<span class="hljs-string">"en"</span>></span>

<span class="hljs-tag"><<span class="hljs-name">head</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">meta</span> <span class="hljs-attr">charset</span>=<span class="hljs-string">"UTF-8"</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">meta</span> <span class="hljs-attr">http-equiv</span>=<span class="hljs-string">"X-UA-Compatible"</span> <span class="hljs-attr">content</span>=<span class="hljs-string">"IE=edge"</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">meta</span> <span class="hljs-attr">name</span>=<span class="hljs-string">"viewport"</span> <span class="hljs-attr">content</span>=<span class="hljs-string">"width=device-width, initial-scale=1.0"</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">title</span>></span>Document<span class="hljs-tag"></<span class="hljs-name">title</span>></span>
<span class="hljs-tag"></<span class="hljs-name">head</span>></span>

<span class="hljs-tag"><<span class="hljs-name">body</span> <span class="hljs-attr">onload</span>=<span class="hljs-string">"initLoad()"</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">canvas</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"myCanvas"</span>></span><span class="hljs-tag"></<span class="hljs-name">canvas</span>></span>
<span class="hljs-tag"></<span class="hljs-name">body</span>></span>
<span class="hljs-tag"><<span class="hljs-name">script</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"vertexShader"</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"x-shader/x_vertex"</span>></span><span class="javascript">
    attribute vec3 v3Position;
    <span class="hljs-keyword">void</span> <span class="hljs-function"><span class="hljs-title">main</span>(<span class="hljs-params"><span class="hljs-keyword">void</span></span>)</span>
    &#123;
        gl_Position = vec4(v3Position,<span class="hljs-number">1.0</span>);
    &#125;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>
<span class="hljs-tag"><<span class="hljs-name">script</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"fragmentShader"</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"x-shader/x_fragment"</span>></span><span class="javascript">
    <span class="hljs-keyword">void</span> <span class="hljs-function"><span class="hljs-title">main</span>(<span class="hljs-params"><span class="hljs-keyword">void</span></span>)</span>
    &#123;
        gl_FragColor = vec4(<span class="hljs-number">0.0</span>,<span class="hljs-number">1.0</span>,<span class="hljs-number">1.0</span>,<span class="hljs-number">1.0</span>);
    &#125;
</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"><<span class="hljs-name">script</span>></span><span class="javascript">
    <span class="hljs-keyword">var</span> VSHADER_SOURCE =
        <span class="hljs-string">"attribute vec4 v3Position;"</span> +
        <span class="hljs-string">"void main() &#123;"</span> +
        <span class="hljs-comment">//设置坐标</span>
        <span class="hljs-string">"gl_Position = v3Position; "</span> +
        <span class="hljs-string">"&#125; "</span>;
    <span class="hljs-keyword">var</span> FSHADER_SOURCE =
        <span class="hljs-string">"void main() &#123;"</span> +
        <span class="hljs-comment">//设置颜色</span>
        <span class="hljs-string">"gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);"</span> +
        <span class="hljs-string">"&#125;"</span>;
    <span class="hljs-keyword">var</span> webgl
    <span class="hljs-keyword">var</span> programObject
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">initLoad</span>(<span class="hljs-params"></span>) </span>&#123;
        <span class="hljs-keyword">var</span> v3PositionIndex = <span class="hljs-number">0</span>;

        <span class="hljs-keyword">var</span> canvas = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'myCanvas'</span>);
        webgl = canvas.getContext(<span class="hljs-string">'webgl'</span>);
        webgl.viewport(<span class="hljs-number">0</span>, <span class="hljs-number">0</span>, canvas.clientWidth, canvas.clientHeight);
        <span class="hljs-comment">// 向显卡传递要执行的代码</span>
        <span class="hljs-comment">// 初始化类似创建了一个main</span>
        <span class="hljs-comment">// 创建顶点着色器对象</span>
        <span class="hljs-keyword">var</span> vertexShaderObject = webgl.createShader(webgl.VERTEX_SHADER);
        <span class="hljs-comment">// 创建片元着色器对象</span>
        <span class="hljs-keyword">var</span> fragmentShaderObject = webgl.createShader(webgl.FRAGMENT_SHADER);
        <span class="hljs-comment">// 像main函数里插入代码</span>
        webgl.shaderSource(vertexShaderObject, VSHADER_SOURCE)
        webgl.shaderSource(fragmentShaderObject, FSHADER_SOURCE)
        <span class="hljs-comment">// 编译代码</span>
        webgl.compileShader(vertexShaderObject);
        webgl.compileShader(fragmentShaderObject);
        <span class="hljs-keyword">if</span> (!webgl.getShaderParameter(vertexShaderObject, webgl.COMPILE_STATUS)) &#123;
            <span class="hljs-comment">// 获取vertexShaderObject的编译状态</span>
            alert(<span class="hljs-string">"error:vertexShaderObject"</span>);
        &#125;
        <span class="hljs-keyword">if</span> (!webgl.getShaderParameter(fragmentShaderObject, webgl.COMPILE_STATUS)) &#123;
            <span class="hljs-comment">// 获取fragmentShaderObject的编译状态</span>
            alert(<span class="hljs-string">"error:fragmentShaderObject"</span>);
        &#125;
        <span class="hljs-comment">// 创建一个进程类似exe</span>
        programObject = webgl.createProgram();
        <span class="hljs-comment">// 向进程里传入编译好的程序</span>
        webgl.attachShader(programObject, vertexShaderObject);
        webgl.attachShader(programObject, fragmentShaderObject);
        <span class="hljs-comment">// 输入值</span>
        webgl.bindAttribLocation(programObject, v3PositionIndex, <span class="hljs-string">"v3Position"</span>);
        <span class="hljs-comment">// 链接生成一个真正的可执行程序</span>
        webgl.linkProgram(programObject)
        <span class="hljs-keyword">if</span> (!webgl.getProgramParameter(programObject, webgl.LINK_STATUS)) &#123;
            <span class="hljs-comment">// 获取fragmentShaderObject的编译状态</span>
            alert(<span class="hljs-string">"error:programObject"</span>);
        &#125;
        <span class="hljs-built_in">console</span>.log(webgl.getAttribLocation(programObject, <span class="hljs-string">'v3Position'</span>))
        <span class="hljs-comment">// glsl</span>
        <span class="hljs-comment">// 使用这个可执行程序</span>
        webgl.useProgram(programObject);
        <span class="hljs-comment">// 坐标</span>
        <span class="hljs-keyword">var</span> jsArrayData = [
            <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>,
            -<span class="hljs-number">1.0</span>, -<span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>,
            <span class="hljs-number">1.0</span>, -<span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>
        ]
        <span class="hljs-keyword">var</span> triangleBuffer = webgl.createBuffer(); <span class="hljs-comment">// 创建一个缓冲区</span>
        <span class="hljs-comment">// 绑定</span>
        webgl.bindBuffer(webgl.ARRAY_BUFFER, triangleBuffer);
        <span class="hljs-comment">// 给缓冲区绑定值和类型 第三个参数标识静态类型 </span>
        webgl.bufferData(webgl.ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>(jsArrayData), webgl.STATIC_DRAW); <span class="hljs-comment">// 如果经常要变化的话使用 DYNAMIC_DRAW</span>
        <span class="hljs-comment">// 偶尔变STREAM_DRAW 顶点缓冲区的三种类型</span>
        <span class="hljs-comment">// webgl.bindBuffer(webgl.ARRAY_BUFFER, triangleBuffer);</span>
        <span class="hljs-comment">//将缓冲区对象分配给v3PositionIndex变量</span>
        webgl.vertexAttribPointer(v3PositionIndex, <span class="hljs-number">3</span>, webgl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">0</span>, <span class="hljs-number">0</span>);
        <span class="hljs-comment">//连接v3PositionIndex变量与分配给它的缓冲区对象</span>
        webgl.enableVertexAttribArray(v3PositionIndex);
        <span class="hljs-comment">// 清除指定<画布>的颜色</span>
        webgl.clearColor(<span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>);

        <span class="hljs-comment">// 清空 <canvas></span>
        webgl.clear(webgl.COLOR_BUFFER_BIT);



        <span class="hljs-comment">// 要赋值的名称    类型就是几维度 变量的类型 是否规格化</span>
        webgl.drawArrays(webgl.TRIANGLES, <span class="hljs-number">0</span>, <span class="hljs-number">3</span>);
    &#125;


</span><span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"></<span class="hljs-name">html</span>></span>


<span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"></<span class="hljs-name">html</span>></span>

<span class="hljs-tag"></<span class="hljs-name">script</span>></span>

<span class="hljs-tag"></<span class="hljs-name">html</span>></span></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<h5 data-id="heading-0">顶点缓冲区</h5>
<pre><code class="hljs language-js copyable" lang="js">webgl.bufferData(webgl.ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>(jsArrayData), webgl.STATIC_DRAW);
webgl.bufferData(webgl.ARRAY_BUFFER,<span class="hljs-number">4</span> * <span class="hljs-number">9</span>, webgl.STATIC_DRAW); <span class="hljs-comment">// 字节</span>
<span class="hljs-comment">// 更新部分缓冲区 </span>
webgl.bufferSubData(webgl.ARRAY_BUFFER,<span class="hljs-number">2</span>,<span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>([]))
<span class="hljs-comment">// 修改从第二个字节开始修改成后面的内容</span>

<span class="copy-code-btn">复制代码</span></code></pre>
<h5 data-id="heading-1">索引缓冲区</h5>
<p>假如要绘制一个矩形的话 可以通过两个三角形拼接起来</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> v3PositionIndex = <span class="hljs-number">0</span>;
   <span class="hljs-keyword">var</span> VSHADER_SOURCE =
        <span class="hljs-string">"attribute vec3 v3Position;"</span> +
        <span class="hljs-string">"void main() &#123;"</span> +
        <span class="hljs-comment">//设置坐标</span>
        <span class="hljs-string">"gl_Position = vec4(v3Position,1.0); "</span> +
        <span class="hljs-string">"&#125; "</span>;
    <span class="hljs-keyword">var</span> FSHADER_SOURCE =
        <span class="hljs-string">"void main() &#123;"</span> +
        <span class="hljs-comment">//设置颜色</span>
        <span class="hljs-string">"gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);"</span> +
        <span class="hljs-string">"&#125;"</span>;
<span class="hljs-keyword">let</span> webgl = <span class="hljs-literal">null</span>;
<span class="hljs-keyword">let</span> programObject  = <span class="hljs-literal">null</span>;
<span class="hljs-keyword">var</span> canvas = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'myCanvas'</span>);
webgl = canvas.getContext(<span class="hljs-string">'webgl'</span>);
webgl.viewport(<span class="hljs-number">0</span>, <span class="hljs-number">0</span>, canvas.clientWidth, canvas.clientHeight);
<span class="hljs-keyword">var</span> vertexShaderObject = webgl.createShader(webgl.VERTEX_SHADER);
<span class="hljs-keyword">var</span> fragmentShaderObject = webgl.createShader(webgl.FRAGMENT_SHADER);
webgl.shaderSource(vertexShaderObject, VSHADER_SOURCE)
webgl.shaderSource(fragmentShaderObject, FSHADER_SOURCE)
webgl.compileShader(vertexShaderObject);
webgl.compileShader(fragmentShaderObject);
programObject = webgl.createProgram();
webgl.attachShader(programObject, vertexShaderObject);
webgl.attachShader(programObject, fragmentShaderObject);
webgl.linkProgram(programObject);
webgl.useProgram(programObject);
webgl.bindAttribLocation(programObject, v3PositionIndex, <span class="hljs-string">"v3Position"</span>);
<span class="hljs-keyword">var</span> triangleBuffer = webgl.createBuffer();
<span class="hljs-keyword">var</span> jsArrayData2 = [
  -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      <span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      <span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
       -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
       <span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      -<span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>
]
webgl.bindBuffer(webgl.ARRAY_BUFFER, triangleBuffer);
webgl.bufferData(webgl.ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>(jsArrayData2), webgl.STATIC_DRAW);
webgl.vertexAttribPointer(v3PositionIndex, <span class="hljs-number">3</span>, webgl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">0</span>, <span class="hljs-number">0</span>);
webgl.enableVertexAttribArray(v3PositionIndex);
webgl.clearColor(<span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>);
webgl.clear(webgl.COLOR_BUFFER_BIT);
webgl.drawArrays(webgl.TRIANGLES, <span class="hljs-number">0</span>, <span class="hljs-number">6</span>);
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/accef683c5064c9ea46cf4d26fb16d91~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer">
然后矩形就画好了 但是 下面的那个用来绘图的float数组一个是4个字节 所有画矩形时需要向显卡传输<code>4*3*6字节的内容（72字节）</code>可以发现有些坐标是重复的 可以少写两个点<code>可以节省4*3*2个字节（24字节）</code>可以用到<code>索引缓冲区</code></p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> jsArrayData2 = [
  -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      <span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      <span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
       -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
       <span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      -<span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>
]
<span class="copy-code-btn">复制代码</span></code></pre>
<p>用法
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d90f430edd59432785f6a4ceaaad3314~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer">
可以看出这个矩形是由两个三角形<code>012和023构成的</code></p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> v3PositionIndex = <span class="hljs-number">0</span>;
   <span class="hljs-keyword">var</span> VSHADER_SOURCE =
        <span class="hljs-string">"attribute vec3 v3Position;"</span> +
        <span class="hljs-string">"void main() &#123;"</span> +
        <span class="hljs-comment">//设置坐标</span>
        <span class="hljs-string">"gl_Position = vec4(v3Position,1.0); "</span> +
        <span class="hljs-string">"&#125; "</span>;
    <span class="hljs-keyword">var</span> FSHADER_SOURCE =
        <span class="hljs-string">"void main() &#123;"</span> +
        <span class="hljs-comment">//设置颜色</span>
        <span class="hljs-string">"gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);"</span> +
        <span class="hljs-string">"&#125;"</span>;
<span class="hljs-keyword">let</span> webgl = <span class="hljs-literal">null</span>;
<span class="hljs-keyword">let</span> programObject  = <span class="hljs-literal">null</span>;
<span class="hljs-keyword">var</span> canvas = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'myCanvas'</span>);
webgl = canvas.getContext(<span class="hljs-string">'webgl'</span>);
webgl.viewport(<span class="hljs-number">0</span>, <span class="hljs-number">0</span>, canvas.clientWidth, canvas.clientHeight);
<span class="hljs-keyword">var</span> vertexShaderObject = webgl.createShader(webgl.VERTEX_SHADER);
<span class="hljs-keyword">var</span> fragmentShaderObject = webgl.createShader(webgl.FRAGMENT_SHADER);
webgl.shaderSource(vertexShaderObject, VSHADER_SOURCE)
webgl.shaderSource(fragmentShaderObject, FSHADER_SOURCE)
webgl.compileShader(vertexShaderObject);
webgl.compileShader(fragmentShaderObject);
programObject = webgl.createProgram();
webgl.attachShader(programObject, vertexShaderObject);
webgl.attachShader(programObject, fragmentShaderObject);
webgl.linkProgram(programObject);
webgl.useProgram(programObject);
webgl.bindAttribLocation(programObject, v3PositionIndex, <span class="hljs-string">"v3Position"</span>);

<span class="hljs-comment">// 修改的内容------</span>
<span class="hljs-comment">// 这里是矩形的四个点</span>
<span class="hljs-keyword">var</span> jsArrayData2 = [
  -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      <span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      <span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>,
      -<span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>
]
<span class="hljs-comment">// 索引数组</span>
<span class="hljs-keyword">var</span> indexArray = [
  <span class="hljs-number">0</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>,
  <span class="hljs-number">0</span>,<span class="hljs-number">2</span>,<span class="hljs-number">3</span>
]
<span class="hljs-comment">// ------</span>
<span class="hljs-keyword">var</span> triangleBuffer = webgl.createBuffer();
<span class="hljs-comment">// 创建一个索引缓冲区</span>
<span class="hljs-keyword">var</span> indexBuffer = webgl.createBuffer();
webgl.bindBuffer(webgl.ARRAY_BUFFER, triangleBuffer);
webgl.bufferData(webgl.ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>(jsArrayData2), webgl.STATIC_DRAW);
<span class="hljs-comment">// 操作索引缓冲区</span>
<span class="hljs-comment">// 把当前操作的缓冲区换成indexBuffer</span>
webgl.bindBuffer(webgl.ELEMENT_ARRAY_BUFFER, indexBuffer);
<span class="hljs-comment">// 赋值 注意这里只能使用无符号的短整型</span>
webgl.bufferData(webgl.ELEMENT_ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Uint16Array</span>(indexArray), webgl.STATIC_DRAW);
webgl.vertexAttribPointer(v3PositionIndex, <span class="hljs-number">3</span>, webgl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">0</span>, <span class="hljs-number">0</span>);
webgl.enableVertexAttribArray(v3PositionIndex);
webgl.clearColor(<span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>);
webgl.clear(webgl.COLOR_BUFFER_BIT);
<span class="hljs-comment">// 这里调用绘画的方法就要变了</span>
<span class="hljs-comment">// webgl.drawArrays(webgl.TRIANGLES, 0, 6);</span>
<span class="hljs-comment">// 第一个参数绘画的类型 ，第二个参数要话几个点 几个索引就一般就几个点 第三个索引值的类型 ，第四个参数是偏移值offset 从几个索引开始绘制</span>
webgl.drawElements(webgl.TRIANGLES, <span class="hljs-number">6</span>, webgl.UNSIGNED_SHORT, <span class="hljs-number">0</span>)
<span class="copy-code-btn">复制代码</span></code></pre>
<p>运行效果和上面一样
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e2b041de64ce4cba8bc73f64db74ef8a~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer">
渐变的矩形</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">var</span> v3PositionIndex = <span class="hljs-number">0</span>;
<span class="hljs-keyword">var</span> inColor = <span class="hljs-number">1</span>;
<span class="hljs-keyword">var</span> VSHADER_SOURCE =
   <span class="hljs-string">"precision lowp float;"</span> +
   <span class="hljs-string">"attribute vec3 v3Position;"</span> +
   <span class="hljs-string">"attribute vec4 inColor;"</span> +
   <span class="hljs-string">"varying vec4 outColor;"</span> +
   <span class="hljs-string">"void main() &#123;"</span> +
   <span class="hljs-comment">//设置坐标</span>
   <span class="hljs-string">"outColor= inColor;"</span> +
   <span class="hljs-string">"gl_Position = vec4(v3Position,1.0); "</span> +
   <span class="hljs-string">"&#125; "</span>;
<span class="hljs-keyword">var</span> FSHADER_SOURCE =
   <span class="hljs-string">"precision lowp float;"</span> +
   <span class="hljs-string">"varying vec4 outColor;"</span> +
   <span class="hljs-string">"void main() &#123;"</span> +
   <span class="hljs-comment">//设置颜色</span>
   <span class="hljs-string">"gl_FragColor = outColor;"</span> +
   <span class="hljs-string">"&#125;"</span>;
<span class="hljs-keyword">let</span> webgl = <span class="hljs-literal">null</span>;
<span class="hljs-keyword">let</span> programObject  = <span class="hljs-literal">null</span>;
<span class="hljs-keyword">var</span> canvas = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'myCanvas'</span>);
webgl = canvas.getContext(<span class="hljs-string">'webgl'</span>);
webgl.viewport(<span class="hljs-number">0</span>, <span class="hljs-number">0</span>, canvas.clientWidth, canvas.clientHeight);
<span class="hljs-keyword">var</span> vertexShaderObject = webgl.createShader(webgl.VERTEX_SHADER);
<span class="hljs-keyword">var</span> fragmentShaderObject = webgl.createShader(webgl.FRAGMENT_SHADER);
webgl.shaderSource(vertexShaderObject, VSHADER_SOURCE)
webgl.shaderSource(fragmentShaderObject, FSHADER_SOURCE)
webgl.compileShader(vertexShaderObject);
webgl.compileShader(fragmentShaderObject);
programObject = webgl.createProgram();
webgl.attachShader(programObject, vertexShaderObject);
webgl.attachShader(programObject, fragmentShaderObject);
webgl.linkProgram(programObject);
webgl.useProgram(programObject);
webgl.bindAttribLocation(programObject, v3PositionIndex, <span class="hljs-string">"v3Position"</span>);

<span class="hljs-comment">// 修改的内容------</span>
<span class="hljs-comment">// 这里是矩形的四个点</span>
   <span class="hljs-keyword">var</span> jsArrayData2 = [
            <span class="hljs-comment">// x,y,z,r,g,b,a</span>
            -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>,
            <span class="hljs-number">0.5</span>, <span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>,
            <span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">1.0</span>,
            -<span class="hljs-number">0.5</span>, -<span class="hljs-number">0.5</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>, <span class="hljs-number">1.0</span>,
        ]
<span class="hljs-comment">// 索引数组</span>
<span class="hljs-keyword">var</span> indexArray = [
  <span class="hljs-number">0</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>,
  <span class="hljs-number">0</span>,<span class="hljs-number">2</span>,<span class="hljs-number">3</span>
]
<span class="hljs-comment">// ------</span>
<span class="hljs-keyword">var</span> triangleBuffer = webgl.createBuffer();
<span class="hljs-comment">// 创建一个索引缓冲区</span>
<span class="hljs-keyword">var</span> indexBuffer = webgl.createBuffer();
webgl.bindBuffer(webgl.ARRAY_BUFFER, triangleBuffer);
webgl.bufferData(webgl.ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Float32Array</span>(jsArrayData2), webgl.STATIC_DRAW);
<span class="hljs-comment">// 操作索引缓冲区</span>
<span class="hljs-comment">// 把当前操作的缓冲区换成indexBuffer</span>
webgl.bindBuffer(webgl.ELEMENT_ARRAY_BUFFER, indexBuffer);
<span class="hljs-comment">// 赋值 注意这里只能使用无符号的短整型</span>
webgl.bufferData(webgl.ELEMENT_ARRAY_BUFFER, <span class="hljs-keyword">new</span> <span class="hljs-built_in">Uint16Array</span>(indexArray), webgl.STATIC_DRAW);
webgl.vertexAttribPointer(v3PositionIndex, <span class="hljs-number">3</span>, webgl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">4</span> * <span class="hljs-number">7</span>, <span class="hljs-number">0</span>);
webgl.vertexAttribPointer(inColor, <span class="hljs-number">4</span>, webgl.FLOAT, <span class="hljs-literal">false</span>, <span class="hljs-number">4</span> * <span class="hljs-number">7</span>, <span class="hljs-number">3</span> * <span class="hljs-number">4</span>);
webgl.enableVertexAttribArray(v3PositionIndex);
webgl.enableVertexAttribArray(inColor);
webgl.clearColor(<span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">0.0</span>, <span class="hljs-number">1.0</span>);
webgl.clear(webgl.COLOR_BUFFER_BIT);
<span class="hljs-comment">// 这里调用绘画的方法就要变了</span>
<span class="hljs-comment">// webgl.drawArrays(webgl.TRIANGLES, 0, 6);</span>
<span class="hljs-comment">// 第一个参数绘画的类型 ，第二个参数要话几个点 几个索引就一般就几个点 第三个索引值的类型 ，第四个参数是偏移值offset 从几个索引开始绘制</span>
webgl.drawElements(webgl.TRIANGLES, <span class="hljs-number">6</span>, webgl.UNSIGNED_SHORT, <span class="hljs-number">0</span>)
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/867043bc82574c478a0a8a1bbae65cf8~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-2">查看顶点着色器对象和片元着色器对象编译后的错误信息</h3>
<pre><code class="hljs language-js copyable" lang="js">     <span class="hljs-keyword">var</span> canvas = <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">'myCanvas'</span>);
        webgl = canvas.getContext(<span class="hljs-string">'webgl'</span>);
 <span class="hljs-keyword">if</span> (!webgl.getShaderParameter(vertexShaderObject, webgl.COMPILE_STATUS)) &#123;
            <span class="hljs-comment">// 获取vertexShaderObject的编译状态</span>
            <span class="hljs-keyword">var</span> err = webgl.getShaderInfoLog(vertexShaderObject)
            <span class="hljs-built_in">console</span>.log(err)
            alert(<span class="hljs-string">"error:vertexShaderObject"</span>);
        &#125;
        <span class="hljs-keyword">if</span> (!webgl.getShaderParameter(fragmentShaderObject, webgl.COMPILE_STATUS)) &#123;
            <span class="hljs-comment">// 获取fragmentShaderObject的编译状态</span>
            <span class="hljs-keyword">var</span> err = webgl.getShaderInfoLog(fragmentShaderObject)
            <span class="hljs-built_in">console</span>.log(err)
            alert(<span class="hljs-string">"error:fragmentShaderObject"</span>);
        &#125;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            