
---
title: '微信小程序为video设置第一帧为缩略图(已经修改为和视频等比大小)'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3db799b9d25a41959382e41828851f19~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 18:54:30 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3db799b9d25a41959382e41828851f19~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>逻辑：在选择视频后获取视频尺寸然后在画图
记录代码</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">view</span>  <span class="hljs-attr">style</span>=<span class="hljs-string">"display: inline-block;visibility:hidden; width: 300px; height: 200px;position:absolute;left:-999rpx; "</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">canvas</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"cvs1"</span> <span class="hljs-attr">canvas-id</span>=<span class="hljs-string">"mycanvas"</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"2d"</span> <span class="hljs-attr">style</span>=<span class="hljs-string">"display: inline-block;border: 1px solid #CCC; width: 300px; height: &#123;&#123;h&#125;&#125;px;"</span>></span><span class="hljs-tag"></<span class="hljs-name">canvas</span>></span>
<span class="hljs-tag"></<span class="hljs-name">view</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">let</span> w = <span class="hljs-number">300</span>
<span class="hljs-keyword">let</span> h = <span class="hljs-number">200</span>
<span class="hljs-function"><span class="hljs-title">chooseVideo</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">let</span> that = <span class="hljs-built_in">this</span>;
    <span class="hljs-comment">// wx.compressVideo(&#123;</span>

    <span class="hljs-comment">// &#125;)</span>
    wx.chooseVideo(&#123;
      <span class="hljs-attr">sourceType</span>: [<span class="hljs-string">'album'</span>, <span class="hljs-string">'camera'</span>],
      <span class="hljs-attr">maxDuration</span>: <span class="hljs-number">60</span>,
      <span class="hljs-attr">camera</span>: <span class="hljs-string">'back'</span>,
      <span class="hljs-attr">success</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">res</span>) </span>&#123;
        <span class="hljs-comment">// let image = res.thumbTempFilePath;</span>
        <span class="hljs-built_in">console</span>.log(res);
        h = res.height;
        w = res.width;
        <span class="hljs-built_in">console</span>.log(h,w)
        that.setData(&#123;
          <span class="hljs-string">'publishInfo.video_thumb'</span>: <span class="hljs-string">''</span>,
          <span class="hljs-string">'publishInfo.url'</span>: <span class="hljs-string">''</span>,
          <span class="hljs-attr">fileList</span>: []
        &#125;)
        wx.showLoading(&#123;
          <span class="hljs-attr">title</span>: <span class="hljs-string">'上传中，请稍等'</span>,
          <span class="hljs-attr">mask</span>:<span class="hljs-literal">true</span>
        &#125;)
        wx.getVideoInfo(&#123;
          <span class="hljs-attr">src</span>:res.tempFilePath,
          <span class="hljs-function"><span class="hljs-title">complete</span>(<span class="hljs-params">res</span>)</span>&#123;
            <span class="hljs-built_in">console</span>.log(res)
          &#125;
        &#125;)
        that.upload(res.tempFilePath).then(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
          that.setData(&#123;
            <span class="hljs-attr">src</span>: <span class="hljs-built_in">JSON</span>.parse(res.data).message
          &#125;, <span class="hljs-function">() =></span> &#123;
            wx.showLoading(&#123;
              <span class="hljs-attr">title</span>: <span class="hljs-string">'设置缩略图中'</span>,
              <span class="hljs-attr">mask</span>:<span class="hljs-literal">true</span>
            &#125;)
          &#125;)
          <span class="hljs-comment">// that.data.fileList.push(&#123;</span>
          <span class="hljs-comment">//   url: image</span>
          <span class="hljs-comment">// &#125;);</span>
          that.setData(&#123;
            <span class="hljs-string">'publishInfo.url'</span>: (<span class="hljs-built_in">JSON</span>.parse(res.data).message),
          &#125;)
        &#125;);
      &#125;
    &#125;)
  &#125;,
<span class="hljs-function"><span class="hljs-title">play</span>(<span class="hljs-params">e</span>)</span> &#123;
    <span class="hljs-built_in">this</span>.draw()
  &#125;,
  <span class="hljs-function"><span class="hljs-title">draw</span>(<span class="hljs-params"></span>)</span> &#123;
    <span class="hljs-keyword">let</span> that = <span class="hljs-built_in">this</span>;
    <span class="hljs-keyword">const</span> dpr = wx.getSystemInfoSync().pixelRatio
    wx.createSelectorQuery().select(<span class="hljs-string">'#video'</span>).context(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
      <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'select video'</span>, res)
      <span class="hljs-keyword">const</span> video = <span class="hljs-built_in">this</span>.video = res.context

      wx.createSelectorQuery().selectAll(<span class="hljs-string">'#cvs1'</span>).node(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'select canvas'</span>, res)
        <span class="hljs-keyword">const</span> ctx1 = res[<span class="hljs-number">0</span>].node.getContext(<span class="hljs-string">'2d'</span>)
        res[<span class="hljs-number">0</span>].node.width = w * dpr
        res[<span class="hljs-number">0</span>].node.height = h * dpr
        <span class="hljs-comment">// setInterval(() => &#123;</span>
        ctx1.drawImage(video, <span class="hljs-number">0</span>, <span class="hljs-number">0</span>, w * dpr, h * dpr);
        <span class="hljs-comment">// ctx1.draw(true)</span>
        wx.canvasToTempFilePath(&#123;
          <span class="hljs-attr">x</span>: <span class="hljs-number">0</span>,
          <span class="hljs-attr">y</span>: <span class="hljs-number">0</span>,
          <span class="hljs-attr">width</span>: w * dpr,
          <span class="hljs-attr">height</span>: h * dpr,
          <span class="hljs-attr">destWidth</span>: w * dpr,
          <span class="hljs-attr">destHeight</span>: h * dpr,
          <span class="hljs-attr">canvas</span>: res[<span class="hljs-number">0</span>].node,
          <span class="hljs-function"><span class="hljs-title">success</span>(<span class="hljs-params">e</span>)</span> &#123;

            that.upload(e.tempFilePath).then(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
              <span class="hljs-built_in">console</span>.log(res)
              that.data.fileList.push(&#123;
                <span class="hljs-attr">url</span>: <span class="hljs-built_in">JSON</span>.parse(res.data).message
              &#125;);

              <span class="hljs-comment">// that.setData(&#123;</span>
              <span class="hljs-comment">//   res11:e.tempFilePath</span>
              <span class="hljs-comment">// &#125;)</span>
              that.setData(&#123;
                <span class="hljs-attr">fileList</span>: that.data.fileList,
                <span class="hljs-string">'publishInfo.video_thumb'</span>:<span class="hljs-built_in">JSON</span>.parse(res.data).message
              &#125;)
            &#125;);
          &#125;,
          <span class="hljs-function"><span class="hljs-title">complete</span>(<span class="hljs-params">e</span>)</span> &#123;
            <span class="hljs-built_in">console</span>.log(e)
            wx.hideLoading(&#123;
              <span class="hljs-attr">complete</span>: <span class="hljs-function">(<span class="hljs-params">res</span>) =></span> &#123;&#125;,
            &#125;)
          &#125;
        &#125;)
      &#125;).exec()
    &#125;).exec()
  &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
<p>缺点因为无法动态获取视频的实际大小所以只能给个固定的宽高</p>
<p>更新：实现途中遇到的坑
1、真机调试时会报这样的错（只有真机调试是会出现）
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3db799b9d25a41959382e41828851f19~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer">
2、第二个坑 （结果是在电脑模拟机上面运行正常、真机每一次第一次上传视频都无法获取封面、第二次以及之后都可以） 在调用画布和视频时才会对画布和视频进行初始化 所以要提前执行一次然后、在需要的时候设置封面
<strong>代码</strong></p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-function"><span class="hljs-title">play</span>(<span class="hljs-params">e</span>)</span> &#123;
    <span class="hljs-keyword">if</span>(<span class="hljs-built_in">this</span>.data.publishInfo.type == <span class="hljs-number">2</span>)&#123;
      <span class="hljs-built_in">this</span>.draw();
      <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">()=></span>&#123;
        <span class="hljs-built_in">this</span>.draw(<span class="hljs-number">1</span>);
      &#125;,<span class="hljs-number">500</span>)
    &#125;
  &#125;,
  <span class="hljs-function"><span class="hljs-title">draw</span>(<span class="hljs-params">b</span>)</span> &#123;
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"bbbb"</span>,b)
    <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =></span> &#123;

      <span class="hljs-keyword">let</span> that = <span class="hljs-built_in">this</span>;
      <span class="hljs-keyword">let</span> ctx;
      <span class="hljs-keyword">const</span> dpr = wx.getSystemInfoSync().pixelRatio
      wx.createSelectorQuery().select(<span class="hljs-string">'#video'</span>).context(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
        <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'select video'</span>, res)
        <span class="hljs-keyword">const</span> video = <span class="hljs-built_in">this</span>.video = res.context

        wx.createSelectorQuery().selectAll(<span class="hljs-string">'#cvs1'</span>).node(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
          <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'select canvas'</span>, res)
          <span class="hljs-keyword">const</span> ctx1 = res[<span class="hljs-number">0</span>].node.getContext(<span class="hljs-string">'2d'</span>)
          ctx = res[<span class="hljs-number">0</span>].node;
          res[<span class="hljs-number">0</span>].node.width = w * dpr
          res[<span class="hljs-number">0</span>].node.height = h * dpr
          <span class="hljs-comment">// setInterval(() => &#123;</span>
          ctx1.drawImage(video, <span class="hljs-number">0</span>, <span class="hljs-number">0</span>, w * dpr, h * dpr);
          <span class="hljs-comment">// ctx1.draw(true)</span>
         
          <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =></span> &#123;
            wx.canvasToTempFilePath(&#123;
              <span class="hljs-attr">x</span>: <span class="hljs-number">0</span>,
              <span class="hljs-attr">y</span>: <span class="hljs-number">0</span>,
              <span class="hljs-attr">width</span>: w * dpr,
              <span class="hljs-attr">height</span>: h * dpr,
              <span class="hljs-attr">destWidth</span>: w * dpr,
              <span class="hljs-attr">destHeight</span>: h * dpr,
              <span class="hljs-attr">canvas</span>: ctx,
              <span class="hljs-function"><span class="hljs-title">success</span>(<span class="hljs-params">e</span>)</span> &#123;
                <span class="hljs-keyword">if</span>(b == <span class="hljs-number">1</span>)&#123;
                  that.upload(e.tempFilePath).then(<span class="hljs-function"><span class="hljs-params">res</span> =></span> &#123;
                    <span class="hljs-built_in">console</span>.log(res)
                    that.data.fileList = [];
                    that.data.fileList.push(&#123;
                      <span class="hljs-attr">url</span>: <span class="hljs-built_in">JSON</span>.parse(res.data).message
                    &#125;);
  
                    <span class="hljs-comment">// that.setData(&#123;</span>
                    <span class="hljs-comment">//   res11:e.tempFilePath</span>
                    <span class="hljs-comment">// &#125;)</span>
                    that.setData(&#123;
                      <span class="hljs-attr">fileList</span>: that.data.fileList,
                      <span class="hljs-string">'publishInfo.video_thumb'</span>: <span class="hljs-built_in">JSON</span>.parse(res.data).message
                    &#125;)
                    wx.hideLoading(&#123;
                      <span class="hljs-attr">complete</span>: <span class="hljs-function">(<span class="hljs-params">res</span>) =></span> &#123;&#125;,
                    &#125;)
                  &#125;);
                &#125;
               
              &#125;,
              <span class="hljs-function"><span class="hljs-title">complete</span>(<span class="hljs-params">e</span>)</span> &#123;
                <span class="hljs-built_in">console</span>.log(e)
            
              &#125;
            &#125;)
          &#125;)
        &#125;).exec()
      &#125;).exec()
    &#125;)

  &#125;,
<span class="copy-code-btn">复制代码</span></code></pre>
<p>3、第三个坑就是wxml 的样式导致无法截图成功 这样就好多调试测试了
这样写是因为 我只要截图的效果 并没有想让在其他地方显示</p>
<pre><code class="hljs language-html copyable" lang="html"><span class="hljs-tag"><<span class="hljs-name">view</span> <span class="hljs-attr">style</span>=<span class="hljs-string">"position:absolute;top:0;left:-9999rpx"</span>></span>
 <span class="hljs-tag"><<span class="hljs-name">video</span> <span class="hljs-attr">style</span>=<span class="hljs-string">""</span> <span class="hljs-attr">autoplay</span> <span class="hljs-attr">muted</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"video"</span> <span class="hljs-attr">autoplay</span>=<span class="hljs-string">"&#123;&#123;true&#125;&#125;"</span> <span class="hljs-attr">controls</span>=<span class="hljs-string">"&#123;&#123;false&#125;&#125;"</span> <span class="hljs-attr">style</span>=<span class="hljs-string">"width: 300px; height: 200px;"</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"&#123;&#123;src&#125;&#125;"</span> <span class="hljs-attr">bindplay</span>=<span class="hljs-string">"play"</span> ></span><span class="hljs-tag"></<span class="hljs-name">video</span>></span>
<span class="hljs-tag"><<span class="hljs-name">view</span> <span class="hljs-attr">style</span>=<span class="hljs-string">"display: inline-block; width: 300px; height: 200px;"</span>></span>
    <span class="hljs-tag"><<span class="hljs-name">canvas</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"cvs1"</span> <span class="hljs-attr">canvas-id</span>=<span class="hljs-string">"mycanvas"</span> <span class="hljs-attr">type</span>=<span class="hljs-string">"2d"</span> <span class="hljs-attr">style</span>=<span class="hljs-string">"display: inline-block; border: 1px solid #CCC; width: 300px; height: &#123;&#123;h&#125;&#125;px;"</span>></span><span class="hljs-tag"></<span class="hljs-name">canvas</span>></span>
<span class="hljs-tag"></<span class="hljs-name">view</span>></span>
<span class="hljs-tag"></<span class="hljs-name">view</span>></span>
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            