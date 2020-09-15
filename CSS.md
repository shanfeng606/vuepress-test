## CSS

### CSS3 有哪些新特性？
常用的有：

**圆角（border-radius）**

**阴影（box-shadow）**

**过渡效果（transition）**

**翻转（transform）**

**动画（animation）**

**媒体查询（@media）**

**弹性盒子（flex）**

```
选择器   E:last-child     E:nth-child(n)
圆角	   border-radius:8px
阴影     box-shadow：: 水平方向的偏移量 垂直方向的偏移量 模糊程度 扩展程度 颜色 是否具有内阴影
背景     background-image:url('1.jpg),url('2.jpg')
渐变     background:linear-gradient(方向，开始颜色，结束颜色)
过渡动画  transition:property duration timing-function delay
动画     @keyframes动画帧     
         animation:name duration timing-function delay interation-count direction play-state
变换     rotate()旋转   translate()平移   scale( )缩放   skew()扭曲/倾斜
媒体查询  @media
```


### 有哪些选择器

* 标签选择器
* 类选择器
* id选择器
* 子选择器 >
* 包含选择器：以空格隔开包含关系的元素，(模块名模块名，修饰空格前模块内所有该模块)
* 兄弟选择器 ~
* 相邻选择器 +
* 全局选择器 *
* 群选择器：以，分隔(逗号分隔开需要修饰的模块名)
* 属性选择器：[] ([type=text]修饰属性为type=text的模块)
* 伪类选择器





### 两种盒模型box-sizing⭐ 

**content-box**  

默认值，其中设置的width 和height是只包含了内容的宽高（content）,但不包含内边距（padding）、边框（border）、外边距（margin）

**border-box**   

其中设置的width和height是包含内容（content）、和padding、border**但是不包含margin**

标准盒子模型 ＝ margin + border + padding + width （width = content ）

IE盒子模型（怪异） ＝ margin + width（width = border + padding + content ）




### 如何垂直居中 ⭐ 

一般常见的几种居中的方法有：

对于**宽高固定**的元素

（1）我们可以利用margin:0auto来实现元素的水平居中。

（2）利用绝对定位，设置四个方向的值都为0，并将margin设置为auto，由于宽高固定，因此对应方向实现平分，可以实现水
平和垂直方向上的居中。

（3）利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过margin负值来调整元素
的中心点到页面的中心。

（4）利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过translate来调整元素
的中心点到页面的中心。

（5）使用flex布局，通过align-items:center和justify-content:center设置容器的垂直和水平方向上为居中对
齐，然后它的子元素也可以实现垂直和水平的居中。

对于**宽高不定**的元素，上面的后面两种方法，可以实现元素的垂直和水平的居中。

```css
width: 300px;
position: absolute;
top: 50%;
left: 50%;
margin-left: -150px;
height: 100px;
margin-top: -50px;
```

```css
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%,-50%);
```

```css
display: flex;
justify-content: center;
align-items: center;
```

```css
position: absolute;
width: 300px;
height: 200px;
margin: auto;
top: 0;
bottom: 0;
left: 0;
right: 0;
```



### flex 怎么用，常用属性有哪些？

Flex属性  `flex-grow`（放大比例），`flex-shrink`(缩小比例)，和 `flex-basis` (占据空间) 属性  

`order`(排列顺序)   `flex-direction`  主轴的方向  `flex-flow` 如果一排放不下如何换行

```css
justify-content: flex-start | flex-end | center | space-around | space-between
align-items: stretch | flex-start | flex-end | center
flex-wrap: nowrap | wrap | wrap-reverse;
```
flex兼容性问题

加前缀

**-webkit-**         Safari/Chrome

**-ms-**                IE

**-moz-**              Firefox 

https://cloud.tencent.com/developer/article/1532737




### BFC 是什么？⭐ 

block format context ，块级格式化上下文

一块独立渲染区域，内部元素的渲染不会影响边界以外的元素

**触发条件**：

1. 浮动元素（元素的 float 不是 none）
2. 绝对定位元素（元素的 position 为 absolute 或 fixed）
3. 行内块元素
4. overflow 值不为 visible 的块元素
5. 弹性元素（display为 flex 或 inline-flex元素的直接子元素）

**作用：**

1. 可以包含浮动元素
2. 不被浮动元素覆盖
3. 阻止父子元素的 margin 折叠





### CSS 选择器优先级

内联样式 > 内部样式 > 外部样式 

**选择器的优先权：**

内联样式1000  

ID选择器100

类选择器 10=伪类

元素选择器 1

总结：

* 越具体优先级越高
* 同样优先级写在后面的覆盖写在前面的
* ！important优先级最高，但要少用



### 清除浮动⭐ 

```css
 .clearfix:after{
     content: '';
     display: block; /*或者 table*/
     clear: both;
 }
 .clearfix{
     zoom: 1; /* IE 兼容*/
 }
```

