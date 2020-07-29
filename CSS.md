## CSS

### 两种盒模型

content-box   border-box(包含边框，内边距)

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

Flex属性  `flex-grow`，`flex-shrink`，和 `flex-basis` 属性

justify-content：`stretch` `flex-start`  `center`  `space-around` `space-between`

align-items : stretch    flex-start    flex-end  center



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



### 圣杯布局和双飞翼布局  ⭐



