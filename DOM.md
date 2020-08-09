## DOM

### property 和 attribute

property：修改对象属性，不会体现到html结构中

attribute：修改html属性，会改变html结构





### 事件绑定的方式

嵌入dom

```
<button onclick="func()">按钮</button>
```

直接绑定

```
btn.onclick = function(){}
```

事件监听

```
btn.addEventListener('click',function(){},false)  一般是false只冒泡
btn.attachEvent('click',handle)
```



 

### DOM事件流与事件委托（代理）

**DOM事件流**

当事件发生在某个DOM节点上时，事件在DOM结构中进行一级一级的传递，这便形成了“流”，事件流便描述了从页面中接收事件的顺序。

**捕获与冒泡**

在捕获阶段，事件由`window`对象开始，一级一级地向下传递，直到传递到最具体的`button`对象上。

事件冒泡阶段与捕获阶段恰好相反，冒泡阶段是从最具体的目标对象开始，一层一层地向上传递，直到`window`对象。

**事件委托**

事件委托又叫事件代理，就是利用**事件冒泡**，只指定一个事件处理程序，就可以管理某一类型的所有事件。

```js
ul.addEventListener('click', function(e){
     if(e.target.tagName.toLowerCase() === 'li'){
         fn() // 执行某个函数
     }
 })
```

bug 在于，如果用户点击的是 li 里面的 span，就没法触发 fn，这显然不对。

高级版：点击 span 后，递归遍历 span 的祖先元素看其中有没有 ul 里面的 li。

**很好记忆的例子：**

简单说，事件委托就是把本来该自己接收的事件委托给自己的上级（父级，祖父级等等）的某个节点，让自己的“长辈们”帮忙盯着，一旦有事件触发，再由“长辈们”告诉自己：“喂，孙子，有人找你~~”。
恩，差不多就是这么个意思，可怜天下父母心。





### JS操作DOM的方法

#### 节点查找（笔试常考）

```
document.getElementById ：根据ID查找元素，大小写敏感，如果有多个结果，只返回第一个；

document.getElementsByClassName ：根据类名查找元素，多个类名用空格分隔，返回一个 HTMLCollection 。注意兼容性为IE9+（含）。另外，不仅仅是document，其它元素也支持 getElementsByClassName 方法；

document.getElementsByTagName ：根据标签查找元素， * 表示查询所有标签，返回一个 HTMLCollection 。

document.getElementsByName ：根据元素的name属性查找，返回一个 NodeList 。

document.querySelector ：返回单个Node，IE8+(含），如果匹配到多个结果，只返回第一个。

document.querySelectorAll ：返回一个 NodeList ，IE8+(含）。

document.forms ：获取当前页面所有form，返回一个 HTMLCollection ；
```

#### DOM元素的基本操作

```
(1).创建:createElement('p');
(2).插入:parentNode.appendChild('p');
(3).删除:removeChild)('p');
(4).更新:replaceChild('p',old);
```







