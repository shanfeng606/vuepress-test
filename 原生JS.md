## 原生JS

### 必考：ES6 语法知道哪些，分别怎么用

https://fangyinghang.com/es-6-tutorials/


### var、let 及 const 区别（相当于变量提升题目）⭐

JavaScript 中，函数及变量的声明都将被提升到函数的最顶部。

JavaScript 中，变量可以在使用后声明，也就是变量可以先使用再声明。

```javascript
console.log(a) // undefined
var a = 1
```

- 函数提升优先于变量提升，函数提升会把整个函数挪到作用域顶部，变量提升只会把声明挪到作用域顶部
- `var` 存在提升，我们能在声明之前使用。`let`、`const` 因为暂时性死区的原因，不能在声明前使用
- `var` 在全局作用域下声明变量会导致变量挂载在 `window` 上，其他两者不会
- `let` 和 `const` 作用基本一致，但是后者声明的变量不能再次赋值


### 为什么0.1+0.2！==0.3

因为 0.1 和 0.2 被转成二进制后会无限循环，由于JS中位数的限制多余的位数会被截掉，就出现了精度损失。



### Map、WeakMap、Set、WeakSet

**Set**

* 成员不能重复，成员可以使任意类型的值

* 只有健值，没有健名，有点类似数组。

* 可以遍历，方法有add, delete，has

**WeakSet**

* 成员只能是对象

* 成员都是弱引用，垃圾回收机制不考虑WeakSet对该对象的引用

* 不能遍历，方法有add, delete,has

**Map**

* 本质上是健值对的集合，类似集合，可以接受任何类型的值作为键名

* 可以遍历，方法很多，可以干跟各种数据格式转换

**WeakMap**

* 直接受对象作为健名（null除外），不接受其他类型的值作为健名

* 健名所指向的对象，不计入垃圾回收机制

* 不能遍历，方法同get,set,has,delete







###   原始类型有哪几种？null 是对象嘛？

* number

* string

* boolean

* null

* undefined

* symbol（ES6中新引入的新类型---可以用来创建匿名的对象属性）

* BigInt（它可以表示任意精度格式的整数）

  原始类型存储的都是值，是没有函数可以调用的，`typeof null`会输出`object`，是JS存在的一个bug

Onject也是一种数据类型，但不是原始类型

（一共有8种数据类型，其中7种是原始类型）


### 什么是原型，什么是原型链⭐

**原型**

简单来说就是有一个构造函数，当用这个构造函数new 一个实例出来的时候，这个实例的原型就是这个构造函数

**原型链**

1.每一个构造函数都有一个prototype属性，称之为显式原型；
2.每一个引用类型都有一个__proto__属性，称之为隐式原型；
3.每一个引用类型的__proto__指向他的构造函数的prototype；

每一个构造函数也有自己的__proto__，因为函数本身就是一个引用类型，这个构造函数的__proto__又指向他自己构造函数的prototype，这样一级一级往上找就形成了原型链；



###  手写new

new做了什么

* 创建一个新的对象
* 继承父类原型上的方法
* 添加父类的属性到新的对象上并初始化. 保存方法的执行结果
* 如果执行结果有返回值并且是一个对象, 返回执行的结果, 否则, 返回新创建的对象

```javascript
function _new(obj, ...rest){
  // 基于obj的原型创建一个新的对象
  const newObj = Object.create(obj.prototype);

  // 添加属性到新创建的newObj上, 并获取obj函数执行的结果.
  const result = obj.apply(newObj, rest);

  // 如果执行结果有返回值并且是一个对象, 返回执行的结果, 否则, 返回新创建的对象
  return typeof result === 'object' ? result : newObj;
}
```


### 同步异步的区别

基于JS是单线程语言

异步不会阻塞代码的执行，使用场景：网络请求&定时任务

同步会阻塞代码执行

Promise解决回调地狱问题

**同步异步**

首先来解释同步和异步的概念，这两个概念与消息的通知机制有关。也就是同步与异步主要是从**消息通知机制**角度来说的。

