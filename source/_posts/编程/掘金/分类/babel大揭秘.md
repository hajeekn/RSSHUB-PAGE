
---
title: 'babel大揭秘'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e0a8a64c61034851bab0167ac0ada024~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Sun, 11 Jul 2021 19:38:46 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e0a8a64c61034851bab0167ac0ada024~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">babel分享</h3>
<h4 data-id="heading-1">babel介绍</h4>
<blockquote>
<p>js 转译器 es6 to es5 es7 to es5  简称 es typescript 代码转换 除了这些 我们还可以做一些 静态分析 eslint等</p>
</blockquote>
<p>babel 是源码 => 源码的过程</p>
<blockquote>
<p>babel 代码转换的过程分为三步</p>
</blockquote>
<pre><code class="copyable">  1. parse 代码 => ast
  2. transform 操作语法书 增删改 ast => ast (修改后的)
  3. generate 修改后的 ast => 新的代码
<span class="copy-code-btn">复制代码</span></code></pre>
<blockquote>
<p>ast 介绍</p>
</blockquote>
<pre><code class="copyable">    抽象语法书 （Abstract Syntax Tree，AST）以树形结构表达 编程语言 的语法
<span class="copy-code-btn">复制代码</span></code></pre>
<p>ast语法树 代码是从 经过词法分析 和 语法分析 最终生成ast
举一个例子
我是张三  词法分析的过程就相当于 <code>我</code>、<code>是</code>、<code>张三</code>
语法分析 <code>是</code> 一个赋值语句 <code>张三</code> 赋值给 <code>我</code></p>
<p><code>me = 'zhangsan'</code>
词法分析过程最终生成结果 token (不能再拆分的单词)
<code>me、= 、'zhangsan'</code>
语法分析的过程 发现 有一个等号（<code>operator</code> 操作符） 发现是赋值操作
left 是 me （标识符 <code>identifier</code>）<code>right</code> 是 (字符串字面量 <code>StringLiteral</code>) <code>'xiaomenggang '</code></p>
<ol>
<li>举个例子</li>
</ol>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fastexplorer.net%2F" target="_blank" rel="nofollow noopener noreferrer" title="https://astexplorer.net/" ref="nofollow noopener noreferrer">astexplorer.net/</a></p>
<p>javascript:</p>
<pre><code class="copyable">    console.log(1)
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e0a8a64c61034851bab0167ac0ada024~tplv-k3u1fbpfcp-watermark.image" alt="WX20210711-000224@2x.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4a61bc43892c47dea8896aca6a07f87e~tplv-k3u1fbpfcp-watermark.image" alt="WX20210711-000251@2x.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>他的树形结构是这样的</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/171503d104274cfc9356759c4ffb1c44~tplv-k3u1fbpfcp-watermark.image" alt="流程图.png" loading="lazy" referrerpolicy="no-referrer"></p>

<h5 data-id="heading-2">ast 常见节点</h5>
<blockquote>
<p>Literal 字面量
字符串字面量 StringLiteral， 例如 'xmg'
数字字面量 NumericLiteral, 例如 1
布尔字面量 BooleanLiteral , 例如 true or false
正则表达式字面量 RegExpLiteral , 例如 /^[0-9]/
Identifier 标识符</p>
</blockquote>
<p>Statement 语句</p>






























<table><thead><tr><th>代码</th><th>节点名称</th><th>中文名</th></tr></thead><tbody><tr><td>for</td><td>ForStatement</td><td>循环语句</td></tr><tr><td>while</td><td>WhileStatement</td><td>while语句</td></tr><tr><td>continue</td><td>ContinueStatement</td><td>continue语句</td></tr><tr><td>Switch</td><td>SwitchStatement</td><td>Switch语句</td></tr></tbody></table>
<blockquote>
<p>Declaration 声明语句</p>
</blockquote>






























