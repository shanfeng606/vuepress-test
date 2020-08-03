## CSS

### 两种盒模型box-sizing

**content-box **  默认值，其中设置的width 和height是只包含了内容的宽高（content）,但不包含内边距（padding）、边框（border）、外边距（margin）

**border-box** 其中设置的width和height是包含内容（content）、和padding、border**但是不包含margin**



### 如何垂直居中⭐

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

```css
justify-content: flex-start | flex-end | center | space-around | space-between
align-items: stretch | flex-start | flex-end | center
flex-wrap: nowrap | wrap | wrap-reverse;
```





### 必考：BFC 是什么？

block format context ，块级格式化上下文

一块独立渲染区域，内部元素的渲染不会影响边界以外的元素

触发条件：

1. 浮动元素（元素的 float 不是 none）
2. 绝对定位元素（元素的 position 为 absolute 或 fixed）
3. 行内块元素
4. overflow 值不为 visible 的块元素
5. 弹性元素（display为 flex 或 inline-flex元素的直接子元素）



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



### 清除浮动

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



### 解释一下 CSS 里的两个单位：`em` 和 `rem`

1em，等于本元素的字体大小，所以在不同的元素里1em的绝对大小是不一样的。
而1rem，等于根元素的字体大小，在一个页面中，无论在哪个元素上1rem都是一样的。
em 适合于用在需要大小需要跟随字体变化的属性上，比如padding、margin、height、width等等，元素继承了不同的字体大小，这些属性最好也能跟着变化；

rem适用于字体，这样就可以通过改变根元素的字体大小来改变整个页面的字体大小。



### 圣杯布局和双飞翼布局  ⭐
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














