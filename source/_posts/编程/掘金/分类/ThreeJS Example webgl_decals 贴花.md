
---
title: 'ThreeJS Example webgl_decals 贴花'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/89e03b8de8724c3ab6b7c5ed4e643d49~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 08 Jul 2021 15:09:50 GMT
thumbnail: 'https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/89e03b8de8724c3ab6b7c5ed4e643d49~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fthreejs.org%2Fexamples%2F%23webgl_decals" target="_blank" rel="nofollow noopener noreferrer" title="https://threejs.org/examples/#webgl_decals" ref="nofollow noopener noreferrer">threejs.org/examples/#w…</a>
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/89e03b8de8724c3ab6b7c5ed4e643d49~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<ul>
<li>贴花材质</li>
</ul>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> decalMaterial = <span class="hljs-keyword">new</span> THREE.MeshPhongMaterial( &#123;
        <span class="hljs-attr">specular</span>: <span class="hljs-number">0x444444</span>,
        <span class="hljs-attr">map</span>: decalDiffuse,
        <span class="hljs-attr">normalMap</span>: decalNormal,
        <span class="hljs-attr">normalScale</span>: <span class="hljs-keyword">new</span> THREE.Vector2( <span class="hljs-number">1</span>, <span class="hljs-number">1</span> ),
        <span class="hljs-attr">shininess</span>: <span class="hljs-number">30</span>,
        <span class="hljs-attr">transparent</span>: <span class="hljs-literal">true</span>,
        <span class="hljs-attr">depthTest</span>: <span class="hljs-literal">true</span>,
        <span class="hljs-attr">depthWrite</span>: <span class="hljs-literal">false</span>, <span class="hljs-comment">//为什么深度写入为false</span>
        <span class="hljs-attr">polygonOffset</span>: <span class="hljs-literal">true</span>,
        <span class="hljs-attr">polygonOffsetFactor</span>: - <span class="hljs-number">4</span>,
        <span class="hljs-attr">wireframe</span>: <span class="hljs-literal">false</span>
&#125; );
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>白色线</li>
</ul>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> geometry = <span class="hljs-keyword">new</span> THREE.BufferGeometry();
geometry.setFromPoints( [ <span class="hljs-keyword">new</span> THREE.Vector3(), <span class="hljs-keyword">new</span> THREE.Vector3() ] );

line = <span class="hljs-keyword">new</span> THREE.Line( geometry, <span class="hljs-keyword">new</span> THREE.LineBasicMaterial() );
scene.add( line );
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>鼠标事件</li>
</ul>
<pre><code class="hljs language-js copyable" lang="js">raycaster = <span class="hljs-keyword">new</span> THREE.Raycaster();
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">checkIntersection</span>(<span class="hljs-params"> x, y </span>) </span>&#123;
        <span class="hljs-keyword">if</span> ( mesh === <span class="hljs-literal">undefined</span> ) <span class="hljs-keyword">return</span>;
        mouse.x = ( x / <span class="hljs-built_in">window</span>.innerWidth ) * <span class="hljs-number">2</span> - <span class="hljs-number">1</span>;
        mouse.y = - ( y / <span class="hljs-built_in">window</span>.innerHeight ) * <span class="hljs-number">2</span> + <span class="hljs-number">1</span>;
        raycaster.setFromCamera( mouse, camera );
        raycaster.intersectObject( mesh, <span class="hljs-literal">false</span>, intersects );
        <span class="hljs-keyword">if</span> ( intersects.length > <span class="hljs-number">0</span> ) &#123;
                <span class="hljs-keyword">const</span> p = intersects[ <span class="hljs-number">0</span> ].point;
                mouseHelper.position.copy( p );
                intersection.point.copy( p );
                <span class="hljs-keyword">const</span> n = intersects[ <span class="hljs-number">0</span> ].face.normal.clone();
                n.transformDirection( mesh.matrixWorld );
                n.multiplyScalar( <span class="hljs-number">10</span> );
                n.add( intersects[ <span class="hljs-number">0</span> ].point );
                intersection.normal.copy( intersects[ <span class="hljs-number">0</span> ].face.normal );
                mouseHelper.lookAt( n );
                <span class="hljs-keyword">const</span> positions = line.geometry.attributes.position;
                positions.setXYZ( <span class="hljs-number">0</span>, p.x, p.y, p.z );
                positions.setXYZ( <span class="hljs-number">1</span>, n.x, n.y, n.z );
                positions.needsUpdate = <span class="hljs-literal">true</span>;
                intersection.intersects = <span class="hljs-literal">true</span>;
                intersects.length = <span class="hljs-number">0</span>;
        &#125; <span class="hljs-keyword">else</span> &#123;
                intersection.intersects = <span class="hljs-literal">false</span>;
        &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>射击</li>
</ul>
<pre><code class="hljs language-js copyable" lang="js">position.copy( intersection.point ); <span class="hljs-comment">//位置</span>
orientation.copy( mouseHelper.rotation ); <span class="hljs-comment">//旋转方向</span>
<span class="hljs-keyword">if</span> ( params.rotate ) orientation.z = <span class="hljs-built_in">Math</span>.random() * <span class="hljs-number">2</span> * <span class="hljs-built_in">Math</span>.PI;
<span class="hljs-keyword">const</span> scale = params.minScale + <span class="hljs-built_in">Math</span>.random() * ( params.maxScale - params.minScale );
size.set( scale, scale, scale ); <span class="hljs-comment">//大小</span>
<span class="hljs-keyword">const</span> material = decalMaterial.clone();
material.color.setHex( <span class="hljs-built_in">Math</span>.random() * <span class="hljs-number">0xffffff</span> );
<span class="hljs-keyword">const</span> m = <span class="hljs-keyword">new</span> THREE.Mesh( <span class="hljs-keyword">new</span> DecalGeometry( mesh, position, orientation, size ), material ); <span class="hljs-comment">//方式</span>
decals.push( m );
scene.add( m );
<span class="copy-code-btn">复制代码</span></code></pre>
<ul>
<li>删除</li>
</ul>
<pre><code class="hljs language-js copyable" lang="js">decals.forEach( <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"> d </span>) </span>&#123;
        scene.remove( d );
&#125; );
decals.length = <span class="hljs-number">0</span>;
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            