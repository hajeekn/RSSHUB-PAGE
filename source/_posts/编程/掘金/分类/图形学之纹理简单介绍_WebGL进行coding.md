
---
title: '图形学之纹理简单介绍_WebGL进行coding'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cf3a62f6e58f41b38933e8f69e4dcd69~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 01:50:12 GMT
thumbnail: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cf3a62f6e58f41b38933e8f69e4dcd69~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>@charset "UTF-8";.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:14px;overflow-x:hidden;color:#353535&#125;.markdown-body h1&#123;padding-bottom:4px;font-size:30px&#125;.markdown-body h1,.markdown-body h2&#123;margin-top:36px;margin-bottom:10px;line-height:1.5;color:#005bb7&#125;.markdown-body h2&#123;position:relative;padding-left:16px;padding-right:10px;padding-bottom:10px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h2:before&#123;content:"「";position:absolute;top:-6px;left:-10px&#125;.markdown-body h2:after&#123;content:"」";position:absolute;top:6px;right:auto&#125;.markdown-body h3&#123;position:relative;padding-bottom:0;margin-top:30px;margin-bottom:10px;font-size:20px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body h3:before&#123;content:"»";padding-right:6px;color:#2196f3&#125;.markdown-body h4&#123;margin-top:24px;font-size:16px&#125;.markdown-body h4,.markdown-body h5&#123;padding-bottom:0;margin-bottom:10px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body h5&#123;margin-top:18px;font-size:14px&#125;.markdown-body h6&#123;padding-bottom:0;margin-top:12px;margin-bottom:10px;font-size:12px;line-height:1.5;color:#005bb7;padding-left:6px&#125;.markdown-body p&#123;line-height:inherit;margin-top:16px;margin-bottom:16px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;position:relative;width:98%;height:1px;margin-top:32px;margin-bottom:32px;background-image:linear-gradient(90deg,#007fff,rgba(255,0,0,.3),hsla(0,0%,100%,.1),rgba(255,0,0,.3),#007fff);border-width:0;overflow:visible&#125;.markdown-body hr:after&#123;content:"";position:absolute;margin:auto;left:0;right:0;bottom:0;top:0;display:inline-block;width:60px;height:20px;background:#fff;background-image:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAgCAYAAABgrToAAAADoklEQVRYR82XTYgcRRTHf2933Q1RjAa9eFO8JHoJ8RQVBQ2iBwXBET0YEUTXNVmNQtTpmeqaWV0XNRq/o4KoECSCEPSg4CF+BYUkIIiCoCJCPIhC/Ihh2Z0nVV27VnZnenumW9i6ddV7//frV69fVQurfMgq56NawFTPAU6QyomqXrw6wIZeyhCPebA5buNR+akKyGoAjd6BshthnYdSjqNcRVuOlIUsD2j0SuA94IwuMHdh5ZUykOUBXfSGbmKI54EtAeYIHSZoy5dl4JxvNYBOKdW1KE8BQ8AkVk6WhasWsAiN0TX9gveXQaPP+Aytpc4u+bMI06JNohsYYYYOR2lJWtS3OKDRfcAtQfgDoI6Vo4UCGb0OmAEuDvZvYmVbEd/igC3dzDz7gQu8sPA9kJDK27mBmjqBeLjTg90PDFOjWawFFQd06kZHEfaj3LAIpTRpSXsZ5E06zEYP9sDimnAApYaV2SLZG/wjMeqAkijwW4xQJ5Gf/ZzRC8OW3hiBTGGlURRswW55Bh/Ssxljrwew8l1PQaM14GngvGDzBUKdDsMeTtgU5o8B92PFlUf3YXUrHa7Fys6lBqcCGnX15YQ2A18FyPd7Crd1A3M8C1wdbH4DD3hWeP6IEXbQkG97ajR1HPFnuPP5jFFq1OWX7hl8WM9l1AO648uNfwLk7tytMeogty+xeQ4rO3r6bdcx1nuwOGsHmaXGtPzae4uzGnLH1kQkvpdZGrHjssBZJrL+pqS05KWc8tgITAPXRzYvYOXe/C2OV43eDcRBDtIhoS2f9wzc0Cv8Wls+zoFzUC5zF0U241h5uZtPfptp6OUM8wbK+cH5GEpCS17P3fJei0Z3+npTxryJ8CPzbKMtn/ZyWbkPGl0PuFPkmkjkcb4h4R2ZLwRq1H0ALmvjkf2HwK1Y+T1PY2XABe/sHJ6MxN5lnoSpnC/UGbsTaI5phK2R7x6s3Ffk5YoDOrWm3onwJHBmEP86bPmBrsGaenNoIdnxCH+gPEhLXi0Cl1VBvyPVLSh7gEuC62yAfOIUqabWEaaiucMIk6RyqJ+Q/QM69V26jjW86Gvov/EaoyT8zRCn+Xq7PVrbx0nuYUaO9wM3WAbjCE1NEUw09Um4UV+2OKfYfu5/S19gsAzGKqm6LE5FrShbdS0ku465DjDwKA/oQht19ejqbaEVuRbiLhuHByYLjtUAZpDutzP7cYdHsPJXWbjyNVgFwQoa1WXwf4Jd9YD/Ap80+yE7+u9aAAAAAElFTkSuQmCC);background-repeat:no-repeat;background-size:auto 100%;background-position-x:center&#125;.markdown-body code&#123;padding:.065em .4em;font-size:.87em;color:#c2185b;word-break:break-word;overflow-x:auto;background-color:#fff4f4;border-radius:2px&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;display:block;padding:16px 12px;margin:0;font-size:12px;color:#333;word-break:normal;overflow-x:auto;background:#f8f8f8&#125;.markdown-body pre>code::-webkit-scrollbar&#123;width:4px;height:4px&#125;.markdown-body pre>code::-webkit-scrollbar-track&#123;background-color:#bedcff&#125;.markdown-body pre>code::-webkit-scrollbar-thumb&#123;background-color:#2196f3;border-radius:10px&#125;.markdown-body a&#123;position:relative;text-decoration:none;color:#3da8f5;border-bottom:1px solid #bedcff&#125;.markdown-body a:hover&#123;color:#007fff;border-bottom-color:#007fff&#125;.markdown-body a:active&#123;color:#007fff&#125;.markdown-body a:after&#123;position:absolute;content:"";top:100%;left:0;width:100%;opacity:0;border-bottom:1px solid #bedcff;transition:top .3s,opacity .3s;transform:translateZ(0)&#125;.markdown-body a:hover:after&#123;top:0;opacity:1;border-bottom-color:#007fff&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #c3e0fd;border-spacing:0;border-collapse:collapse&#125;.markdown-body table thead&#123;color:#000;text-align:left;font-size:14px;background:#f6f6f6&#125;.markdown-body table tr:nth-child(2n)&#123;background-color:#f7fbff&#125;.markdown-body table tr:hover&#123;background-color:#e0edf7&#125;.markdown-body table td,.markdown-body table th&#123;padding:12px 8px;line-height:24px;border:1px solid #c3e0fd&#125;.markdown-body table th&#123;color:#005bb7;background-color:#dff0ff&#125;.markdown-body table td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#8c8c8c;border-left:4px solid #2196f3;background-color:#f0fdff;padding:1px 20px;margin:22px 0&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body b,.markdown-body blockquote>b,.markdown-body blockquote>strong,.markdown-body strong&#123;color:#2196f3&#125;.markdown-body em,.markdown-body i&#123;color:#4fc3f7&#125;.markdown-body del&#123;color:#ccc&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:4px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body details>summary&#123;outline:none;color:#005bb7;font-size:20px;font-weight:bolder;border-bottom:1px solid #bedcff;cursor:pointer&#125;.markdown-body details>p&#123;padding:10px 20px;margin:10px 0 0;color:#666;background-color:#f0fdff;border:2px dashed #2196f3&#125;.markdown-body h1::selection,.markdown-body h2::selection,.markdown-body h3::selection,.markdown-body h4::selection,.markdown-body h5::selection,.markdown-body h6::selection&#123;color:#005bb7;background-color:rgba(160,200,255,.15)&#125;.markdown-body p::selection&#123;color:#c80000&#125;.markdown-body a::selection,.markdown-body b::selection,.markdown-body del::selection,.markdown-body em::selection,.markdown-body i::selection,.markdown-body strong::selection&#123;background-color:transparent&#125;.markdown-body code::selection&#123;background-color:#ffeaeb&#125;.markdown-body pre>code::selection&#123;background-color:rgba(160,200,255,.25)&#125;.markdown-body ol ::selection,.markdown-body ul ::selection&#123;background-color:rgba(160,200,255,.15)&#125;.markdown-body .contains-task-list&#123;padding-left:14px;list-style:none&#125;.markdown-body .contains-task-list input[type=checkbox]&#123;position:relative&#125;.markdown-body .contains-task-list input[type=checkbox]:before&#123;content:"";position:absolute;top:0;left:0;right:0;bottom:0;width:inherit;height:inherit;background:#f0f8ff;border:1px solid #add6ff;border-radius:2px;box-sizing:border-box;z-index:1&#125;.markdown-body .contains-task-list input[type=checkbox]:checked:after&#123;content:"✓";position:absolute;top:-12px;left:0;right:0;bottom:0;width:0;height:0;color:#f55;font-size:20px;font-weight:700;z-index:2&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">背景</h1>
<p>本篇收录于<a href="https://juejin.cn/column/6966134135991566344" target="_blank" title="https://juejin.cn/column/6966134135991566344">《数据可视化和图形学》</a>专栏</p>
<p>首先Canvas 2D 和 WebGL上篇文章做了简单的对比,可以了解到WebGL的API相对来说比较难懂。所以我觉得后续的coding更多是采取WebGL来实现我们的效果(欸,就是玩~) 当然知识点还是从简单到复杂。。。如果一上来就介绍视觉物理,光照/全局光照,抗锯齿,延迟渲染,实时渲染....或许我创建专栏的初衷就丢掉了;当然如果有想深入讨论的可以私下交流。</p>
<blockquote>
<p>上文实现了简单的2d图形 <a href="https://juejin.cn/post/6981444627270205453" target="_blank" title="https://juejin.cn/post/6981444627270205453">有需要可以参考上文</a></p>
</blockquote>
<h2 data-id="heading-1">本篇大纲</h2>
<ol>
<li>什么是纹理?2d与3d纹理贴图区别?</li>
<li>纹理管线 The Texturing Pipeline</li>
<li>coding (WebGL中简单使用纹理)</li>
</ol>
<h3 data-id="heading-2">1. 什么是纹理?2d与3d纹理贴图区别?</h3>
<p>在计算机图形学中，纹理贴图（Texturing）是使用图像、函数或其他数据源来改变物体表面外观的技术。</p>
<h4 data-id="heading-3">2d纹理</h4>
<p>二维纹理(2D texture)是一张简单的位图图片，用于为三维模型提供表面点的颜色值</p>
<h4 data-id="heading-4">3d纹理</h4>
<p>三维纹理(3D texture)，可以被认为由很多张 2D 纹理组成，用于描述三维空间数据的图片。</p>
<h3 data-id="heading-5">2. 通用纹理管线 The Texturing Pipeline</h3>
<blockquote>
<p>渲染管线对于日常使用可能是个黑盒 但是理解这个对你的编程是有莫大的提高...(不懂也没关系本来这块介绍的也很浅 大部分从别的地方copy的. 哈哈)</p>
</blockquote>
<p>简单来说,纹理(Texturing)是一种针对物体表面属性进行“建模”的高效技术。图像纹理中的像素通常被称为纹素(Texels),区别于屏幕上的像素。</p>
<h4 data-id="heading-6">请看下图---单个纹理应用纹理贴图的详细过程</h4>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cf3a62f6e58f41b38933e8f69e4dcd69~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<ol>
<li>投射函数(projector function) 就是将空间中的三维点转化为纹理坐标，也就是获取表面的位置并将其投影到参数空间中。例如有球形、圆柱、以及平面投影相关的函数</li>
<li>映射函数（The Corresponder Function）的作用是将参数空间坐标（parameter-space coordinates）转换为纹理空间位置（texture space locations）。</li>
</ol>
</blockquote>
<ul>
<li>第一步。通过将 <strong>投影方程(projector function)</strong> 运用于空间中的点 ，从而得到一组称为<strong>参数空间值(parameter-space values)</strong> 的关于纹理的数值。</li>
<li>第二步。在使用这些新值访问纹理之前，可以使用一个或者多个<strong>映射函数(corresponder function)</strong> 将<strong>参数空间值(parameter-space values)</strong> 转换到纹理空间。</li>
<li>第三步。使用这些<strong>纹理空间值(texture-space locations)</strong> 从纹理中获取<strong>相应的值(obtain value)</strong> 。例如，可以使用图像纹理的数组索引来检索像素值。</li>
<li>第四步。再使用<strong>值变换函数(value transform function)</strong> 对检索结果进行值变换，最后使用得到的新来改变表面属性，如材质或者着色法线等等。</li>
</ul>
<p><em>法线/法向量相关知识需要自行补充 在图形学中非常重要(经常会见到)</em></p>
<h3 data-id="heading-7">coding (WebGL中简单使用纹理贴图2d)</h3>
<blockquote>
<p>简单用WebGL实现一个纹理(贴图),并通过一个矩阵进行动画(旋转) 插入的gif有点卡 大概示意...</p>
</blockquote>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f43cf09989a3403bb4ba6430b0417409~tplv-k3u1fbpfcp-watermark.image" alt="webgl2d.gif" loading="lazy" referrerpolicy="no-referrer"></p>
<h4 data-id="heading-8">1. shader编写 增加了纹理坐标 修改了顶点坐标(采用矩阵/旋转)</h4>
<pre><code class="copyable">//vertex shader
attribute vec4 a_position;
attribute vec2 a_texcoord;  

