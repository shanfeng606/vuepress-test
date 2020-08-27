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

> 创建新节点

```
createDocumentFragment() // 创建一个DOM片段
createElement() // 创建一个具体的元素
createTextNode() // 创建一个文本节点
```

> 添加、移除、替换、插入

```
appendChild()
removeChild()
replaceChild()
insertBefore() // 在已有的子节点前插入一个新的子节点
```

> 查找

```
getElementsByTagName() // 通过标签名称
getElementsByName() // 通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
getElementById() // 通过元素Id，唯一性
```


### DOM Tree与Render Tree之间的区别是什么?

Dom Tree 包含了所有的HTMl标签，包括display：none ，JS动态添加的元素等。

Dom Tree 和样式结构体结合后构建呈现Render Tree。Render Tree 能识别样式，每个node都有自己的style，且不包含隐藏的节点（比如display : none的节点）。