所谓同步就是一个任务的完成需要依赖另外一个任务时，只有等待被依赖的任务完成后，依赖的任务才能算完成，这是一种可靠的任务序列。要么成功都成功，失败都失败，两个任务的状态可以保持一致。

所谓异步是不需要等待被依赖的任务完成，只是通知被依赖的任务要完成什么工作，依赖的任务也立即执行，只要自己完成了整个任务就算完成了。至于被依赖的任务最终是否真正完成，依赖它的任务无法确定，所以它是不可靠的任务序列。



**阻塞非阻塞**

阻塞和非阻塞这两个概念与**程序（线程）等待消息通知(无所谓同步或者异步)时的状态**有关。也就是说阻塞与非阻塞主要是程序（线程）等待消息通知时的状态角度来说的。

阻塞调用是指调用结果返回之前，当前线程会被挂起，一直处于等待消息通知，不能够执行其他业务。函数只有在得到结果之后才会返回。


### 异步编程方案

1.JS 异步编程进化史：callback -> promise -> generator -> async + await

2.async/await 函数的实现，就是将 Generator 函数和自动执行器，包装在一个函数里。

3.async/await可以说是异步终极解决方案了。


### Promise、Promise.all、Promise.race 怎么用

* 背代码 Promise 用法

```js
function fn(){
     return new Promise((resolve, reject)=>{
         成功时调用 resolve(数据)
         失败时调用 reject(错误)
     })
 }
 fn().then(success, fail).then(success2, fail2)
```

* 背代码 Promise.all 用法

promise1和promise2都成功才会调用success1

```js
Promise.all([promise1, promise2]).then(success1, fail1)
```

* 背代码 Promise.race 用法

  promise1和promise2只要有一个成功就会调用success1；
  promise1和promise2只要有一个失败就会调用fail1；
  总之，谁第一个成功或失败，就认为是race的成功或失败。

```js
Promise.race([promise1, promise2]).then(success1, fail1)
```

  

### 必考：手写函数防抖和函数节流⭐

* 节流（一段时间执行一次之后，就不执行第二次）

```javascript
function throttle(fn, delay){
     let canUse = true
     return function(){
         if(canUse){
             fn.apply(this, arguments)
             canUse = false
             setTimeout(()=>canUse = true, delay)
         }
     }
 }

 const throttled = throttle(()=>console.log('hi'))
 throttled()
 throttled()

```

防抖（一段时间会等，然后带着一起做了）

```js
function debounce(fn, delay){
     let timerId = null
     return function(){
         const context = this
         if(timerId){window.clearTimeout(timerId)}
         timerId = setTimeout(()=>{
             fn.apply(context, arguments)
             timerId = null
         },delay)
     }
 }
 const debounced = debounce(()=>console.log('hi'))
 debounced()
 debounced()
```



### 手写AJAX⭐

```js
 var request = new XMLHttpRequest()
 request.open('GET', '/a/b/c?name=ff', true);
 request.onreadystatechange = function () {
   if(request.readyState === 4 && request.status === 200) {
     console.log(request.responseText);
   }};
 request.send();
```

第1步：创建XMLHttpRequest对象，也就是创建一个异步调用对象
第2步：创建一个新的HTTP请求，并指定该HTTP请求的方法、URL以及验证信息。
第3步：设置响应HTTP状态变化的函数。
第4步：发送HTTP请求。




补充：

- **0**：请求未初始化（还没有调用 `open()`）。
- **1**：请求已经建立，但是还没有发送（还没有调用 `send()`）。
- **2**：请求已发送，正在处理中（通常现在可以从响应中获取内容头）。
- **3**：请求在处理中；通常响应中已有部分数据可用了，但是服务器还没有完成响应的生成。
- **4**：响应已完成；您可以获取并使用服务器的响应了。

jQuery实现jsonp

```js
$.ajax({
	url:'http://api.json',
	dataType:'jsonp',
	jsonpCallback:'callback',
	success:function(data){
		console.log(data)
	}
})
```







### 这段代码里的 this 是什么？⭐