<table><thead><tr><th>代码</th><th>节点名称</th><th>中文名</th></tr></thead><tbody><tr><td>var a = 'xmg';</td><td>variableDeclaratio</td><td>变量声明</td></tr><tr><td>function fn()&#123;&#125;</td><td>functionDeclaratio</td><td>函数声明</td></tr><tr><td>import d from 'e';</td><td>importDeclaratio</td><td>导出声明</td></tr><tr><td>Switch</td><td>SwitchStatement</td><td>Switch语句</td></tr></tbody></table>
<blockquote>
<p>Expression 表达式</p>
</blockquote>



































<table><thead><tr><th>代码</th><th>节点名称</th><th>中文名</th></tr></thead><tbody><tr><td>[1,2,3]</td><td>ArrayExpression</td><td>数组表达式</td></tr><tr><td>a = 1</td><td>AssignmentExpression</td><td>赋值表达式</td></tr><tr><td>1 + 2</td><td>BinaryExpression</td><td>二元表达式</td></tr><tr><td>funciton () &#123;&#125;</td><td>FunctionExpression</td><td>函数表达式</td></tr><tr><td>() => &#123;&#125;</td><td>ArrowFunctionExpression</td><td>箭头函数表达式</td></tr></tbody></table>
<p>超级微小编译器</p>
<p><a href="https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fjamiebuilds%2Fthe-super-tiny-compiler%2Fblob%2Fmaster%2Fthe-super-tiny-compiler.js" target="_blank" rel="nofollow noopener noreferrer" title="https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js" ref="nofollow noopener noreferrer">github.com/jamiebuilds…</a></p>
<p>简单的从 词法分析 到 语法分析的一个简单实现过程</p>
<h3 data-id="heading-3">我们先来看下babel 的api</h3>
<h5 data-id="heading-4">parse</h5>
<p>parse @babel/parser 将代码转换成 ast</p>
<p>参数 <code>plugin</code>，<code>souseType</code>（<code>script</code> script 则不解析 es module 语法 <code>module</code> 是解析 es module 语法 <code>unambiguous</code> 根据环境自动判断 ）</p>
<p>transform @babel/traverse 遍历AST 使用访问者 模式 对ast修改</p>
<p>traverse(ast, visitor)</p>
<pre><code class="copyable">visitor: &#123;
  StringLiteral(path) &#123;
    debugger
    console.log(path.node.value)
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>path 上面有很多方法
比如 path.node 当前节点
比如 path.parent 获取父级节点
path.insertBefore 向前插入
path.repalceWith 替换
path.remove 删除
path.stop 停止遍历</p>
<p>generate @babel/generate 将代码 从 ast 转成 code</p>
<p>@babel/types 提供快速生成 ast 和 断言的方法
创建 ast和判断ast的节点类型
比如 types.IfStatement()</p>
<pre><code class="copyable">if(1)&#123;&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<pre><code class="copyable">  types.ifStatement(types.NumericLiteral(1),types.blockStatement([]))
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>types.isIfStatement():boolean</code></p>
<h4 data-id="heading-5">我们再来做一个例子 删除console代码</h4>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> parser = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/parser'</span>);
<span class="hljs-keyword">const</span> traverse = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/traverse'</span>).default;
<span class="hljs-keyword">const</span> generate = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/generator'</span>).default;
<span class="hljs-keyword">const</span> types = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/types'</span>);


<span class="hljs-comment">// console.log(types.ifStatement(types.NumericLiteral(1),types.blockStatement([])))</span>
<span class="hljs-comment">// console.log(generate(types.ifStatement(types.NumericLiteral(1),types.blockStatement([]))))</span>

<span class="hljs-keyword">const</span> sourceCode = <span class="hljs-string">`
    console.log(1);
    function func() &#123;
        var a = 2
        console.info(a);
    &#125;
    export default class Clazz &#123;
        say() &#123;
            var b = 3
            console.debug(b);
        &#125;
        render() &#123;
            let bbb = 333
            console.log(bbb)
            return <div>&#123;bbb&#125;</div>
        &#125;
    &#125;
`</span>;

