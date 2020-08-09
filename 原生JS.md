## 原生JS

### ES6 语法知道哪些，分别怎么用

https://fangyinghang.com/es-6-tutorials/

let const 展开运算符 解构赋值 模块导入导出 class继承 promise symbol,set数据类型



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



### ==与===的区别

"==" 就代表会先把两端的变量试图转换成相同类型，然后再比较；

"===" 就代表会直接去比较类型是否相同，如果类型相同则继续比较值是否相同。



==操作符的强制类型转换规则，看看就好

```
（1）字符串和数字之间的相等比较，将字符串转换为数字之后再进行比较。

（2）其他类型和布尔类型之间的相等比较，先将布尔值转换为数字后，再应用其他规则进行比较。

（3）null 和 undefined 之间的相等比较，结果为真。其他值和它们进行比较都返回假值。

（4）对象和非对象之间的相等比较，对象先调用 ToPrimitive 抽象操作后，再进行比较。

（5）如果一个操作值为 NaN ，则相等比较返回 false（ NaN 本身也不等于 NaN ）。

（6）如果两个操作值都是对象，则比较它们是不是指向同一个对象。如果两个操作数都指向同一个对象，则相等操作符返回 true，否则，返回 false。
```







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

* 只接受对象作为健名（null除外），不接受其他类型的值作为健名

* 健名所指向的对象，不计入垃圾回收机制

* 不能遍历，方法同get,set,has,delete



###   JS的数据类型及存放位置

* **Number**

* **string**

* **Boolean**

* **Null**

* **Undefined**

* **Symbol**（ES6中新引入的新类型---可以用来创建匿名的对象属性，代表创建后独一无二且不可变的数据类型，它的出现我认为主要是为了解决可能出现的全局变量冲突的问题。）

* **BigInt**（它可以表示任意精度格式的整数）

  原始类型存储的都是值，是没有函数可以调用的，`typeof null`会输出`object`，是JS存在的一个bug



（一共有8种数据类型，其中7种是原始类型）



栈：原始数据类型（Undefined、Null、Boolean、Number、String）

堆：引用数据类型（对象、数组和函数）


### 判断数据类型

**typeof（原始数据类型）**

它返回表示数据类型的**字符串**

```js
typeof(1)                              //number
typeof("1")                            //string
typeof(true)                           //boolean
typeof(undefined)                      //undefined
typeof(null)                           //object
```

**注释：**您也许会问，为什么 typeof 运算符对于 null 值会返回 "object"。这实际上是 JavaScript 最初实现中的一个错误，然后被 ECMAScript 沿用了。现在，null 被认为是对象的占位符，从而解释了这一矛盾，但从技术上来说，它仍然是原始值。



**instanceof（引用类型）**

原理 因为A instanceof B 可以判断A是不是B的实例，返回一个**布尔值**，由构造类型判断出数据类型

```js
console.log(arr instanceof Array ); // true
console.log(date instanceof Date ); // true
console.log(fn instanceof Function ); // true
//注意： instanceof 后面一定要是对象类型，大小写不能写错，该方法试用一些条件选择或分支
```



**使用`Object.prototype.toString.call()`来判断值的类型**

可以**通用**的来判断原始数据类型和引用数据类型

```js
Object.prototype.toString.call({name:'Jack'}) // [object Object]
Object.prototype.toString.call(function(){}) // [object Function]
Object.prototype.toString.call(/name/) // [object RegExp]
```

而对于基本类型：

```js
Object.prototype.toString.call('abc') // [object String]
Object.prototype.toString.call(12) // [object Number]
Object.prototype.toString.call(true) // [object Boolean]
```

基本类型值是没有构造函数的，为什么也能返回构造函数名呢？这是因为在`toString`被调用时 JavaScript 将基本类型值转换成了包装类型。

而对于`null`和`undefined`：

```js
Object.prototype.toString.call( null );			// "[object Null]"
Object.prototype.toString.call( undefined );	// "[object Undefined]"
```

虽然 JavaScript 中没有`Null()`和`Undefined`构造器，但是 JavaScript 也为我们处理这这两种情况。




### 什么是原型，什么是原型链⭐

**原型**

我们创建的每个函数都有一个 `prototype(原型)` 属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。

**原型链**

1.每一个构造函数都有一个**prototype**属性，称之为显式原型；
2.每一个引用类型都有一个__proto__属性，称之为隐式原型；
3.每一个引用类型的__proto__指向他的构造函数的**prototype**；

每一个构造函数也有自己的__proto__，因为函数本身就是一个引用类型，这个构造函数的__proto__又指向他自己构造函数的**prototype**，这样一级一级往上找就形成了原型链；