this的值是在函数执行时确定的

1. fn()    （比如setInterval()）
   this => window/global
2. obj.fn()
   this => obj
3. fn.call/apply/bind(xx)
   this => xx
4. new Fn()
   this => 新的对象
5. fn = ()=> {}
   this => 外面的 this


### bind、call、apply的区别

call和apply改变了函数的this上下文后便执行该函数,而bind则是返回改变了上下文后的一个函数。
他们俩之间的差别在于参数的区别，call和apply的第一个参数都是要改变上下文的对象，而call从第二个参数开始以参数列表的形式展现，apply则是把参数放在一个数组里面作为它的第二个参数。
```js
fn.call(this,p1,p2,p3)
fn.apply(this,arguments)
```






### 闭包/立即执行函数是什么？⭐

**闭包的定义**：其实很简单：函数 A 内部有一个函数 B，函数 B 可以访问到函数 A 中的变量，那么函数 B 就是闭包。

```javascript
//闭包隐藏数据，只提供API
function createCache(){
    const data={} //闭包中的数据，被隐藏，不被外接访问
    return{
        set:function(key,val){
            data[key]=val
        },
        get:function(key){
            return data[key] 
        }
    }
}

const c = createCache()
c.set('a',100)
console.log(c.get('a'))
```

**立即执行函数**就是

1. 声明一个匿名函数
2. 马上调用这个匿名函数

只有一个作用：创建一个独立的作用域。



### 必考：什么是 JSONP，什么是 CORS，什么是跨域？

JSONP

1. JSONP是通过 script 标签加载数据的方式去获取数据当做 JS 代码来执行

2. 提前在页面上声明一个函数，函数名通过接口传参的方式传给后台，后台解析到函数名后在原始数据上「包裹」这个函数名，发送给前端。换句话说，JSONP 需要对应接口的后端的配合才能实现。



CORS

CORS是一种协议，它用来约定服务端和客户端那些行为是被服务端允许的。尽管服务端是可以进行验证和认证的，但基本上这是由**客户端浏览器**来保证的。这些对行为的允许是放在应答包的header里面的。

它允许浏览器向跨源服务器，发出 XMLHttpRequest 请求，从而克服了 Ajax 只能同源使用的限制。

**以下是MDN的解释： **