<span class="hljs-keyword">const</span> ast = parser.parse(sourceCode, &#123;
    <span class="hljs-attr">sourceType</span>: <span class="hljs-string">'unambiguous'</span>,
    <span class="hljs-attr">plugins</span>: [<span class="hljs-string">'jsx'</span>]
&#125;);

traverse(ast, &#123;
    <span class="hljs-function"><span class="hljs-title">StringLiteral</span>(<span class="hljs-params">path</span>)</span> &#123;
        <span class="hljs-keyword">debugger</span>
        <span class="hljs-built_in">console</span>.log(path)
    &#125;,
    <span class="hljs-function"><span class="hljs-title">CallExpression</span>(<span class="hljs-params">path</span>)</span> &#123;
        <span class="hljs-comment">// if(path.scope) &#123;</span>
        <span class="hljs-comment">//     path.scope.generateUid('maidian')</span>
        <span class="hljs-comment">//     console.log(path.scope.generateUid('maidian'))</span>
        <span class="hljs-comment">// &#125;</span>
        <span class="hljs-comment">// types.ifStatement</span>
        <span class="hljs-keyword">if</span> ( types.isMemberExpression(path.node.callee) 
            && path.node.callee.object.name === <span class="hljs-string">'console'</span> 
           ) &#123;
            path.remove()
        &#125;
    &#125;
&#125;);

<span class="hljs-keyword">const</span> &#123; code, map &#125; = generate(ast);
<span class="hljs-built_in">console</span>.log(code);
<span class="copy-code-btn">复制代码</span></code></pre>
<h4 data-id="heading-6">我们再来做一个例子 实现代码混淆</h4>
<p>我们要说下 path 上的 scope 是作用域信息 生成作用域的就是模块、函数、块
作用域之间会形成嵌套关系，也就是作用域链</p>
<p>scope.bindings 当前作用域内声明的所有变量</p>
<pre><code class="hljs language-js copyable" lang="js"><span class="hljs-keyword">const</span> parser = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/parser'</span>);
<span class="hljs-keyword">const</span> traverse = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/traverse'</span>).default;
<span class="hljs-keyword">const</span> generate = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/generator'</span>).default;
<span class="hljs-keyword">const</span> types = <span class="hljs-built_in">require</span>(<span class="hljs-string">'@babel/types'</span>);
<span class="hljs-keyword">let</span> num=<span class="hljs-number">0</span>;
<span class="hljs-keyword">const</span> string = <span class="hljs-string">`abcdefghigklsisysjsks`</span>

<span class="hljs-keyword">const</span> sourceCode = <span class="hljs-string">`
    function getScr() &#123;
        const num1 = 3
        const num3 = num1**num1
        const num5 = num3**num3
        function add () &#123;
            return num5 + num3
        &#125;
        const sum = add()
        return sum
    &#125;
`</span>;

<span class="hljs-keyword">const</span> ast = parser.parse(sourceCode, &#123;
    <span class="hljs-attr">sourceType</span>: <span class="hljs-string">'unambiguous'</span>,
&#125;);

traverse(ast, &#123;
    <span class="hljs-function"><span class="hljs-title">StringLiteral</span>(<span class="hljs-params">path</span>)</span> &#123;
        <span class="hljs-built_in">console</span>.log(path)
    &#125;,
    <span class="hljs-function"><span class="hljs-title">Scopable</span>(<span class="hljs-params">path, state</span>)</span> &#123;
        <span class="hljs-keyword">if</span>(path.scope.bindings) &#123;
            <span class="hljs-built_in">Object</span>.entries(path.scope.bindings).forEach(<span class="hljs-function">(<span class="hljs-params">[key,binding] </span>)=></span> &#123;
                binding.scope.rename(key,binding.scope.generateUid(string[num++]))
            &#125;)
        &#125;
    &#125;
&#125;);

<span class="hljs-keyword">const</span> &#123; code, map &#125; = generate(ast);
<span class="hljs-built_in">console</span>.log(code);
<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            