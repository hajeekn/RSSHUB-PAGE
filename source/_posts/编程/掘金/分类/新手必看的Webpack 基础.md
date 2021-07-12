
---
title: '新手必看的Webpack 基础'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=5061'
author: 掘金
comments: false
date: Mon, 12 Jul 2021 01:45:13 GMT
thumbnail: 'https://picsum.photos/400/300?random=5061'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p><strong>webpack 是什么呢？有什么用呢？</strong></p>
<p>1.是前端资源模块化管理和打包工具。</p>
<p>2.可以使前端开发更加模块化。详细来讲就是：将松散的模块按依赖、规则打包成符合当前环境部署的前端资源；按需（异步）加载；通过loader转换，任何资源都可视作模块，比如 CommonJS、AMD、ES6、JSON、LESS、图片等。</p>
<p><strong>webpack 常见的一些名词解释：</strong></p>
<ul>
<li>chunk ：打包后的代码块。包含多个module，存在于webpack处理过程中的阶段。不是所有的chuncks都会成为最终的输出文件。</li>
<li>bundle：由一个或许多不同的chuncks生成，包含源码处理后的最终版本。</li>
<li>module：是webpack支持解析的模块。</li>
<li>runtime：模块交互时，链接模块所需的加载和解析逻辑。</li>
</ul>
<h2 data-id="heading-0">核心概念 ：1. 入口  2. 输出  3. loader  4. 插件</h2>
<p><strong>一、入口</strong>：
入口可以被认为是根上下文 或 app第一个启动文件。</p>
<p><strong>语法：</strong></p>
<ol>
<li>
<p>单个入口语法 entry: string | Array ， 向entry传入一个数组将会创建多个主入口（会由多个彼此分离的依赖图）。</p>
</li>
<li>
<p>对象语法 entry: &#123; [ entryChunkName : string ]: string | Array  &#125;，繁琐但可扩展度高。</p>
</li>
</ol>
<p>多入口场景：1.分离 应用程序 和 公共库。2.多个页面应用程序。</p>
<p><code>注意：不推荐在 library 中使用数组作为 entry。</code></p>
<p><strong>二、输出</strong>：
即使可以存在多个入口起点，但只指定一个输出配置。</p>
<p><strong>语法：</strong>
output: &#123; filename : string &#125;，如果多个入口，应使用占位符来确保每个文件具有唯一的名称，eg: filename: '[name].js'。</p>
<p><strong>三、模式 mode</strong>： 告知webpack使用相应模式的内置优化模式。</p>
<p><strong>语法：</strong>
mode: string，默认为 'production'，应使用占位符来确保每个文件具有唯一的名称，eg: filename: '[name].js'。</p>
<p><strong>参数：</strong></p>
<p><strong>1.development</strong>：开发环境。</p>
<p>会将 DefinePlugin 中 process.env.NODE_ENV 的值设置为 development. 为模块和 chunk 启用有效的名。启用 NamedChunksPlugin 和 NamedModulesPlugin。</p>
<p><strong>2.production</strong>:  生产环境。</p>
<p>启用 FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, ModuleConcatenationPlugin, NoEmitOnErrorsPlugin, OccurrenceOrderPlugin, SideEffectsFlagPlugin 和 UglifyJsPlugin</p>
<p><strong>四、插件 plugin</strong>： 旨在解决 loader 无法实现的其他事。</p>
<p>插件是一个具有 apply 属性的js 对象。plugins 参数中传入new实例。</p>
<h2 data-id="heading-1">其他常用配置</h2>
<p><strong>一、loader</strong>：
用于对模块的源代码进行转换。在 import 或 "load(加载)" 模块时预处理文件。</p>
<p><strong>为什么需要loader 呢？</strong>
因为集成的模块都需要转变为 js 可识别与运行的代码。</p>
<p><strong>语法：</strong>  test属性：用于标识出应该被对应的 loader 进行转换的某个或某些文件；use属性：表示进行转换时，应该使用哪个 loader。 eg：&#123; test: /.css$/, use: 'css-loader' &#125;,</p>
<p><strong>二、resolve</strong>： 配置模块如何解析。</p>
<p><strong>为什么需要loader 呢？</strong>
因为集成的模块都需要转变为 js 可识别与运行的代码。</p>
<p><strong>语法：</strong>  resolve: &#123; object &#125;</p>
<p><strong>常见属性：</strong></p>
<ol>
<li>
<p>extensions：自动解析确定的扩展。默认值为 ['.wasm', '.mjs', '.js', '.json']</p>
</li>
<li>
<p>alias：创建 import 或 require 的别名，来确保模块引入变得更简单。 eg：alias:&#123;'SRC': path.join(__dirname, '..', "src")&#125;</p>
</li>
<li>
<p>module：包含的选项决定了如何处理项目中的不同类型的模块。</p>
<p>常见属性：rules，属性为 test, include, exclude 和 resource等组成的对象数组。</p>
</li>
</ol></div>  
</div>
            