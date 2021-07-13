
---
title: 'flutter 学习笔记-容器与布局（1）'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://picsum.photos/400/300?random=5170'
author: 掘金
comments: false
date: Tue, 13 Jul 2021 01:52:07 GMT
thumbnail: 'https://picsum.photos/400/300?random=5170'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h1 data-id="heading-0">flutter 学习笔记-容器与布局（1）</h1>
<h3 data-id="heading-1">布局</h3>

























<table><thead><tr><th>Widget</th><th>对应的Element</th><th>用途</th></tr></thead><tbody><tr><td>LeafRenderObjectWidget</td><td>LeafRenderObjectElement</td><td>Widget树的叶子节点，用于没有子节点的widget，通常基础组件都属于这一类，如Image。</td></tr><tr><td>SingleChildRenderObjectWidget</td><td>SingleChildRenderObjectElement</td><td>包含一个子Widget，如：ConstrainedBox、DecoratedBox等</td></tr><tr><td>MultiChildRenderObjectWidget</td><td>MultiChildRenderObjectElement</td><td>包含多个子Widget，一般都有一个children参数，接受一个Widget数组。如Row、Column、Stack等</td></tr></tbody></table>
<h3 data-id="heading-2">Row、Column、Container、Expanded、Flex、DefaultTextStyle、SizeBox、Padding</h3>
<ul>
<li>Row 横排，对齐方法 CrossAxisAlignment，类似flex</li>
<li>Column 纵排</li>
<li>Container 为SingleChildRenderObjectWidget 只有一个child，类似div</li>
<li>Expanded 扩展 Row、Column、Container高度和宽度为100%</li>
<li>Flex 配合Expanded设置flex比例</li>
<li>DefaultTextStyle 的style参数可以设置所有文笔颜色样式</li>
<li>SizeBox 可以设置容器的大小，Containe 类似</li>
<li>Padding</li>
</ul>
<pre><code class="hljs language-dart copyable" lang="dart"><span class="hljs-keyword">import</span> <span class="hljs-string">'dart:async'</span>;
<span class="hljs-keyword">import</span> <span class="hljs-string">'dart:ffi'</span>;
<span class="hljs-keyword">import</span> <span class="hljs-string">'package:flutter/foundation.dart'</span>;
<span class="hljs-keyword">import</span> <span class="hljs-string">'package:flutter/material.dart'</span>;
<span class="hljs-keyword">import</span> <span class="hljs-string">'package:flutter/rendering.dart'</span>;
<span class="hljs-keyword">import</span> <span class="hljs-string">'view/header.dart'</span>;

<span class="hljs-keyword">void</span> main() &#123;
  debugPaintSizeEnabled = <span class="hljs-keyword">true</span>;
  <span class="hljs-comment">//debugPaintSizeEnabled=true;</span>
  runApp(MyApp());
&#125;

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MyApp</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">StatelessWidget</span> </span>&#123;
  <span class="hljs-comment">// This widget is the root of your application.</span>
  <span class="hljs-built_in">int</span> <span class="hljs-built_in">num</span> = <span class="hljs-number">0</span>;

  <span class="hljs-meta">@override</span>
  Widget build(BuildContext context) &#123;
    <span class="hljs-keyword">return</span> MaterialApp(title: <span class="hljs-string">"piccre"</span>, home: MyHomePage(title: <span class="hljs-string">"Home"</span>));
  &#125;