其他方法：**父级div定义overflow:hidden，定义overflow:auto当内部超出时会有滚动条**



### position 的值 relative 和 absolute 定位原点是？

**relative**定位的元素，是相对于元素本身的正常位置来进行定位的。

**absolute**定位的元素，是相对于它的第一个position值为absolute或者relative的父元素的paddingbox来进行定位的。

补充：

fixed（老IE不支持）
生成绝对定位的元素，相对于浏览器窗口进行定位。

static
默认值。没有定位，元素出现在正常的流中



### CSS隐藏元素的方式

* 使用 **display:none;**隐藏元素，渲染树不会包含该渲染对象，因此该元素不会在页面中占据位置，也不会响应绑定的监听事件。

* 使用 **visibility:hidden;**隐藏元素。元素在页面中仍占据空间，但是不会响应绑定的监听事件。

* 使用 **opacity:0;**将元素的透明度设置为 0，以此来实现元素的隐藏。元素在页面中仍然占据空间，并且能够响应元素绑定的监听事件。

* 通过使用绝对定位将元素**移除可视区域内**，以此来实现元素的隐藏。

* 通过**z-index** 负值，来使其他元素遮盖住该元素，以此来实现隐藏。

* 通过 **transform:scale(0,0)**来将元素缩放为 0，以此来实现元素的隐藏。这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。







### `em` 和 `rem`的区别

1em，等于**本元素**的字体大小，所以在不同的元素里1em的绝对大小是不一样的。
而1rem，等于**根元素**的字体大小，在一个页面中，无论在哪个元素上1rem都是一样的。
em 适合于用在需要大小需要跟随字体变化的属性上，比如padding、margin、height、width等等，元素继承了不同的字体大小，这些属性最好也能跟着变化；

rem适用于字体，这样就可以通过改变根元素的字体大小来改变整个页面的字体大小。
**补充：**

rpx微信小程序的css尺寸单位，可根据屏幕进行自适应

在 iPhone6 上，屏幕宽度为375px，共有750个物理像素，则750rpx = 375px = 750物理像素，1rpx = 0.5px = 1物理像素。

也就是说，在iPhone6上，1rpx=1物理像素=0.5px。

DPR=设备像素/css像素（某一方向上）

dpi：像素密度，每英寸点数




### css两栏布局的实现

以左边宽度固定为 200px 为例

（1）利用浮动，将左边元素宽度设置为 200px，并且设置向左浮动。将右边元素的 margin-left 设置为 200px，宽度设置为 auto（默认为 auto，撑满整个父元素）。

（2）第二种是利用 flex 布局，将左边元素的放大和缩小比例设置为 0，基础大小设置为 200px。将右边的元素的放大比例设置为 1，缩小比例设置为 1，基础大小设置为 auto。

（3）第三种是利用绝对定位布局的方式，将父级元素设置相对定位。左边元素设置为 absolute 定位，并且宽度设置为 200px。将右边元素的 margin-left 的值设置为 200px。

（4）第四种还是利用绝对定位的方式，将父级元素设置为相对定位。左边元素宽度设置为 200px，右边元素设置为绝对定位，左边定位为 200px，其余方向定位为 0。



### css 三栏布局的实现

这里以左边宽度固定为100px，右边宽度固定为200px为例。

（1）利用绝对定位的方式，左右两栏设置为绝对定位，中间设置对应方向大小的margin的值。

（2）利用flex布局的方式，左右两栏的放大和缩小比例都设置为0，基础大小设置为固定的大小，中间一栏设置为auto。（flex自带等高布局）

（3）利用浮动的方式，左右两栏设置固定大小，并设置对应方向的浮动。中间一栏设置左右两个方向的margin值，注意这种方式，中间一栏必须放到最后。

（4）**圣杯布局，利用浮动和负边距来实现。**父级元素设置左右的padding，三列均设置向左浮动，中间一列放在最前面，宽度设置为父级元素的宽度，因此后面两列都被挤到了下一行，通过设置margin负值将其移动到上一行，再利用相对定位，定位到两边。

（5）双飞翼布局，双飞翼布局相对于圣杯布局来说，左右位置的保留是通过**中间列的margin值**来实现的，而不是通过父元素的padding来实现的。本质上来说，也是通过浮动和外边距负值来实现的。



### 三列等高布局

**（1）真实等高布局 flex**

技术点：弹性盒子布局flex，默认值就是自带等高布局的特点。

**（2）真实等高布局 table-cell**

技术点：table布局天然就具有等高的特性。

**（3）假等高列布局      使用数值非常大正padding-bottom与负margin-bottom**

实现：设置父容器的overflow属性为hidden。给每列设置比较大的底内边距，然后用数值相似的负外边距消除这个高度。

