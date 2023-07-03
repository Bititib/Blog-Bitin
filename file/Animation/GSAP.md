# GSAP 动画

一、学习——准备

> gsap 官网：https://greensock.com/
>
> 文档地址：https://greensock.com/docs/v3/GSAP
>
> 免费课程：https://www.creativecodingclub.com/courses/take/FreeGSAP3Express/lessons/16523777-our-development-environment
>
> 在线编辑地址：https://codepen.io/pen/

二、在线编辑

打开在线编辑地址，你会发现那是一个在线编辑器能够实时生成对应代码效果

> 包括：HTML CSS JavaScript，内置gsap.js用来学习再好不过了

## 下载GSAP

[CDN][https://greensock.com/docs/v3/Installation]

> ```html
> <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.0/gsap.min.js"></script>
> ```

NPM

>npm install gsap 
>
>此方法下载的是没有插件的

更多可以去GitHub或者官网查看

## Tween 补间动画

 常见的有

> gsap.to ('element',{endCSSOptions});
>
> gsap.from('element',(endCSSOptions));
>
> gsap.fromTo('element',{start CSS Options},{end CSS Options});
>
> 这里的目标元素element可以是用选择器来选择，也可以用js获取的元素来选择
>
> 用选择器是要使用字符串形式，使用js获取的直接使用变量

实例

```html
<div class="content">
    Holle Word
</div>
<script>
	const el = document.querySelector(".content");
    gsap.to(el,{rotation: 27, x: 100, duration: 1})//x ：translateX的值
    gsap.from(el,{rotation: -360, x: -100, duration: 1});
    gsap.fromTo(el, {x: -100},{rotation: 360, x: 100, duration: 1});
</script>
```

> 三者CSS对象样式区别：
>
> .to()： 表示要去往的目标位置及使用什么动画，
>
> .from() ： 表示从哪个位置为起始点，前往元素本来的位置
>
> .fromTo() ：前一个对象属性表示起始样式，第二个对象属性表示目标位置
>
> 相同点：都是根据元素原本的样式进行动画

### stagger特殊属性——分割时间使元素交错进行

案例

```html
<div class="item"> 一个圆角盒子 </div>
<div class="item"> 一个圆角盒子 </div>
<div class="item"> 一个圆角盒子 </div>
<script>
const item = document.querySelectorAll('.item')
gsap.to(item,{stagger:1,x:600,fill:"yellow",rotation:360,duration:3}) //fill : 颜色填充
</script>
```

其他特殊属性

> - 延迟和重复
>
>   - **delay** ：延迟时间
>   - **repeat**  ：重复播放；设置为-1，将无限播放
>   - **yoyo** ：当设置为true的时候动画将来回播放
>   - **repeatDelay**：每次重复间隔多长时间
>
> - 缓动控制动画播放时的**变化率**
>
>   - ease：制你的动画是**减慢**还是**加速**。
>     - bounce ： 会在出来时反弹
>     - bounce.in ： 会在途中反弹
>     - bounce.inOut ：会在到达目标位置前时反弹
>     - elastic ： 过目标位置会有反弹效果
>     - back ：过目标位置会有缓慢的反弹效果
>     - back(6) : 配置back()会有更强的过冲
>     - linear ： 默认缓慢渐入
>
> - stagger ： 前一个元素开始执行多久后执行
>
>   - each ： 控制的时间
>   - from :  动画开始的位置 "start"是从头开始 "end"是从尾开始
>   - ease : "动画"
>
>   **each:0.2**表示每个动画开始 **之间**会有 0.2 秒。
>
>   如果改为使用**amount:0.2则所有动画将在 0.2 秒内**开始

### 补间控制

提供多个能够进行动画播放控制 

> play()：播放、pause()：暂停、reverse()：反转、restart()：重新开始 、等

实例

```css
body{
  background-color: #f60;
}
.item{
  width:20px;
  height:20px;
  margin-top:5px;
  border-radius:2px;
  background-color:#fff;
}
.tween{
  display:flex;
  width:220px;
  height:40px;
  line-height:40px;
  border:1px soild #aaa;
}
.c{
  width:50px;
  height:100%;
  line-height:250%;
  background-color:#ccc;
  text-align:center;
}

```

```html
<div class="item"> </div>
<div class="item"> </div>
<div class="item"> </div>
<div class="tween">
  <div class="play c"> paly </div>
  <div class="pause c"> pause </div>
  <div class="revers c"> revers </div>
  <div class="restart c"> restart </div>
</div>

<script>
const item = document.querySelectorAll('.item')
const tween = gsap.to(item,{stagger:1,x:60,rotation:360,duration:3,pause:ture})//此处设置pause:ture表示禁止自动播放

// 补间控制
document.querySelector('.play').onClick = ()=> tween.play();

document.querySelector('.pause').onclick = () => tween.pause();

document.querySelector('.revers').onclick = () => tween.reverse();

document.querySelector('.restart').onclick = () => tween.restart();

</script>
```

### tranform-origin——变换原点

默认情况下，DOM 元素将围绕其中心点缩放、旋转和倾斜。 如果我们想改变我们有权访问 css 属性 transform-origin。 与所有带连字符的 css 属性一样，**transform-origin**在 GSAP 补间中使用时变为**transformOrigin **。**transformOrigin 值使用一对水平**(x) 和**垂直**(y) 值设置为单个字符串。这些值*通常*以 **像素**、**百分比**或使用**css 关键字**设置：left、center、right、top、bottom。transformOrigin使用一个字符引号将其包括

> gasp.to('el',{ transformOrigin:"bottom center" })



## 时间线

使用 gsap.timeline() 创建时间线；时间轴中的所有补间自然地一个接一个地播放

```js
gsap.timeline()
  .from("#demo", {autoAlpha:0})
  .from("#title", {opacity:0, scale:0, ease:"back"})
  .from("#freds img", {y:160, stagger:0.1, duration:0.8, ease:"back"})
  .from("#time", {xPercent:100, duration:0.2})
```

### 位置参数

> 在时间线中补间动画添加多一个参数属性表示触发的时间线：
>
> - "+=1" 在前一个补间结束后一秒开始
> - "-=1"在前一个补间结束前一秒开始
> - "<" 表示跟前一个补间同一时间开始
> - "<1" 表示前一个补间开始后一秒开始
> - 1  ： 数字表示时间轴,时间为1时触发

```js
var tl = gsap.timeline();
  tl.to(object, {y:300}, "+=1")  // start 1 second after previous tween ends
  tl.to(object, {x:300}, "-=1")  // start 1 second before previous tween ends
  tl.to(object, {rotation:90}, "<")  // start when previous tween begins
  tl.to(object, {opacity:0.5}, "<1") // start 1 second after previous tween begins
  tl.to(object2, {x:200}, 1) // start exactly at a time of 1

使用“+=”和“-=”位置参数的相对补间相对于时间线的末尾放置，不一定总是时间线中的前一个补间。

```



## ScrollTrigger (滚动条)

gsap 利用ScrollTrigger插件创建令人瞠目结舌的动画(Magical animation) 。触发任何与滚动相关的内容，即使目前没有动画；



### 引入ScrollTrigger插件

> CDN
>
> ```html
> <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
> ```
>
> NPM
>
> 

创建一个ScrollTrigger实例

> ```js
> ScrollTrigger.create({
> 
> 	trigger:'targetElement',	
> 
> 	animation:gsap.to('element',{'a lot`s  animation'})
> 
> })
> ```
>
> 



官网实例：

```js
let tl = gsap.timeline({
    // 可以将它写入补间动画
    scrollTrigger: {
      trigger: ".container",
      pin: true,   // 激活时固定触发器
      start: "top top", // 当触发器的顶部碰到视窗的顶部时
      end: "+=500", // 滚动超过起始点500px后结束
      scrub: 1, // 平滑擦洗，需要1秒“赶上”滚动条
      snap: {
        snapTo: "labels", //捕捉到时间轴上最近的标签
        duration: {min: 0.2, max: 3}, // 快照动画至少0.2秒，但不超过3秒(由速度决定)
        delay: 0.2, // 从最后一个滚动事件开始等待0.2秒，然后再进行捕捉
        ease: "power1.inOut" // 快照动画的易用性(默认为“power3”)
      }
    }
  });