uniform mat4 u_matrix;

varying vec2 v_texcoord;

void main() &#123;
   gl_Position = u_matrix * a_position;
   // 纹理坐标传递
   v_texcoord = a_texcoord;
&#125;
// fragment shader
precision mediump float;

varying vec2 v_texcoord;

uniform sampler2D u_texture;

void main() &#123;
   gl_FragColor = texture2D(u_texture, v_texcoord);
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-9">2. 初始化context(渲染上下文) 以及 着色器程序</h4>
<pre><code class="copyable">var canvas = document.querySelector("#canvas");
var gl = canvas.getContext("webgl");
if (!gl) &#123;
    return;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-10">3. 初始设置GLSL程序并新增缓冲区(纹理)</h4>
<pre><code class="copyable">// 设置GLSL程序
  var program = webglUtils.createProgramFromScripts(gl, ["vertex-shader", "fragment-shader"]);
  // 获取顶点坐标需要绑定的地方
  var positionLocation = gl.getAttribLocation(program, "a_position");
  var texcoordLocation = gl.getAttribLocation(program, "a_texcoord");
  // 获取 uniforms
  var matrixLocation = gl.getUniformLocation(program, "u_matrix");
  var textureLocation = gl.getUniformLocation(program, "u_texture");
 
 
  // 创建缓冲区
  var positionBuffer = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
  var positions = [
    -1, -1,
    -1,  1,
     1, -1,
     1, -1,
    -1,  1,
     1,  1,
  ];
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(positions), gl.STATIC_DRAW);
  // 为纹理坐标创建缓冲区
  var texcoordBuffer = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, texcoordBuffer);
  var texcoords = [
    0, 0,
    0, 1,
    1, 0,
    1, 0,
    0, 1,
    1, 1,
  ];
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(texcoords), gl.STATIC_DRAW);
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-11">4. 创建并加载纹理</h4>
<pre><code class="copyable"> //解决图片跨域问题
 function requestCORSIfNotSameOrigin(img, url) &#123;
    if ((new URL(url, window.location.href)).origin !== window.location.origin) &#123;
      img.crossOrigin = "";
    &#125;
  &#125;
 // 创建一个纹理 &#123; width: w, height: h, texture: tex &#125;
 // 初始化1x1 px像素 图片加载完更新
 function loadImageAndCreateTextureInfo(url) &#123;
    var tex = gl.createTexture();
    gl.bindTexture(gl.TEXTURE_2D, tex);
    // Fill the texture with a 1x1 blue pixel.
    gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, 1, 1, 0, gl.RGBA, gl.UNSIGNED_BYTE,
                  new Uint8Array([0, 0, 255, 255]));

    // let's assume all images are not a power of 2
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR);

    var textureInfo = &#123;
      width: 1,   
      height: 1,
      texture: tex,
    &#125;;
    var img = new Image();
    img.addEventListener('load', function() &#123;
      textureInfo.width = img.width;
      textureInfo.height = img.height;

      gl.bindTexture(gl.TEXTURE_2D, textureInfo.texture);
      // 调用 texImage2D() 把已经加载的图片图形数据写到纹理
      gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, img);
      render()
    &#125;);
    requestCORSIfNotSameOrigin(img, url);
    img.src = url;

    return textureInfo;
