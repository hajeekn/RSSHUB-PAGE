
---
title: '用 antd 两个 DatePicker 组件实现起止时间相互约束的流程'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6eb889b5e1f74210b7d05c5d483880e4~tplv-k3u1fbpfcp-zoom-1.image'
author: 掘金
comments: false
date: Sat, 10 Jul 2021 18:56:41 GMT
thumbnail: 'https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6eb889b5e1f74210b7d05c5d483880e4~tplv-k3u1fbpfcp-zoom-1.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><h3 data-id="heading-0">背景</h3>
<p>一个基于 React 前端技术的项目，在做搜索功能时，虽然 antd 有 <code>DateRange</code> 插件，但技术选择用的是两个 <code>DatePicker</code> ，所以需要自己实现起止时间的约束：</p>
<ol>
<li>开始时间必须小于结束时间</li>
<li>结束时间必须大于开始时间，且不超过当日</li>
</ol>
<h3 data-id="heading-1">实现流程</h3>
<p>第一，定义两个成员变量和两个 state 属性：</p>
<ol>
<li>两个记录当前日期插件选中的时间的变量；</li>
<li>两个 state 时间变量，初始化日期插件的变量。</li>
</ol>
<p>第二，起止时间插件各自用到的两个回调函数：</p>
<ol>
<li>onChangeStart ，开始时间，选择时间变更后，记录对应值</li>
<li>onChangeEnd ，结束时间，选择时间变更后，记录对应值</li>
<li>disableDateStart ，开始时间回调</li>
<li>disableDateEnd ，结束时间的回调</li>
</ol>
<h3 data-id="heading-2">第一，全局变量定义</h3>
<p>组件构造函数定义两个成员变量用来记录当前选择的日期，<strong>注意是成员变量</strong>，而不是 state 的两个属性。</p>
<pre><code class="copyable">constructor(props) &#123;
let now = new Date();
let year = now.getFullYear();
let month = now.getMonth() + 1 < 10 ? '0' + (now.getMonth() + 1) : now.getMonth() + 1;
let day = now.getDate() < 10 ? '0' + now.getDate() : now.getDate();
let defaultStartTime = year + "-" + month + "-" + day + " 00:00:00";
let defaultEndTime = year + "-" + month + "-" + day + " 23:59:59";

// 页面需要的常量：当天时间起止值
this.todayStart = moment(defaultStartTime);
this.todayEnd = moment(defaultEndTime);

// 页面 state 数据
this.state = &#123;
startTime: this.todayStart,
endTime: this.todayEnd,
&#125;

// 由于 state.xxx 属性设置后容易出现 undefined ，所以用全局类变量
this.currentStartTime = this.todayStart;
this.currentEndTime = this.todayEnd; 
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-3">第二，日期插件引用</h3>
<p>组件引用两个日期插件，指定初始值和各自的回调：</p>
<pre><code class="copyable"><Form ref=&#123;this.formRef&#125; onFinish=&#123;this.onFinish&#125;>
<div>开始时间</div>
<Form.Item name="startTime" initialValue=&#123;this.state.startTime&#125;>
<DatePicker
showTime=&#123;&#123; format: 'HH:mm:ss' &#125;&#125;
format="YYYY-MM-DD HH:mm:ss"
allowClear=&#123;false&#125;
onChange=&#123; this.dateChangeStart&#125;
disabledDate=&#123;this.disabledDateStart&#125;
/>
</Form.Item>
<div>结束时间</div>
<Form.Item name="endTime" initialValue=&#123;this.state.endTime&#125;>
<DatePicker
showTime=&#123;&#123; format: 'HH:mm:ss' &#125;&#125;
format="YYYY-MM-DD HH:mm:ss"
onChange=&#123; this.dateChangeEnd&#125;
disabledDate=&#123;this.disabledDateEnd&#125;
allowClear=&#123;false&#125;
/>
        </Form.Item>
</Form>
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-4">第三，日期变动回调定义</h3>
<p>为起止时间插件，定义 <code>onChange</code> 回调，如果选择了新日期，则记录到全局变量中。</p>
<pre><code class="copyable">// 点击都会触发该函数，未选择时是 undefiend
dateChangeStart = (current) => &#123;
if(current != undefined) &#123;
this.currentStartTime = current; // 修改全局变量，通知日期插件
&#125;
&#125;

dateChangeEnd = (current) => &#123;
if(current != undefined) &#123;
this.currentEndTime= current; // 修改全局变量，通知日期插件
&#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-5">第四，禁用时间回调定义</h3>
<p>开始时间插件的 <code>disabledDate</code> 根据当前选中的结束日期值设定禁用时间，同理，结束时间插件根据开始时间和当天设定禁用范围。</p>
<p>详细函数定义为：</p>
<pre><code class="copyable">// 开始时间范围：不能包含今天以后的，且不能超过结束时间
disabledDateStart = (current) => &#123;
const endValue = this.currentEndTime;//获取结束时间
if (!endValue) &#123;//如果开始日期或者结束日期都没有选择，限定今日之后的不允许选择
return current && current.valueOf() > this.todayEnd.valueOf();
&#125;

//用户选择了结束时间，则开始时间要小于结束时间
return current.valueOf() > endValue.valueOf();
&#125;

disabledDateEnd = (current) => &#123;
const startValue = this.currentStartTime;
const currentcurrent = this.currentEndTime;

// 如果用户未选择开始时间，则不能选今天以后的
if (!startValue) &#123;
return current && current.valueOf() > this.todayEnd.valueOf();
&#125;

// 时间范围在开始时间和当日之间
return current.valueOf() <= startValue.valueOf() || 
current.valueOf() > this.todayEnd.valueOf();
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<h3 data-id="heading-6">运行效果</h3>
<p>选定开始和结束时间后，查看各自插件的选择范围：
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6eb889b5e1f74210b7d05c5d483880e4~tplv-k3u1fbpfcp-zoom-1.image" alt="在这里插入图片描述" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-7">启示录</h3>
<p>思路很简单，就是 <code>disableDate</code> 回调要利用当前日期插件选择的时间，来确定范围。</p>
<p>有一个坑点就是 <code>state</code> 变量，感觉它是异步的，即使刚刚设置了值，<code>disableDate</code> 回调取到的却是 <code>undefined</code> 。</p>
<p>最初为了记录选中日期，将其设置为 <code>state.curerntStartTime</code> ，结果取值时会出现 <code>undefined</code> 的情况，页面选择几次日期后，禁用时间范围就乱套了。</p>
<p><strong>结论</strong>：要实现两个日期插件的选择范围联动，函数中引用的变量应该定义为 <code>this.xxx</code> 属性，而非 <code>this.state.xxx</code> 。</p>
<p>这可能跟 <code>state</code> 的作用有关吧，它主要是动态回显组件值的，数值更新有滞后！</p></div>  
</div>
            