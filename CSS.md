## CSS



### 两种盒模型box-sizing⭐ 

**content-box **  

默认值，其中设置的width 和height是只包含了内容的宽高（content）,但不包含内边距（padding）、边框（border）、外边距（margin）

**border-box**   

其中设置的width和height是包含内容（content）、和padding、border**但是不包含margin**





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

类选择器 10

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





### css两栏布局的实现

以左边宽度固定为 200px 为例

（1）利用浮动，将左边元素宽度设置为 200px，并且设置向左浮动。将右边元素的 margin-left 设置为 200px，宽度设置为 auto（默认为 auto，撑满整个父元素）。

（2）第二种是利用 flex 布局，将左边元素的放大和缩小比例设置为 0，基础大小设置为 200px。将右边的元素的放大比例设置为 1，缩小比例设置为 1，基础大小设置为 auto。

（3）第三种是利用绝对定位布局的方式，将父级元素设置相对定位。左边元素设置为 absolute 定位，并且宽度设置为 200px。将右边元素的 margin-left 的值设置为 200px。

（4）第四种还是利用绝对定位的方式，将父级元素设置为相对定位。左边元素宽度设置为 200px，右边元素设置为绝对定位，左边定位为 200px，其余方向定位为 0。



### css 三栏布局的实现

这里以左边宽度固定为100px，右边宽度固定为200px为例。

（1）利用绝对定位的方式，左右两栏设置为绝对定位，中间设置对应方向大小的margin的值。

（2）利用flex布局的方式，左右两栏的放大和缩小比例都设置为0，基础大小设置为固定的大小，中间一栏设置为auto。

（3）利用浮动的方式，左右两栏设置固定大小，并设置对应方向的浮动。中间一栏设置左右两个方向的margin值，注意这种方式，中间一栏必须放到最后。

（4）圣杯布局，利用浮动和负边距来实现。父级元素设置左右的padding，三列均设置向左浮动，中间一列放在最前面，宽度设置为父级元素的宽度，因此后面两列都被挤到了下一行，通过设置margin负值将其移动到上一行，再利用相对定位，定位到两边。

（5）双飞翼布局，双飞翼布局相对于圣杯布局来说，左右位置的保留是通过中间列的margin值来实现的，而不是通过父元素的padding来实现的。本质上来说，也是通过浮动和外边距负值来实现的。









### 圣杯布局和双飞翼布局 ⭐ 

**圣杯布局**

```html
<div id="header"></div>
<div id="container">
  <div id="center" class="column"></div>
  <div id="left" class="column"></div>
  <div id="right" class="column"></div>
</div>
<div id="footer"></div>
```

```css
body {
  min-width: 550px;
}

#container {
  padding-left: 200px; 
  padding-right: 150px;
}

#container .column {
  float: left;
}

#center {
  width: 100%;
}

#left {
  width: 200px; 
  margin-left: -100%;
  position: relative;
  right: 200px;
}

#right {
  width: 150px; 
  margin-right: -150px; 
}

#footer {
  clear: both;
}
```



**双飞翼布局**

```html
<body>
  <div id="header"></div>
  <div id="container" class="column">
    <div id="center"></div>
  </div>
  <div id="left" class="column"></div>
  <div id="right" class="column"></div>
  <div id="footer"></div>
<body>
```

```css
body {
  min-width: 500px;
}

#container {
  width: 100%;
}

.column {
  float: left;
}
        
#center {
  margin-left: 200px;
  margin-right: 150px;
}
        
#left {
  width: 200px; 
  margin-left: -100%;
}
        
#right {
  width: 150px; 
  margin-left: -150px;
}
        
#footer {
  clear: both;
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