**（4）绝对定位：top与bottom为0**





### 圣杯布局和双飞翼布局 ⭐ 

**圣杯布局（padding）**

* 三个部分都设定为左浮动，**否则左右两边内容上不去，就不可能与中间列同一行**。然后设置center的宽度为100%(**实现中间列内容自适应**)，此时，left和right部分会跳到下一行
* 通过设置margin-left为负值让left和right部分回到与center部分同一行
* 通过设置相对定位，让left和right部分移动到两边。

```html
<article class="container">
    <div class="center"></div>
    <div class="left"></div>
    <div class="right"></div>
</article>
```

```css
.container {
    padding-left: 220px;//为左右栏腾出空间
    padding-right: 220px;
}
.left {
    float: left;
    width: 200px;
    height: 400px;
    background: red;
    margin-left: -100%;
    position: relative;
    left: -220px;
}
.center {
    float: left;
    width: 100%;
    height: 500px;
    background: yellow;
}
.right {
    float: left;
    width: 200px;
    height: 400px;
    background: blue;
    margin-left: -200px;
    position: relative;
    right: -220px;
}
```



**双飞翼布局（margin）**

双飞翼布局和圣杯布局很类似，不过是在middle的div里又插入一个div，通过调整内部div的margin值，实现中间栏自适应，内容写到内部div中。

```html
<article class="container">
    <div class="center">
        <div class="inner">双飞翼布局</div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
</article>
```

```css
.container {
    min-width: 600px;//确保中间内容可以显示出来，两倍left宽+right宽
}
.center {
    float: left;
    width: 100%;
    height: 500px;
    background: yellow;
}
.center .inner {
    margin: 0 200px; //新增部分
}
.left {
    float: left;
    width: 200px;
    height: 400px;
    background: red;
    margin-left: -100%;
}
.right {
    float: left;
    width: 200px;
    height: 400px;
    background: blue;
    margin-left: -200px;
}
```



### CSS动画

* animation属性

  ```css
  div{
  	animation: myfirst 5s linear 2s infinite alternate;
  }
  @keyframes myfirst{
      0%   {background: red; left:0px; top:0px;}
      25%  {background: yellow; left:200px; top:0px;}
      50%  {background: blue; left:200px; top:200px;}
      75%  {background: green; left:0px; top:200px;}
      100% {background: red; left:0px; top:0px;}
  }
  ```

* transtion属性

  ```css
  语法：transition: property duration timing-function delay;
  //宽度从100变到300
  div{
      width:100px;
      height:100px;
      background:blue;
      transition:width 2s;
  }
  
  div:hover{
  	width:300px;
  }
  ```

### CSS与JS动画优缺点

CSS实现动画：animation transition transform

JS实现动画：setInterval setTimeout requestAnimationFrame

JS动画：控制方便，能做复杂的动画，没有兼容性问题

css动画：代码简单，集中所有的DOM，一次重绘重排，可用硬件加速功能

https://www.cnblogs.com/sarah-wen/p/10801002.html



**CSS动画流畅的原因**

渲染线程分为main thread(主线程)和compositor thread(合成器线程)。

**如果CSS动画只是改变`transform`和`opacity，`**`这时整个CSS动画得以在compositor thread完成（而JS动画则会在main thread执行，然后触发compositor进行下一步操作），所以，当在JS执行一些昂贵的任务时，main thread繁忙，CSS动画由于使用了compositor thread可以保持流畅。`





### CSSSprites原理和优势

将一个页面涉及到的所有图片都包含到一张大图中去，然后利用CSS的background-image，background-repeat，background
-position的组合进行背景定位。

优点：

减少HTTP请求数，极大地提高页面加载速度
增加图片信息重复度，提高压缩比，减少图片大小
更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现

缺点：

图片合并麻烦
维护麻烦，修改一个图片可能需要重新布局整个图片，样式





### CSS实现三角形

```css
.arrow{
	width:0;
    height:0;
	border-right:50px solid transparent;
	border-left:50px solid transparent;
	border-bottom:50px solid red;
}
```



### ::before 和:after 中双冒号和单冒号有什么区别？

在css3中使用单冒号来表示伪类，用双冒号来表示伪元素。但是为了兼容已有的伪元素的写法，在一些浏览器中也可以使用单冒号
来表示伪元素。

伪类一般匹配的是元素的一些特殊状态，如hover、link等，而伪元素一般匹配的特殊的位置，比如after、before等。


### link与import的区别

1，link是XHTML标签，除了可以加载css外还可以加载rss等一些其他事务，而这个@import属于css范畴，只能加载css。

2，link在页面加载的时候他就可以加载css文件，而@import必须等到页面加载完成后才可以加载css。

3，link是XHTML标签，没有任何兼容问题，而@import是在css2.1之后提出的，所以可能存在兼容问题。