&#125;
// 加载纹理
var texInfo = loadImageAndCreateTextureInfo('https://webglfundamentals.org/webgl/resources/leaves.jpg');
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-12">5. 绘制相关设置 纹理坐标并赋值矩阵坐标。 使用着色程序 绘制。</h4>
<pre><code class="copyable">function render(time) &#123;
    time *= 0.001; // time 加速度 旋转图片
    // 重新设置canvas大小
    webglUtils.resizeCanvasToDisplaySize(gl.canvas);

    // 裁剪像素区
    gl.viewport(0, 0, gl.canvas.width, gl.canvas.height);
    gl.clear(gl.COLOR_BUFFER_BIT);
    gl.bindTexture(gl.TEXTURE_2D, texInfo.texture);

    // 使用着色器程序
    gl.useProgram(program);

    // 设置参数，让我们可以绘制任何尺寸的图像
    gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
    gl.enableVertexAttribArray(positionLocation);
    gl.vertexAttribPointer(positionLocation, 2, gl.FLOAT, false, 0, 0);
    gl.bindBuffer(gl.ARRAY_BUFFER, texcoordBuffer);
    gl.enableVertexAttribArray(texcoordLocation);
    gl.vertexAttribPointer(texcoordLocation, 2, gl.FLOAT, false, 0, 0);

    var aspect = gl.canvas.clientWidth / gl.canvas.clientHeight;
    var matrix = m4.scaling(1, aspect, 1);  //可是试试将aspect 改为0.1看看效果 - -
    matrix = m4.zRotate(matrix, time);
    matrix = m4.scale(matrix, 0.5, 0.5, 1);
    // 设置矩阵
    gl.uniformMatrix4fv(matrixLocation, false, matrix);

    // 从第0个unit开始获取纹理
    gl.uniform1i(textureLocation, 0);

    // 绘制 (2 triangles, 6 vertices)
    gl.drawArrays(gl.TRIANGLES, 0, 6);

    requestAnimationFrame(render);
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<ol>
<li><code>webgl-utils.js</code> webgl相关函数封装工具库</li>
<li><code>m4.js</code>  矩阵相关数学函数库</li>
</ol>
<p>完整代码示例 <a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2FXieguoiang%2Fwebgl-learning%2Ftree%2Fmain%2F7-12-webgl2d" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/Xieguoiang/webgl-learning/tree/main/7-12-webgl2d" ref="nofollow noopener noreferrer">请点击git仓库查看代码示例</a></p>
</blockquote>
<h2 data-id="heading-13">2D渲染方面你可能需要了解的有</h2>
<ol>
<li>纹理缓存</li>
<li>纹理压缩</li>
<li>2D/2D纹理优化</li>
<li>渲染优化...</li>
</ol>
<h1 data-id="heading-14">最后</h1>
<blockquote>
<p>最后强烈希望大家学习相关理论知识;理论可能日常用到的地方很少,但是它能决定你走多远。(有的人问难怎么办,勤于练习吧),写作速度呢 该专栏我加速(一周1-2篇) 其他专栏(1篇) 计算机图形学相关的基础知识都会带一遍。然后后续主要写数据可视化方向。</p>
</blockquote></div>  
</div>
            