![img](https://cdn.nlark.com/yuque/0/2018/png/199663/1544807307596-1e74bf82-9587-458b-bcff-62dfd57b0c87.png){:height="50%" width="50%"}





### 同步异步的区别

**异步**不会阻塞代码的执行，使用场景：网络请求&定时任务

**同步**会阻塞代码执行

**同步异步**

首先来解释同步和异步的概念，这两个概念与消息的通知机制有关。也就是同步与异步主要是从**消息通知机制**角度来说的。

所谓同步就是一个任务的完成需要依赖另外一个任务时，只有等待被依赖的任务完成后，依赖的任务才能算完成，这是一种可靠的任务序列。要么成功都成功，失败都失败，两个任务的状态可以保持一致。

所谓异步是不需要等待被依赖的任务完成，只是通知被依赖的任务要完成什么工作，依赖的任务也立即执行，只要自己完成了整个任务就算完成了。至于被依赖的任务最终是否真正完成，依赖它的任务无法确定，所以它是不可靠的任务序列。



**阻塞非阻塞**

阻塞和非阻塞这两个概念与**程序（线程）等待消息通知(无所谓同步或者异步)时的状态**有关。也就是说阻塞与非阻塞主要是程序（线程）等待消息通知时的状态角度来说的。

阻塞调用是指调用结果返回之前，当前线程会被挂起，一直处于等待消息通知，不能够执行其他业务。函数只有在得到结果之后才会返回。



### 异步编程方案（有待完善）

1.JS 异步编程进化史：callback -> promise -> generator(*|yield) -> async + await

2.async/await 函数的实现，就是将 Generator 函数和自动执行器，包装在一个函数里。

3.async/await可以说是异步终极解决方案了。



Promise 是异步编程的一种解决方案，解决了回调地狱的问题

所谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。

**特点**

* 对象的状态不受外界影响。`Promise`对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）。
* 一旦状态改变，就不会再变







### 这段代码里的 this 是什么？⭐

this的值是在**函数执行时**确定的

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

`call`和`apply`改变了函数的this上下文后便**执行该函数**，而`bind`则是**返回**改变了上下文后的一个**函数**。

他们俩之间的差别在于参数的区别，`call`和`apply`的第一个参数都是要改变上下文的对象，而`call`从第二个参数开始以参数列表的形式展现，`apply`则是把参数放在一个数组里面作为它的第二个参数。

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

**闭包的作用**
1.可以在函数外调用闭包函数，访问到函数内的变量，可以用这种方法来创建私有变量
2.保护变量不被内存回收机制回收



**闭包的缺点**
闭包长期占用内存，内存消耗很大，可能导致内存泄露



**立即执行函数**就是

1. 声明一个匿名函数
2. 马上调用这个匿名函数

只有一个作用：创建一个独立的作用域。









### async/await 怎么用，如何捕获异常？ 

**async**

ES2017 标准引入了 async 函数，使得异步操作变得更加方便。

async 函数是什么？一句话，它就是 Generator 函数的语法糖。

`async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。

**await**

正常情况下，`await`命令后面是一个 **Promise 对象**，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

`await`命令只能用在`async`函数之中，如果用在普通函数，就会报错。

`await`命令后面的`Promise`对象，运行结果可能是`rejected`，所以最好把`await`命令放在`try...catch`代码块中。





### 如何用正则实现 trim()？

```js
function trim(string){
    return string.replace(/^\s+|\s+$/g, '')
}
```







### 垃圾回收机制⭐(有待补充)

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





### requestAnimationFrame的优势是什么？

告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。不需要设置时间间隔，是由系统的时间间隔定义的。大多数浏览器的刷新频率是60Hz(每秒钟反复绘制60次)，循环间隔是1000/60，约等于16.7ms。不需要调用者指定帧速率，**浏览器会自行决定最佳的帧效率**。只被执行一次，这样就不会引起丢帧现象，也不会导致动画出现卡顿的问题。

**语法**：

```js
window.requestanimationframe(callback);
参数callback：下一次重绘之前更新动画帧所调用的函数(即上面所说的回调函数)。
```

**范例**

```js
var start = null;
var element = document.getElementById('SomeElementYouWantToAnimate');
element.style.position = 'absolute';

function step(timestamp) {
  if (!start) start = timestamp;
  var progress = timestamp - start;
  element.style.left = Math.min(progress / 10, 200) + 'px';
  if (progress < 2000) {
    window.requestAnimationFrame(step);
  }
}

window.requestAnimationFrame(step);
```







### 说一下事件循环(Event Loop)？  node的机制有待补充

`js` 是单线程的，所以一次只能执行一个任务，当一个任务需要很长时间时，主线程一直等待任务的执行完成，在执行下个任务是很浪费资源的。

 所以，`js`中任务就被分成两种，一种是同步任务，一种是异步任务。执行步骤如下图所示：

![img](https://user-gold-cdn.xitu.io/2019/6/23/16b83ece9d14eab0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

为了更精细的区分任务，`js`中可以将异步任务划分为宏任务和微任务。
**宏任务（macro-task）**: 同步 script (整体代码)，setTimeout 回调函数, setInterval 回调函数, I/O, UI rendering；
**微任务（micro-task）**: process.nextTick, Promise 回调函数，Object.observe，MutationObserver

其执行的顺序是这样的：

1. 首先 JavaScript 引擎会执行一个宏任务，注意这个宏任务一般是指主干代码本身，也就是目前的同步代码
2. 执行过程中如果遇到微任务，就把它添加到微任务任务队列中
3. 宏任务执行完成后，立即执行当前微任务队列中的微任务，直到微任务队列被清空
4. 微任务执行完成后，开始执行下一个宏任务
5. 如此循环往复，直到宏任务和微任务被清空



Node.js也是单线程的Event Loop，但是它的运行机制不同于浏览器环境。