4，link支持JavaScript操作dom方式去改变样式，而@import则不支持。

### CSS设置链接样式顺序

正确顺序：“爱恨原则”（LoVe/HAte），即四种伪类的首字母:LVHA。再重复一遍正确的顺序：a:link、a:visited、a:hover、a:active .

解析：a:link,a:visited,a:hover,a:active 分别是什么意思?  

      1. link:连接平常的状态  

      2. visited:连接被访问过之后  

      3. hover:鼠标放到连接上的时候  

   4. active:连接被按下的时候



### 如何画一条0.5px的线

* 直接设置0.5px，在不同的浏览器会有不同的表现
* 缩放：设置1px，然后**scale 0.5**
* 设置box-shadow的第二个参数为0.5px，表示阴影垂直方向的偏移为0.5px      box-shadow: 0 0.5px 0 #000;


### 如何判断浏览器是否支持css3属性

**CSS.supports()方法**

```js
//判断是否支持flex布局
var supportsFlex = CSS.supports("display", "flex");

//判断是否支持rem单位
var supportsRem = CSS.supports("width","1rem");

//判断兼容性属性
var supportsAPS = CSS.supports("animation-play-state")||CSS.supports("-webkit-animation-play-state")||CSS.supports("-ms-animation-play-state")||CSS.supports("-Moz-animation-play-state")||CSS.supports("-o-animation-play-state");
```

**查找document.documentElement.style是否存在要查询的属性**

```js
function isString(value){
    return typeof value == "string";
}
var docStyle = document.documentElement.style;
var supportsAPS = isString(docStyle.animationPlayState)||isString(docStyle.webkitanimationPlayState)||isString(docStyle.MozanimationPlayState)||isString(docStyle.msanimationPlayState)||isString(docStyle.oanimationPlayState);
```





### Flex 与 Grid的区别

**Grid**

Grid在全局布局方面大胜，是元帅
**网格=>二维布局**，以布局为基础，布局自适应，多维联动厉害
独立源：可以设置区域及项目选择区域而与书写文档脱钩=>好维护
网格分层：z-index(可以看成3维)，脱离文档流

**Flex**

Flex在局部布局方面大胜，是大将
**弹性=>一维(多行1.5维)**，以内容为基础，内容自适应，单行联动厉害
order:半个独立源
排版方向或内容排版方面绝对的高手
弹性特点：没有方向，空间自由分配，自动对齐





### scrollHeight, clientHeight, offsetHeight, scrollTop

**scrollHeight**

所有的内容（指图一图中有文字的红色框框内）和内边距，这个内容包括肉眼看不见、溢出、被窗口遮挡的部分；

**clientHeight**

视野内可见的内容和内边距，不包括x轴的滚动条高度、边框、外边距

**offsetHeight**

在clientHeight的基础上， 加上边框和滚动条的高度；

**scrollTop**

滚动条滚动了多少距离（包括之前已滚动过的隐藏内容）就是scrollTop



元素距离文档顶端和左边的偏移值 

document.getBoundingClientRect 

```html
obj.offsetTop //IE firefox
obj.offsetLeft //IE firefox
```







### 重绘（Repaint）和回流（Reflow）⭐ 

* 重绘是当节点需要**更改外观而不会影响布局**的，比如改变 `color` 就叫称为重绘

* 回流是**布局或者几何属性需要改变**就称为回流。需要重新计算渲染树，成本高

回流**必定**会发生重绘，重绘**不一定**会引发回流。回流所需的成本比重绘高的多，改变父节点里的子节点很可能会导致父节点的一系列回流

> **减少重绘和回流(能记多少是多少)**

- **使用 `transform` 替代 `top`**
- **使用 `visibility` 替换 `display: none`** ，因为前者只会引起重绘，后者会引发回流（改变了布局
- **避免使用`table`布局**，可能很小的一个小改动会造成整个 `table` 的重新布局。
- **尽可能在`DOM`树的最末端改变`class`**，回流是不可避免的，但可以减少其影响。尽可能在DOM树的最末端改变class，可以限制了回流的范围，使其影响尽可能少的节点。
- **避免设置多层内联样式**，CSS 选择符**从右往左**匹配查找，避免节点层级过多。
- **将动画效果应用到`position`属性为`absolute`或`fixed`的元素上**，避免影响其他元素的布局
- **避免使用`CSS`表达式**，可能会引发回流。
- **CSS3 硬件加速（GPU加速）**

- **避免频繁操作样式**，最好一次性重写`style`属性，或者将样式列表定义为`class`并一次性更改`class`属性。
- **避免频繁操作`DOM`**，创建一个`documentFragment`，在它上面应用所有`DOM操作`，最后再把它添加到文档中。
- **避免频繁读取会引发回流/重绘的属性**，如果确实需要多次使用，就用一个变量缓存起来。