跨域资源共享([CORS](https://developer.mozilla.org/zh-CN/docs/Glossary/CORS)) 是一种机制，它使用额外的 [HTTP](https://developer.mozilla.org/zh-CN/docs/Glossary/HTTP) 头来告诉浏览器 让运行在一个 origin (domain) 上的Web应用被准许访问来自不同源服务器上的指定的资源。当一个资源从与该资源本身所在的服务器**不同的域、协议或端口**请求一个资源时，资源会发起一个**跨域 HTTP 请求**。

比如，站点 http://domain-a.com 的某 HTML 页面通过 [ 的 src ](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Img#Attributes)请求 http://domain-b.com/image.jpg。网络上的许多页面都会加载来自不同域的CSS样式表，图像和脚本等资源。

出于安全原因，浏览器限制从脚本内发起的跨源HTTP请求。 例如，XMLHttpRequest和Fetch API遵循同源策略。 这意味着使用这些API的Web应用程序只能从加载应用程序的同一个域请求HTTP资源，除非响应报文包含了正确CORS响应头。

 （译者注：这段描述不准确，并不一定是浏览器限制了发起跨站请求，也可能是跨站请求可以正常发起，但是返回结果被浏览器拦截了。）

跨域资源共享（ [CORS](https://developer.mozilla.org/zh-CN/docs/Glossary/CORS) ）机制允许 Web 应用服务器进行跨域访问控制，从而使跨域数据传输得以安全进行。现代浏览器支持在 API 容器中（例如 [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 或 [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) ）使用 CORS，以降低跨域 HTTP 请求所带来的风险。



什么是跨域：之前总结过



### 常考：async/await 怎么用，如何捕获异常？ 

**async**

ES2017 标准引入了 async 函数，使得异步操作变得更加方便。

async 函数是什么？一句话，它就是 Generator 函数的语法糖。

`async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。

**await**

正常情况下，`await`命令后面是一个 Promise 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

`await`命令只能用在`async`函数之中，如果用在普通函数，就会报错。

`await`命令后面的`Promise`对象，运行结果可能是`rejected`，所以最好把`await`命令放在`try...catch`代码块中。



### 如何实现浅拷贝，深拷贝？⭐



**浅拷贝**

复制一份，不会引起连锁改变

可以通过 `Object.assign `实现

```javascript
let a = {
  age: 1
}
let b = Object.assign({}, a)
a.age = 2
console.log(b.age) // 1
```

也可以通过展开运算符 `...` 来实现浅拷贝

```javascript
let a = {
  age: 1
}
let b = { ...a }
a.age = 2
console.log(b.age) // 1
```



**深拷贝**

背代码，要点：https://juejin.im/post/5ece6dfbe51d4578a6796fd8

https://segmentfault.com/a/1190000020255831

1. 递归
2. 判断类型
3. 检查环（也叫循环引用）
4. 需要忽略原型

```js
/**
 * 深拷贝
 * @param {Object} obj 要拷贝的对象
 */
function deepClone(obj = {}) {
    if (typeof obj !== 'object' || obj == null) {
        // obj 是 null ，或者不是对象和数组，直接返回
        return obj
    }

    // 初始化返回结果
    let result
    if (obj instanceof Array) {
        result = []
    } else {
        result = {}
    }

    for (let key in obj) {
        // 保证 key 不是原型的属性
        if (obj.hasOwnProperty(key)) {
            // 递归调用！！！
            result[key] = deepClone(obj[key])
        }
    }

    // 返回结果
    return result
}
```





### 常考：如何用正则实现 trim()？

```js
function trim(string){
    return string.replace(/^\s+|\s+$/g, '')
}
```



### 常考：不用 class 如何实现继承？用 class 又如何实现？

不用class

```js
function Animal(color){
     this.color = color
 }
 Animal.prototype.move = function(){} // 动物可以动
 function Dog(color, name){
     Animal.call(this, color) // 或者 Animal.apply(this, arguments)
     this.name = name
 }
 // 下面三行实现 Dog.prototype.__proto__ = Animal.prototype
 function temp(){}
 temp.prototype = Animal.prototype
 Dog.prototype = new temp()

```

用class

```js
class Animal{
     constructor(color){
         this.color = color
     }
     move(){}
 }
 class Dog extends Animal{
     constructor(){
         super()
     }
 }
```



### 常考：如何实现数组去重？

https://www.cnblogs.com/wisewrong/p/9642264.html

1、哈希

2、双重 for 循环（最烂）

3、for...of + includes()

4、Array.sort()

5、new Set([iterable])


### 垃圾回收机制

**垃圾回收的意思可以理解为，将已经不需要的内存释放**
一个主要的方法就是：找出用不到的对象，然后删除它

```js
//假设有一个对象a,占用了100m内存
var a = {/*我占用了100M内存*/}
a = null  // 浏览器就会垃圾回收掉那100m内存 什么时候回收不确定
```

**总结来说就是：把所有指向这块内存的变量全部置为`null`**
1. 什么是垃圾（没有被引用的是垃圾，如果有几个对象相互引用形成环，那也是垃圾）

2. 如何捡垃圾（遍历和计数，只是不同的算法而已）（从全局作用域开始，把所有遇到的变量都标记一下，如果这些变量引用了其他变量，那就再标记，直到早不到新的对象。标记完后将所有没有标记的对象清除掉）（另一种方法计数标记法）

   





### 如何捕获JS中的异常

```js
try{
	//todo
}catch(ex){
	console.error(ex)  //手动捕获
}finally{
	//todo
}
```

```js
//自动捕获
window.onerror=function(message,source,lineNum,colNum,error){
	//第一，对于跨域的js，如cdn的，不会有详细的报错信息
	//第二，对于压缩的js，还要配合sourceMap反查到未压缩的代码的行列
}
```

