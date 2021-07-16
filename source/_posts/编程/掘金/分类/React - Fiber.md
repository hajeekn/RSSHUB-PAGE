
---
title: 'React - Fiber'
categories: 
 - 编程
 - 掘金
 - 分类
headimg: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0c467f248564f7aabb71b252466d2f9~tplv-k3u1fbpfcp-watermark.image'
author: 掘金
comments: false
date: Thu, 15 Jul 2021 06:23:51 GMT
thumbnail: 'https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0c467f248564f7aabb71b252466d2f9~tplv-k3u1fbpfcp-watermark.image'
---

<div>   
<div class="markdown-body"><style>.markdown-body&#123;word-break:break-word;line-height:1.75;font-weight:400;font-size:15px;overflow-x:hidden;color:#333&#125;.markdown-body h1,.markdown-body h2,.markdown-body h3,.markdown-body h4,.markdown-body h5,.markdown-body h6&#123;line-height:1.5;margin-top:35px;margin-bottom:10px;padding-bottom:5px&#125;.markdown-body h1&#123;font-size:30px;margin-bottom:5px&#125;.markdown-body h2&#123;padding-bottom:12px;font-size:24px;border-bottom:1px solid #ececec&#125;.markdown-body h3&#123;font-size:18px;padding-bottom:0&#125;.markdown-body h4&#123;font-size:16px&#125;.markdown-body h5&#123;font-size:15px&#125;.markdown-body h6&#123;margin-top:5px&#125;.markdown-body p&#123;line-height:inherit;margin-top:22px;margin-bottom:22px&#125;.markdown-body img&#123;max-width:100%&#125;.markdown-body hr&#123;border:none;border-top:1px solid #ddd;margin-top:32px;margin-bottom:32px&#125;.markdown-body code&#123;word-break:break-word;border-radius:2px;overflow-x:auto;background-color:#fff5f5;color:#ff502c;font-size:.87em;padding:.065em .4em&#125;.markdown-body code,.markdown-body pre&#123;font-family:Menlo,Monaco,Consolas,Courier New,monospace&#125;.markdown-body pre&#123;overflow:auto;position:relative;line-height:1.75&#125;.markdown-body pre>code&#123;font-size:12px;padding:15px 12px;margin:0;word-break:normal;display:block;overflow-x:auto;color:#333;background:#f8f8f8&#125;.markdown-body a&#123;text-decoration:none;color:#0269c8;border-bottom:1px solid #d1e9ff&#125;.markdown-body a:active,.markdown-body a:hover&#123;color:#275b8c&#125;.markdown-body table&#123;display:inline-block!important;font-size:12px;width:auto;max-width:100%;overflow:auto;border:1px solid #f6f6f6&#125;.markdown-body thead&#123;background:#f6f6f6;color:#000;text-align:left&#125;.markdown-body tr:nth-child(2n)&#123;background-color:#fcfcfc&#125;.markdown-body td,.markdown-body th&#123;padding:12px 7px;line-height:24px&#125;.markdown-body td&#123;min-width:120px&#125;.markdown-body blockquote&#123;color:#666;padding:1px 23px;margin:22px 0;border-left:4px solid #cbcbcb;background-color:#f8f8f8&#125;.markdown-body blockquote:after&#123;display:block;content:""&#125;.markdown-body blockquote>p&#123;margin:10px 0&#125;.markdown-body ol,.markdown-body ul&#123;padding-left:28px&#125;.markdown-body ol li,.markdown-body ul li&#123;margin-bottom:0;list-style:inherit&#125;.markdown-body ol li .task-list-item,.markdown-body ul li .task-list-item&#123;list-style:none&#125;.markdown-body ol li .task-list-item ol,.markdown-body ol li .task-list-item ul,.markdown-body ul li .task-list-item ol,.markdown-body ul li .task-list-item ul&#123;margin-top:0&#125;.markdown-body ol ol,.markdown-body ol ul,.markdown-body ul ol,.markdown-body ul ul&#123;margin-top:3px&#125;.markdown-body ol li&#123;padding-left:6px&#125;.markdown-body .contains-task-list&#123;padding-left:0&#125;.markdown-body .task-list-item&#123;list-style:none&#125;@media (max-width:720px)&#123;.markdown-body h1&#123;font-size:24px&#125;.markdown-body h2&#123;font-size:20px&#125;.markdown-body h3&#123;font-size:18px&#125;&#125;</style><p>本文转载自<a href="https://juejin.cn/post/6844903975112671239" target="_blank" title="https://juejin.cn/post/6844903975112671239">这可能是最通俗的 React Fiber(时间分片) 打开方式</a>这篇文章。</p>
<h3 data-id="heading-0">为什么要引入 Fiber 架构</h3>
<p>React 为什么要引入 Fiber 架构？ 看看下面的火焰图，这是React V15 下面的一个列表渲染资源消耗情况。整个渲染花费了130ms。🔴 <strong>在这里面 React 会递归比对VirtualDOM树，找出需要变动的节点，然后同步更新它们, 一气呵成。这个过程 React 称为 Reconcilation(中文可以译为协调)。</strong></p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0c467f248564f7aabb71b252466d2f9~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>在 Reconcilation 期间，React 会霸占着浏览器资源，一则会导致用户触发的事件得不到响应, 二则会导致掉帧，用户可以感知到这些卡顿。</p>
<p>同步模式下的 React:</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43b74d42fa8a43ddbebf78db213d8688~tplv-k3u1fbpfcp-watermark.image" alt="1.gif" loading="lazy" referrerpolicy="no-referrer"></p>
<p>优化后的 Concurrent 模式下的 React:</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0b04a7d3a48d492986a30bc6dbb707f1~tplv-k3u1fbpfcp-watermark.image" alt="2.gif" loading="lazy" referrerpolicy="no-referrer"></p>
<p>React 的 Reconcilation 是CPU密集型的操作, 它就相当于我们上面说的’长进程‘。所以初衷和进程调度一样，我们要让高优先级的进程或者短进程优先运行，不能让长进程长期霸占资源。</p>
<p>所以React 是怎么优化的？🔴 <strong>为了给用户制造一种应用很快的'假象'，我们不能让一个程序长期霸占着资源. 你可以将浏览器的渲染、布局、绘制、资源加载(例如HTML解析)、事件响应、脚本执行视作操作系统的'进程'，我们需要通过某些调度策略合理地分配CPU资源，从而提高浏览器的用户响应速率, 同时兼顾任务执行效率。</strong></p>
<p>🔴 <strong>所以 React 通过 Fiber 架构，让自己的Reconcilation 过程变成可被中断。适时地让出CPU执行权，除了可以让浏览器及时地响应用户的交互，还有其他好处:</strong></p>
<ul>
<li>与其一次性操作大量 DOM 节点相比, 分批延时对DOM进行操作，可以得到更好的用户体验。</li>
</ul>
<p>这就是为什么React 需要 Fiber。</p>
<h3 data-id="heading-1">何为 Fiber</h3>
<p>对于 React 来说，Fiber 可以从两个角度理解:</p>
<h4 data-id="heading-2">一种流程控制语</h4>
<p>Fiber 也称协程、或者纤程。</p>
<p>**其实协程和线程并不一样，协程本身是没有并发或者并行能力的（需要配合线程），它只是一种控制流程的让出机制。**要理解协程，你得和普通函数一起来看, 以Generator为例:</p>
<p>普通函数执行的过程中无法被<code>中断和恢复</code>：</p>
<pre><code class="copyable">const tasks = []
function run() &#123;
  let task
  while (task = tasks.shift()) &#123;
    execute(task)
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>而 <code>Generator</code> 可以:</p>
<pre><code class="copyable">const tasks = []
function * run() &#123;
  let task

  while (task = tasks.shift()) &#123;
    // 🔴 判断是否有高优先级事件需要处理, 有的话让出控制权
    if (hasHighPriorityEvent()) &#123;
      yield
    &#125;

    // 处理完高优先级事件后，恢复函数调用栈，继续执行...
    execute(task)
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>React Fiber 的思想和协程的概念是契合的: 🔴 <strong>React 渲染的过程可以被中断，可以将控制权交回浏览器，让位给高优先级的任务，浏览器空闲后再恢复渲染。</strong></p>
<p>那么现在你应该有以下疑问:</p>
<p>1️⃣ 浏览器没有抢占的条件, 所以React只能用让出机制?</p>
<p>2️⃣ 怎么确定有高优先任务要处理，即什么时候让出？</p>
<p>3️⃣ React 那为什么不使用 Generator？</p>
<p>答1️⃣: 没错, React主动让出。</p>
<p>一是浏览器中没有类似进程的概念，任务之间的界限很模糊，没有上下文，所以不具备中断/恢复的条件。二是没有抢占的机制，我们无法中断一个正在执行的程序。</p>
<p>所以我们只能采用类似协程这样控制权让出机制。这个和上文提到的进程调度策略都不同，它有更一个专业的名词：<strong>合作式调度(Cooperative Scheduling), 相对应的有抢占式调度(Preemptive Scheduling)。</strong></p>
<p><strong>这是一种’契约‘调度，要求我们的程序和浏览器紧密结合，互相信任。</strong> 比如可以由浏览器给我们分配执行时间片(通过requestIdleCallback实现, 下文会介绍)，我们要按照约定在这个时间内执行完毕，并将控制权还给浏览器。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07b21457d39b4b6e871226db42052296~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>答2️⃣: requestIdleCallback API</p>
<p>上面代码示例中的 <code>hasHighPriorityEvent()</code> 在目前浏览器中是无法实现的，我们没办法判断当前是否有更高优先级的任务等待被执行。</p>
<p>只能换一种思路，通过超时检查的机制来让出控制权。解决办法是: <code>确定一个合理的运行时长，然后在合适的检查点检测是否超时(比如每执行一个小任务)，如果超时就停止执行，将控制权交换给浏览器。</code></p>
<p>举个例子，为了让视图流畅地运行，可以按照人类能感知到最低限度每秒60帧的频率划分时间片，这样每个时间片就是 16ms。</p>
<p>其实浏览器提供了相关的接口 —— <code>requestIdleCallback</code> API：</p>
<pre><code class="copyable">window.requestIdleCallback(
  callback: (dealine: IdleDeadline) => void,
  option?: &#123;timeout: number&#125;
)
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>IdleDeadline</code>的接口如下：</p>
<pre><code class="copyable">interface IdleDealine &#123;
  didTimeout: boolean // 表示任务执行是否超过约定时间
  timeRemaining(): DOMHighResTimeStamp // 任务可供执行的剩余时间
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>单从名字上理解的话，<code>requestIdleCallback</code> 的意思是让浏览器在'有空'的时候就执行我们的回调，这个回调会传入一个期限，表示浏览器有多少时间供我们执行, 为了不耽误事，我们最好在这个时间范围内执行完毕。</p>
<p>那浏览器什么时候有空？</p>
<p>我们先来看一下浏览器在一帧(Frame，可以认为事件循环的一次循环)内可能会做什么事情:</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a23f4b8d25b244d49cd5c5697d476f50~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>浏览器在一帧内可能会做执行下列任务，而且它们的执行顺序基本是固定的:</p>
<ul>
<li>处理用户输入事件</li>
<li>Javascript执行</li>
<li>requestAnimation 调用</li>
<li>布局 Layout</li>
<li>绘制 Paint</li>
</ul>
<p>上面说理想的一帧时间是 <code>16ms</code> (1000ms / 60)，如果浏览器处理完上述的任务(布局和绘制之后)，还有盈余时间，浏览器就会调用 <code>requestIdleCallback</code> 的回调。例如：</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/16759bed0b1342d5af1428eb9b6ca8e2~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>但是在浏览器繁忙的时候，可能不会有盈余时间，这时候requestIdleCallback回调可能就不会被执行。 为了避免饿死，可以通过requestIdleCallback的第二个参数指定一个超时时间。</strong></p>
<p>另外<code>不建议在requestIdleCallback中进行DOM操作</code>，因为这可能<code>导致样式重新计算或重新布局</code>(比如操作DOM后马上调用 getBoundingClientRect)，这些时间很难预估的，<code>很有可能导致回调执行超时，从而掉帧。</code></p>
<p>目前 <code>requestIdleCallback</code> 目前只有Chrome支持。所以目前 React 自己实现了一个。它利用<code>MessageChannel</code> 模拟将回调延迟到'绘制操作'之后执行。</p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ace66710f18478e9811ce6d6533d47f~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h5 data-id="heading-3">任务优先级</h5>
<p>上面说了，为了避免任务被饿死，可以设置一个超时时间. 这个超时时间不是死的，低优先级的可以慢慢等待, 高优先级的任务应该率先被执行. 目前 React 预定义了 5 个优先级, 这个我在[《谈谈React事件机制和未来(react-events)》]中也介绍过:</p>
<ul>
<li><code>Immediate(-1)</code> - 这个优先级的任务会同步执行, 或者说要马上执行且不能中断</li>
<li><code>UserBlocking(250ms)</code> - 这些任务一般是用户交互的结果, 需要即时得到反馈</li>
<li><code>Normal (5s)</code> - 应对哪些不需要立即感受到的任务，例如网络请求</li>
<li><code>Low (10s)</code> - 这些任务可以放后，但是最终应该得到执行. 例如分析通知</li>
<li><code>Idle (没有超时时间)</code> - 一些没有必要做的任务 (e.g. 比如隐藏的内容), 可能会被饿死</li>
</ul>
<p>答3️⃣: 太麻烦</p>
<ul>
<li>
<p>Generator 不能在栈中间让出。比如你想在嵌套的函数调用中间让出, 首先你需要将这些函数都包装成Generator，另外这种栈中间的让出处理起来也比较麻烦，难以理解。除了语法开销，现有的生成器实现开销比较大，所以不如不用。</p>
</li>
<li>
<p>Generator 是有状态的, 很难在中间恢复这些状态。</p>
</li>
</ul>
<h4 data-id="heading-4">一个执行单元</h4>
<p>Fiber的另外一种解读是“纤维”: <code>这是一种数据结构或者说执行单元</code>。我们暂且不管这个数据结构长什么样，🔴<strong>将它视作一个执行单元，每次执行完一个“执行单元”, React 就会检查现在还剩多少时间，如果没有时间就将控制权让出去。</strong></p>
<p>上文说了，React 没有使用 Generator 这些语言/语法层面的让出机制，而是实现了自己的调度让出机制。这个机制就是基于’Fiber‘这个执行单元的，它的过程如下：</p>
<p>假设用户调用 <code>setState</code> 更新组件, 这个待更新的任务会先放入队列中, 然后通过 <code>requestIdleCallback</code> 请求浏览器调度：</p>
<pre><code class="copyable">updateQueue.push(updateTask);
requestIdleCallback(performWork, &#123;timeout&#125;);
<span class="copy-code-btn">复制代码</span></code></pre>
<p>现在浏览器有空闲或者超时了就会调用 <code>performWork</code> 来执行任务：</p>
<pre><code class="copyable">// 1️⃣ performWork 会拿到一个Deadline，表示剩余时间
function performWork(deadline) &#123;

  // 2️⃣ 循环取出updateQueue中的任务
  while (updateQueue.length > 0 && deadline.timeRemaining() > ENOUGH_TIME) &#123;
    workLoop(deadline);
  &#125;

  // 3️⃣ 如果在本次执行中，未能将所有任务执行完毕，那就再请求浏览器调度
  if (updateQueue.length > 0) &#123;
    requestIdleCallback(performWork);
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><code>workLoop</code> 的工作大概猜到了，它会从更新队列(updateQueue)中弹出更新任务来执行，每执行完一个“执行单元”，就检查一下剩余时间是否充足，如果充足就进行执行下一个执行单元，反之则停止执行，保存现场，等下一次有执行权时恢复。</p>
<pre><code class="copyable">// 保存当前的处理现场
let nextUnitOfWork: Fiber | undefined // 保存下一个需要处理的工作单元
let topWork: Fiber | undefined        // 保存第一个工作单元

function workLoop(deadline: IdleDeadline) &#123;
  // updateQueue中获取下一个或者恢复上一次中断的执行单元
  if (nextUnitOfWork == null) &#123;
    nextUnitOfWork = topWork = getNextUnitOfWork();
  &#125;

  // 🔴 每执行完一个执行单元，检查一次剩余时间
  // 如果被中断，下一次执行还是从 nextUnitOfWork 开始处理
  while (nextUnitOfWork && deadline.timeRemaining() > ENOUGH_TIME) &#123;
    // 下文我们再看performUnitOfWork
    nextUnitOfWork = performUnitOfWork(nextUnitOfWork, topWork);
  &#125;

  // 提交工作，下文会介绍
  if (pendingCommit) &#123;
    commitAllWork(pendingCommit);
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/094039c4a5224007ab05bcd81a6843bc~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h3 data-id="heading-5">React的 Fiber 改造</h3>
<h4 data-id="heading-6">1. 数据结构的调整</h4>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/60d111bc6309488e926056c3b1650cf8~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>左侧是Virtual DOM，右侧可以看作diff的递归调用栈。</p>
<p>上文中提到 React 16 之前，<code>Reconcilation 是同步的、递归执行的</code>。也就是说这是基于函数’调用栈‘的Reconcilation算法，因此通常也称它为<code>Stack Reconcilation</code>。</p>
<p>栈挺好的，代码量少，递归容易理解， 至少比现在的 React Fiber 架构好理解, 递归非常适合树这种嵌套数据结构的处理。</p>
<p>只不过这种依赖于调用栈的方式不能随意中断、也很难被恢复, 不利于异步处理。这种调用栈，不是程序所能控制的，如果你要恢复递归现场，可能需要从头开始, 恢复到之前的调用栈。</p>
<p>因此首先我们<strong>需要对React现有的数据结构进行调整，<code>模拟函数调用栈</code>, 将之前需要递归进行处理的事情分解成增量的执行单元，将递归转换成迭代</strong>。</p>
<p>React 目前的做法是使用<code>链表</code>, 每个 <code>VirtualDOM</code> 节点内部现在使用 Fiber 表示, 它的结构大概如下:</p>
<pre><code class="copyable">export type Fiber = &#123;
  // Fiber 类型信息
  type: any,
  // ...

  // ⚛️ 链表结构
  // 指向父节点，或者render该节点的组件
  return: Fiber | null,
  // 指向第一个子节点
  child: Fiber | null,
  // 指向下一个兄弟节点
  sibling: Fiber | null,
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>用图片来展示这种关系会更直观一些：</p>
<p><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5ca1e22347634716b3286a3f2c410a2c~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p><strong>使用链表结构只是一个结果，而不是目的，React 开发者一开始的目的是冲着模拟调用栈去的。</strong></p>
<p><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/02a7aee904cc4021977b0bda7590d9dc~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<blockquote>
<p>调用栈最经常被用于存放子程序的<strong>返回地址</strong>。在调用任何子程序时，主程序都必须暂存子程序运行完毕后应该返回到的地址。因此，如果被调用的子程序还要调用其他的子程序，其自身的返回地址就必须存入调用栈，在其自身运行完毕后再行取回。除了返回地址，还会保存<code>本地变量</code>、<code>函数参数</code>、<code>环境传递</code>。</p>
</blockquote>
<p>React Fiber 也被称为虚拟栈帧(Virtual Stack Frame), 你可以拿它和函数调用栈类比一下, 两者结构非常像：</p>








































<table><thead><tr><th></th><th>函数调用栈</th><th>Fiber</th></tr></thead><tbody><tr><td>基本单位</td><td>函数</td><td>Virtual DOM 节点</td></tr><tr><td>输入</td><td>函数参数</td><td>Props</td></tr><tr><td>本地状态</td><td>本地变量</td><td>State</td></tr><tr><td>输出</td><td>函数返回值</td><td>React Element</td></tr><tr><td>下级</td><td>嵌套函数调用</td><td>子节点(child)</td></tr><tr><td>上级引用</td><td>返回地址</td><td>父节点(return)</td></tr></tbody></table>
<p>Fiber 和调用栈帧一样, 保存了节点处理的上下文信息，因为是手动实现的，所以更为可控，我们可以保存在内存中，随时中断和恢复。</p>
<p>有了这个数据结构调整，现在可以以迭代的方式来处理这些节点了。来看看 <code>performUnitOfWork</code> 的实现, 它其实就是一个深度优先的遍历：</p>
<pre><code class="copyable">/**
 * @params fiber 当前需要处理的节点
 * @params topWork 本次更新的根节点
 */
function performUnitOfWork(fiber: Fiber, topWork: Fiber) &#123;
  // 对该节点进行处理
  beginWork(fiber);

  // 如果存在子节点，那么下一个待处理的就是子节点
  if (fiber.child) &#123;
    return fiber.child;
  &#125;

  // 没有子节点了，上溯查找兄弟节点
  let temp = fiber;
  while (temp) &#123;
    completeWork(temp);

    // 到顶层节点了, 退出
    if (temp === topWork) &#123;
      break
    &#125;

    // 找到，下一个要处理的就是兄弟节点
    if (temp.sibling) &#123;
      return temp.sibling;
    &#125;

    // 没有, 继续上溯
    temp = temp.return;
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>你可以配合上文的 workLoop 一起看，<strong>Fiber 就是我们所说的工作单元，performUnitOfWork 负责对 Fiber 进行操作，并按照深度遍历的顺序返回下一个 Fiber。</strong></p>
<p><strong>因为使用了链表结构，即使处理流程被中断了，我们随时可以从上次未处理完的Fiber继续遍历下去。</strong></p>
<p>整个迭代顺序和之前递归的一样, 下图假设在 div.app 进行了更新：</p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0371c2b4b0054618922a28fd79b97ff8~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>比如你在text(hello)中断了，那么下一次就会从 p 节点开始处理。</p>
<p>这个数据结构调整还有一个好处，就是某些节点异常时，我们可以打印出完整的“节点栈”，只需要沿着节点的<code>return</code>回溯即可。</p>
<h4 data-id="heading-7">2. 两个阶段的拆分</h4>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/aeb084d1fe1746fcb442e7e6fcd9bf15~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>除了Fiber 工作单元的拆分，两阶段的拆分也是一个非常重要的改造，在此之前都是一边Diff一边提交的。先来看看这两者的区别：</p>
<ul>
<li>
<p>⚛️ 协调阶段: 可以认为是 Diff 阶段, 这个阶段可以被中断, 这个阶段会找出所有节点变更，例如节点新增、删除、属性变更等等，这些变更React 称之为'副作用(Effect)'。以下生命周期钩子会在协调阶段被调用：</p>
<ul>
<li>constructor</li>
<li>componentWillMount 废弃</li>
<li>componentWillReceiveProps 废弃</li>
<li>static getDerivedStateFromProps</li>
<li>shouldComponentUpdate</li>
<li>componentWillUpdate 废弃</li>
<li>render</li>
</ul>
</li>
<li>
<p>⚛️ 提交阶段: 将上一个阶段计算出来的需要处理的 <strong>副作用(Effects)</strong> 一次性执行了。这个阶段必须同步执行，不能被打断。这些生命周期钩子在提交阶段被执行：</p>
<ul>
<li>getSnapshotBeforeUpdate() 严格来说，这个是在进入 commit 阶段前调用</li>
<li>componentDidMount</li>
<li>componentDidUpdate</li>
<li>componentWillUnmount</li>
</ul>
</li>
</ul>
<p>也就是说，在协调阶段如果时间片用完，React就会选择让出控制权。因为协调阶段执行的工作不会导致任何用户可见的变更，所以在这个阶段让出控制权不会有什么问题。</p>
<p>需要注意的是：<strong>因为协调阶段可能被中断、恢复，甚至重做，React 协调阶段的生命周期钩子可能会被调用多次!!!</strong> 例如 componentWillMount 可能会被调用两次。</p>
<p>因此建议 <strong>协调阶段的生命周期钩子不要包含副作用</strong>。索性 React 就废弃了这部分可能包含副作用的生命周期方法，例如<code>componentWillMount</code>、<code>componentWillUpdate</code>。v17后我们就不能再用它们了, 所以现有的应用应该尽快迁移.</p>
<p>现在你应该知道为什么“提交阶段”必须同步执行，不能中断的吧？ 因为我们要正确地处理各种副作用，包括DOM变更、还有你在componentDidMount中发起的异步请求、useEffect 中定义的副作用... 因为有副作用，所以必须保证按照次序只调用一次，况且会有用户可以察觉到的变更, 不容出错。</p>
<h4 data-id="heading-8">3. Reconcilation</h4>
<p>接下来就是就是我们熟知的<code>Reconcilation</code>(为了方便理解，本文不区分Diff和Reconcilation, 两者是同一个东西)阶段了. 思路和 Fiber 重构之前差别不大, 只不过这里不会再递归去比对、而且不会马上提交变更。</p>
<p>首先再进一步看一下Fiber的结构:</p>
<pre><code class="copyable">interface Fiber &#123;
  /**
   * ⚛️ 节点的类型信息
   */
  // 标记 Fiber 类型, 例如函数组件、类组件、宿主组件
  tag: WorkTag,
  // 节点元素类型, 是具体的类组件、函数组件、宿主组件(字符串)
  type: any,

  /**
   * ⚛️ 结构信息
  */ 
  return: Fiber | null,
  child: Fiber | null,
  sibling: Fiber | null,
  // 子节点的唯一键, 即我们渲染列表传入的key属性
  key: null | string,

  /**
   * ⚛️ 节点的状态
   */
  // 节点实例(状态)：
  //   对于宿主组件，这里保存宿主组件的实例, 例如DOM节点。
  //   对于类组件来说，这里保存类组件的实例
  //   对于函数组件说，这里为空，因为函数组件没有实例
  stateNode: any,
  // 新的、待处理的props
  pendingProps: any,
  // 上一次渲染的props
  memoizedProps: any, // The props used to create the output.
  // 上一次渲染的组件状态
  memoizedState: any,


  /**
   * ⚛️ 副作用
   */
  // 当前节点的副作用类型，例如节点更新、删除、移动
  effectTag: SideEffectTag,
  // 和节点关系一样，React 同样使用链表来将所有有副作用的Fiber连接起来
  nextEffect: Fiber | null,

  /**
   * ⚛️ 替身
   * 指向旧树中的节点
   */
  alternate: Fiber | null,
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>Fiber 包含的属性可以划分为 5 个部分:</p>
<ul>
<li>
<p>🆕 结构信息 - 这个上文我们已经见过了，Fiber 使用链表的形式来表示节点在树中的定位。</p>
</li>
<li>
<p>节点类型信息 - 这个也容易理解，tag表示节点的分类、type 保存具体的类型值，如div、MyComp。</p>
</li>
<li>
<p>节点的状态 - 节点的组件实例、props、state等，它们将影响组件的输出。</p>
</li>
<li>
<p>🆕 副作用 - 这个也是新东西. 在 Reconciliation 过程中发现的“副作用”(变更需求)就保存在节点的<code>effectTag</code> 中(想象为打上一个标记)。那么怎么将本次渲染的所有节点副作用都收集起来呢？ 这里也使用了链表结构，在遍历过程中React会将所有有‘副作用’的节点都通过<code>nextEffect</code>连接起来。</p>
</li>
<li>
<p>🆕 替身 - React 在 Reconciliation 过程中会构建一颗新的树(官方称为workInProgress tree，WIP树)，可以认为是一颗表示当前工作进度的树。还有一颗表示已渲染界面的旧树，React就是一边和<code>旧树</code>比对，一边构建<code>WIP树</code>的。 alternate 指向旧树的同等节点。</p>
</li>
</ul>
<p>现在可以放大看看beginWork 是如何对 Fiber 进行比对的：</p>
<pre><code class="copyable">function beginWork(fiber: Fiber): Fiber | undefined &#123;
  if (fiber.tag === WorkTag.HostComponent) &#123;
    // 宿主节点diff
    diffHostComponent(fiber)
  &#125; else if (fiber.tag === WorkTag.ClassComponent) &#123;
    // 类组件节点diff
    diffClassComponent(fiber)
  &#125; else if (fiber.tag === WorkTag.FunctionComponent) &#123;
    // 函数组件节点diff
    diffFunctionalComponent(fiber)
  &#125; else &#123;
    // ... 其他类型节点，省略
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>宿主节点比对：</p>
<pre><code class="copyable">function diffHostComponent(fiber: Fiber) &#123;
  // 新增节点
  if (fiber.stateNode == null) &#123;
    fiber.stateNode = createHostComponent(fiber)
  &#125; else &#123;
    updateHostComponent(fiber)
  &#125;

  const newChildren = fiber.pendingProps.children;

  // 比对子节点
  diffChildren(fiber, newChildren);
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>类组件节点比对也差不多：</p>
<pre><code class="copyable">function diffClassComponent(fiber: Fiber) &#123;
  // 创建组件实例
  if (fiber.stateNode == null) &#123;
    fiber.stateNode = createInstance(fiber);
  &#125;

  if (fiber.hasMounted) &#123;
    // 调用更新前生命周期钩子
    applybeforeUpdateHooks(fiber)
  &#125; else &#123;
    // 调用挂载前生命周期钩子
    applybeforeMountHooks(fiber)
  &#125;

  // 渲染新节点
  const newChildren = fiber.stateNode.render();
  // 比对子节点
  diffChildren(fiber, newChildren);

  fiber.memoizedState = fiber.stateNode.state
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>子节点比对：</p>
<pre><code class="copyable">function diffChildren(fiber: Fiber, newChildren: React.ReactNode) &#123;
  let oldFiber = fiber.alternate ? fiber.alternate.child : null;
  // 全新节点，直接挂载
  if (oldFiber == null) &#123;
    mountChildFibers(fiber, newChildren)
    return
  &#125;

  let index = 0;
  let newFiber = null;
  // 新子节点
  const elements = extraElements(newChildren)

  // 比对子元素
  while (index < elements.length || oldFiber != null) &#123;
    const prevFiber = newFiber;
    const element = elements[index]
    const sameType = isSameType(element, oldFiber)
    if (sameType) &#123;
      newFiber = cloneFiber(oldFiber, element)
      // 更新关系
      newFiber.alternate = oldFiber
      // 打上Tag
      newFiber.effectTag = UPDATE
      newFiber.return = fiber
    &#125;

    // 新节点
    if (element && !sameType) &#123;
      newFiber = createFiber(element)
      newFiber.effectTag = PLACEMENT
      newFiber.return = fiber
    &#125;

    // 删除旧节点
    if (oldFiber && !sameType) &#123;
      oldFiber.effectTag = DELETION;
      oldFiber.nextEffect = fiber.nextEffect
      fiber.nextEffect = oldFiber
    &#125;

    if (oldFiber) &#123;
      oldFiber = oldFiber.sibling;
    &#125;

    if (index == 0) &#123;
      fiber.child = newFiber;
    &#125; else if (prevFiber && element) &#123;
      prevFiber.sibling = newFiber;
    &#125;

    index++
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>上面的代码很粗糙地还原了 Reconciliation 的过程, 但是对于我们理解React的基本原理已经足够了。</p>
<p><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/44e5d583a181479293b6879a61ee5f6b~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<p>上图是 <code>Reconciliation</code> 完成后的状态，左边是旧树，右边是WIP树。对于需要变更的节点，都打上了“标签”。 在提交阶段，React 就会将这些打上标签的节点应用变更。</p>
<h4 data-id="heading-9">4. 双缓冲</h4>
<p><code>WIP 树</code>构建这种技术类似于图形化领域的“双缓存(Double Buffering)”技术, 图形绘制引擎一般会使用双缓冲技术，先将图片绘制到一个缓冲区，再一次性传递给屏幕进行显示，这样可以防止屏幕抖动，优化渲染性能。</p>
<p>WIP 树构建这种技术类似于图形化领域的'双缓存(Double Buffering)'技术, 图形绘制引擎一般会使用双缓冲技术，先将图片绘制到一个缓冲区，再一次性传递给屏幕进行显示，这样可以防止屏幕抖动，优化渲染性能。</p>
<p>双缓存技术还有另外一个重要的场景就是异常的处理，比如当一个节点抛出异常，仍然可以继续沿用旧树的节点，避免整棵树挂掉。</p>
<p><strong>你可以将 WIP 树想象成从旧树中 Fork 出来的功能分支，你在这新分支中添加或移除特性，即使是操作失误也不会影响旧的分支。当你这个分支经过了测试和完善，就可以合并到旧分支，将其替换掉. 这或许就是’提交(commit)阶段‘的提交一词的来源吧？</strong></p>
<p><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7e3e8a6c3e5a46c0b165451f2a39ffc8~tplv-k3u1fbpfcp-watermark.image" alt="image.png" loading="lazy" referrerpolicy="no-referrer"></p>
<h4 data-id="heading-10">5. 副作用的收集和提交</h4>
<p>接下来就是将所有打了 Effect 标记的节点串联起来，这个可以在completeWork中做, 例如：</p>
<pre><code class="copyable">function completeWork(fiber) &#123;
  const parent = fiber.return

  // 到达顶端
  if (parent == null || fiber === topWork) &#123;
    pendingCommit = fiber
    return
  &#125;

  if (fiber.effectTag != null) &#123;
    if (parent.nextEffect) &#123;
      parent.nextEffect.nextEffect = fiber
    &#125; else &#123;
      parent.nextEffect = fiber
    &#125;
  &#125; else if (fiber.nextEffect) &#123;
    parent.nextEffect = fiber.nextEffect
  &#125;
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>最后，将所有副作用提交：</p>
<pre><code class="copyable">function commitAllWork(fiber) &#123;
  let next = fiber
  while(next) &#123;
    if (fiber.effectTag) &#123;
      // 提交，偷一下懒，这里就不展开了
      commitWork(fiber)
    &#125;
    next = fiber.nextEffect
  &#125;

  // 清理现场
  pendingCommit = nextUnitOfWork = topWork = null
&#125;
<span class="copy-code-btn">复制代码</span></code></pre>
<p>开启 <code>Concurrent Mode</code> 后，我们可以得到以下好处(详见Concurrent Rendering in React):</p>
<ul>
<li>快速响应用户操作和输入，提升用户交互体验。</li>
<li>让动画更加流畅，通过调度，可以让应用保持高帧率。</li>
<li>利用好 <code>I/O</code> 操作空闲期或者CPU空闲期，进行一些预渲染。比如离屏(offscreen)不可见的内容，优先级最低，可以让 React 等到CPU空闲时才去渲染这部分内容。这和浏览器的preload等预加载技术差不多。</li>
<li>用 <code>Suspense</code> 降低加载状态(load state)的优先级，减少闪屏。比如数据很快返回时，可以不必显示加载状态，而是直接显示出来，避免闪屏；如果超时没有返回才显式加载状态。</li>
</ul>
<h3 data-id="heading-11">参考文章</h3>
<p><a href="https://juejin.cn/post/6844903975112671239" target="_blank" title="https://juejin.cn/post/6844903975112671239">这可能是最通俗的 React Fiber(时间分片) 打开方式</a></p>
<p><a href="https://juejin.cn/post/6844903905382367245" target="_blank" title="https://juejin.cn/post/6844903905382367245">谈谈React事件机制和未来(react-events)</a></p>
<p><a href="https://juejin.cn/post/6844903861434449933" target="_blank" title="https://juejin.cn/post/6844903861434449933">从Preact中了解React组件和hooks基本原理</a></p>
<p><a href="https://juejin.cn/post/6844903582622285831" target="_blank" title="https://juejin.cn/post/6844903582622285831">React Fiber</a></p></div>  
</div>
            