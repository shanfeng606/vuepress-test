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
btn.addEventListener('click',function(){})
```



### 必考:事件委托

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

### 虚拟DOM与Diff算法（有待完善）

https://juejin.im/post/5c4a76b4e51d4526e57da225

**虚拟DOM**简单讲就是讲真实的dom节点用JavaScript来模拟出来，而Dom变化的对比，放到 Js 层来做。

目的：减少不必要的dom操作



**diff算法**：找出有必要更新的节点更新，没有更新的节点就不要动

内容：

- 只比较同一级，不跨级比较
- tag不相同，直接删掉重建，不再深度比较
- tag和key，两者都相同，则认为是相同节点，不在深度比较



之前在Virtual DOM中讲到当状态改变了，vue便会重新构造一棵树的对象树，然后用这个新构建出来的树和旧树进行对比。这个过程就是patch。比对得出「差异」，最终将这些「差异」更新到视图上。