&#125;

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MyHomePage</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">StatefulWidget</span> </span>&#123;
  MyHomePage(&#123;Key? key, <span class="hljs-keyword">required</span> <span class="hljs-keyword">this</span>.title&#125;) : <span class="hljs-keyword">super</span>(key: key);
  <span class="hljs-keyword">final</span> <span class="hljs-built_in">String</span> title;

  <span class="hljs-meta">@override</span>
  App createState() => App();
&#125;

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">App</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">State</span> </span>&#123;
  <span class="hljs-built_in">bool</span> switchState = <span class="hljs-keyword">true</span>;
  FocusNode fn = <span class="hljs-keyword">new</span> FocusNode();
  FocusNode pw = <span class="hljs-keyword">new</span> FocusNode();
  TextEditingController tec = TextEditingController(text: <span class="hljs-string">"test"</span>);
  GlobalKey forms = <span class="hljs-keyword">new</span> GlobalKey<FormState>();
  <span class="hljs-keyword">final</span> sizeBox = DefaultTextStyle(style:TextStyle(color:Colors.deepOrange,fontSize:<span class="hljs-number">16</span>),child: SizedBox(
    height: <span class="hljs-number">200</span>,
    child: Flex(direction: Axis.horizontal, children: <Widget>[
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test1"</span>))),
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test2"</span>))),
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test2"</span>))),
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test2"</span>))),
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test2"</span>))),
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test2"</span>))),
      Expanded(
          flex: <span class="hljs-number">1</span>,
          child: Container(width: <span class="hljs-number">100</span>, child: Text(<span class="hljs-string">"test2"</span>))),
    ]),
  ));
  <span class="hljs-meta">@override</span>
  Widget build(BuildContext context) &#123;
    <span class="hljs-comment">// <span class="hljs-doctag">TODO:</span> implement build</span>
    <span class="hljs-keyword">return</span> Scaffold(
        appBar: AppBar(
            title: Text(<span class="hljs-string">"picc"</span>, textAlign: TextAlign.center),
            centerTitle: <span class="hljs-keyword">true</span>),
        body: Column(
            mainAxisSize: MainAxisSize.min,
            mainAxisAlignment: MainAxisAlignment.start,
            children: <Widget>[

              sizeBox,
              Padding(
                  padding: EdgeInsets.all(<span class="hljs-number">10.0</span>),
                  child: Form(
                    key: forms,
                    autovalidate: <span class="hljs-keyword">true</span>, <span class="hljs-comment">//开启自动校验</span>
                    child: Column(children: <Widget>[
                      TextFormField(
                        focusNode: fn,
                        controller: tec,
                        <span class="hljs-comment">//autofocus:true,</span>
                        decoration: InputDecoration(
                            labelText: <span class="hljs-string">'姓名'</span>,
                            hintText: <span class="hljs-string">'请输入姓名'</span>,
                            prefixIcon: Icon(Icons.account_circle)),
                        onChanged: (val) &#123;
                          <span class="hljs-built_in">print</span>(val);
                        &#125;,
                        validator: (v) &#123;
                          <span class="hljs-built_in">print</span>(v);
                          <span class="hljs-keyword">return</span> <span class="hljs-string">"test1"</span>;
                        &#125;,
                      ),
                      TextFormField(
                        <span class="hljs-comment">//autofocus:true,</span>
                        focusNode: pw,
                        decoration: InputDecoration(
                            labelText: <span class="hljs-string">'密码'</span>,
                            hintText: <span class="hljs-string">'请输入密码'</span>,
                            prefixIcon: Icon(Icons.keyboard)),
                        validator: (val) &#123;
                          <span class="hljs-keyword">return</span> <span class="hljs-string">"test2"</span>;
                        &#125;,
                      ),
                      RaisedButton(
                          padding: EdgeInsets.all(<span class="hljs-number">10.0</span>),
                          child: Text(<span class="hljs-string">"登录"</span>),
                          color: Theme.of(context).primaryColor,
                          textColor: Colors.white,
                          onPressed: () &#123;
                            (forms.currentState <span class="hljs-keyword">as</span> FormState).validate();
                          &#125;)
                    ]),
                  )),
              Switch(value: switchState, onChanged: onChanged),
              Text(<span class="hljs-string">"<span class="hljs-subst">$switchState</span>"</span>),
              Flex(direction: Axis.horizontal,mainAxisAlignment:MainAxisAlignment.spaceEvenly, children: <Widget>[
                Expanded(
                    flex: <span class="hljs-number">1</span>,
                    child: Container(
                        padding:EdgeInsets.all(<span class="hljs-number">20.0</span>),
                        child: Image(

                            image: AssetImage(<span class="hljs-string">'lib/image/img.png'</span>)))),
                Expanded(
                    flex: <span class="hljs-number">1</span>,
                    child: Container(
                        padding:EdgeInsets.all(<span class="hljs-number">20.0</span>),
                        child: Image(

                            image: NetworkImage(
                                <span class="hljs-string">'https://avatars2.githubusercontent.com/u/20411648?s=460&v=4'</span>))))
              ])

              <span class="hljs-comment">//Header()</span>
<span class="hljs-comment">//          Container(</span>
<span class="hljs-comment">//            child:Text("test"),</span>
<span class="hljs-comment">//          )</span>
            ]));
  &#125;

  <span class="hljs-meta">@override</span>
  <span class="hljs-keyword">void</span> initState() &#123;
    <span class="hljs-comment">// <span class="hljs-doctag">TODO:</span> implement initState</span>
    <span class="hljs-keyword">super</span>.initState();
    <span class="hljs-built_in">print</span>(<span class="hljs-string">"1=========================="</span>);
    <span class="hljs-comment">// print(FocusScope.of(context));</span>
    <span class="hljs-keyword">new</span> Timer(<span class="hljs-built_in">Duration</span>(seconds: <span class="hljs-number">10</span>), () &#123;
      (FocusScope.of(context)).requestFocus(pw);
      <span class="hljs-built_in">print</span>(<span class="hljs-string">'=================2'</span>);
    &#125;);
    <span class="hljs-keyword">new</span> Timer(<span class="hljs-built_in">Duration</span>(seconds: <span class="hljs-number">20</span>), () &#123;
      pw.unfocus();
      <span class="hljs-built_in">print</span>(<span class="hljs-string">'===============2.5'</span>);
    &#125;);
    <span class="hljs-built_in">print</span>(<span class="hljs-string">"============3"</span>);
  &#125;

  <span class="hljs-comment">// <span class="hljs-doctag">TODO:</span></span>
  <span class="hljs-keyword">void</span> onChanged(<span class="hljs-built_in">bool</span> value) &#123;
    setState(() &#123;
      switchState = value;
    &#125;);
  &#125;
&#125;

<span class="copy-code-btn">复制代码</span></code></pre></div>  
</div>
            