/* add animations and labels to the timeline
向时间轴添加动画和标签 */
tl.addLabel("start")
  .from(".box p", {scale: 0.3, rotation:45, autoAlpha: 0})
  .addLabel("color")
  .from(".box", {backgroundColor: "#28a92b"})
  .addLabel("spin")
  .to(".box", {rotation: 360})
  .addLabel("end");
```

### 用途及特殊性能

scrolltrigger既可以用作触发器的简写(如下所述)，也可以用作具有以下任何属性的配置对象:

| Property（属性） | typeOf Values（属性值类型）                                  | Description（描述）                                          | 使用分析                                                     |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| trigger          | String \| Element                                            | 在正常文档流中的位置用于计算 ScrollTrigger 开始位置的元素（或元素的选择器文本） |                                                              |
| start            | String \| Number \| Function                                 | 确定 ScrollTrigger 的起始位置。                              | · String - 描述触发器上的位置和滚动条上必须相遇才能启动ScrollTrigger的位置。例如`"top center"`表示的是trigger元素触发器的顶部和滚动条中心为起始点。`"top, center 80%"`表示距离滚动条中心80%处为起点，`"top bottom -=100px"`当触发器顶部位于视口滚动条底部上方100px时。<br />· Number - 精确的滚动值，因此`200`当视口滚动条滚动恰好 200 像素时会触发<br />Function - 每当 ScrollTrigger 计算其位置时（通常在创建时和滚动条调整大小时）都会调用的函数。它应该返回一个字符串或数字，如上所述。这使得动态计算值变得容易。与所有回调一样，该函数接收 ScrollTrigger 实例本身作为唯一参数，因此您可以将位置基于前一个 ScrollTrigger 的末尾，例如`start: self => self.previous().end` |
| end              | String \| Number \| Function                                 | 确定 ScrollTrigger 的结束位置                                | 使用与start相同                                              |
| animation        | Tween \| Timeline                                            | 应由 ScrollTrigger 控制的GSAP [Tween](https://greensock.com/docs/v3/GSAP/Tween)或[Timeline实例](https://greensock.com/docs/v3/GSAP/Timeline) | 每个 ScrollTrigger 仅控制一个动画，但您可以将所有动画包装在单个时间轴中（最佳），或者根据您的喜好创建多个 ScrollTrigger。 |
| pin              | Boolean \| String                                            | 在 ScrollTrigger 处于活动状态期间应固定的元素（或元素的选择器文本），这意味着它将显示为“粘在”其起始位置，而其余内容继续在其下方滚动。 | 只允许一个固定元素，但它可以包含任意数量的元素。设置`pin: true`将导致它固定该`trigger`元素。**警告**不要对固定元素本身进行动画处理，因为这会影响测量结果（ScrollTrigger 针对性能进行了高度优化，并尽可能地进行预先计算）。相反，您可以嵌套事物，以便仅对固定元素内的元素进行动画处理。**注意：**如果您要固定嵌套 *在其中的东西*另一个*也*被固定的元素，请确保您定义了一个`pinnedContainer`，以便 ScrollTrigger 知道相应地偏移开始/结束位置。使用反应？确保进行适当的清理 |
| markers          | Boolean \|  Object                                           | 添加在开发/故障排除过程中有用的标记。                        | `markers: true`使用默认值添加它们（startColor：“green”，endColor：“red”，fontSize：“16px”，fontWeigth：“normal”，indent：0），但您可以使用像markers: {startColor: "white", endColor: "white", fontSize: "18px", fontWeight: "bold", indent: 20}`··只在开发阶段设置` |
| once             | Boolean                                                      | 如果`true`，ScrollTrigger 将在到达结束位置后立即终止自身。   | 这会导致它停止侦听滚动事件，并且有资格进行垃圾回收。这也只会调用 onEnter 最多一次。它不会**杀死**关联的动画。当您只希望动画在向前滚动时播放一次并且永远不会重置或重播时，它非常适合。它还将toggleActions 设置为“play none none none”。 |
| onUpdate         | Function                                                     | 每次 ScrollTrigger 的进度发生变化（意味着滚动位置发生变化）时调用的回调。 | 如果您应用了数字`scrub`，请记住，在滚动位置停止后，关联的动画将继续拖动一段时间，因此，如果您的目标是在动画更新时更新某些内容，最好将 应用于动画`onUpdate`本身比 ScrollTrigger 。[请参阅此处的演示](https://codepen.io/osublake/pen/2152a28cffe2c2c0cca8a3e47f7b21c6?editors=0010) (AirPods)。onUpdate 回调接收一个参数 - ScrollTrigger 实例本身，它具有`progress`、`direction`、`isActive`和 等属性/方法`getVelocity()`。例子： |
| anticipatePin    | Number                                                       | 如果您固定较大的部分/面板，您可能会注意到，当您快速滚动时，固定会出现轻微的延迟。 | 因为大多数现代浏览器在单独的线程上处理滚动重绘，因此在固定时，浏览器可能已经绘制了预固定的内容，使其可见的时间可能为 1/60 秒。解决这个问题的唯一方法是让 ScrollTrigger 监视滚动速度并预测固定，稍微提前应用它以避免未固定内容的闪烁。值`anticipatePin: 1`通常很好，但您可以减少或增加该数字来控制固定的提前时间。然而，在许多情况下，您不需要任何预期Pin（默认值为0）。 |
| scrub            | Boolean \| *Number*                                          | 将动画的进度直接链接到滚动条，因此它的作用就像一个滑块。您可以应用平滑，以便播放头需要一点时间才能赶上滚动条的位置！ | **布尔值**-`scrub: true`将动画的进度直接链接到 ScrollTrigger 的进度。**Number** - 播放头“赶上”所需的时间（以秒为单位），因此`scrub: 0.5`会导致动画的播放头需要 0.5 秒才能赶上滚动条的位置。这对于解决问题非常有用。 |
| snap             | *Number* \| *Array* \| *Function* \| *Object* \| *"labels"* \| *"labelsDirectional"* | 允许您在用户停止滚动后捕捉到某些进度值（0 到 1 之间）。因此`snap: 0.1`将以 0.1 的增量（10%、20%、30% 等）捕捉。`snap: [0, 0.1, 0.5, 0.8, 1]`只会让它取决于这些特定进度值之一。 | 它可以是以下任何一个：<br />**数字**-`snap: 0.1`以 0.1 为增量捕捉（10%、20%、30% 等）。如果您有一定数量的部分，只需执行`1 / (sections - 1)`.<br />**数组**-`snap: [0, 0.1, 0.5, 0.8, 1]`在上次滚动的方向上捕捉到数组中最接近的进度值（除非您设置`directional: false`）。<br />**函数**-`snap: (value) => Math.round(value / 0.2) * 0.2`将自然目标值（基于速度）输入到函数中，并使用返回的任何内容作为最终进度值（在本例中增量为 0.2），因此您可以运行您想要的任何逻辑。这些值应始终介于 0 和 1 之间，表示动画的进度，因此 0.5 位于中间。<br />    **“标签”** -`snap: "labels"`捕捉到时间线中最近的标签（当然，动画必须是带有标签的时间线）<br />         **“labelsDirectional”** -`snap: "labelsDirectional"`捕捉到时间线中最近滚动方向上最接近的标签。因此，如果您向下一个标签滚动一点（然后停止），即使当前滚动位置在技术上最接近当前/最后一个标签，它也会捕捉到该方向的下一个标签。这可以让用户感觉更直观。<br />**对象**- 与 一样snap: {snapTo: "labels", duration: 0.3, delay: 0.1, ease: "power1.inOut"}，可以使用以下任何属性完全自定义（仅需要“snapTo”)```更多属性前往官网查看``` |
|                  |                                                              |                                                              |                                                              |



平滑展开——实例

> 案例分析 ： 当目标触发器启动时，图片从中间向两边散开
>
> ```html
> <div class="accordionBox">
>     <div class="selectBox">
>         <img class="pic1" src="./素材2.png" alt="">
>         <img class="pic2" src="./素材2.png" alt="">
>         <img class="pic3" src="./素材2.png" alt="">
>     </div>
> </div>
> <style>
>     .accordionBox{
>     position: relative;
>     display: flex;
>     justify-content: center;
>     width: 100vw;
>     height: 100vh;
>     background-color: aqua;
> }
> .selectBox{
>     position: absolute;
>     display: flex;
>     justify-content: center;
>     align-items: center;
>     width: 50%;
>     height: 100%;
> }
> .selectBox > img{
>     position: absolute;
> }
> </style>
> <script>
>     let t2 = gsap.timeline()
>     t2.fromTo('.pic2',{width:'12em'},{width:'11em',left:0,duration:2,ease:'power1'})
>     .fromTo('.pic1',{width:'12em'},{width:'11em',right:0,duration:2,ease:'power1'},'<');
>     ScrollTrigger.create({
>     trigger:'.accordionBox',
>     start:'top center',
>     end:'bottom bottom',
>     animation:t2,
>     markers:true,
>     pin:false,
>     scrub: true,
>     anticipatePin: 1, 
> })
> </script>
> ```

## 交错动画

