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



###   原始类型有哪几种？null 是对象嘛？

* number

* string

* boolean

* null

* undefined

* symbol（ES6中新引入的新类型---可以用来创建匿名的对象属性）

* BigInt（它可以表示任意精度格式的整数）

  原始类型存储的都是值，是没有函数可以调用的，`typeof null`会输出`object`，是JS存在的一个bug

Object也是一种数据类型，但不是原始类型

（一共有8种数据类型，其中7种是原始类型）



### 判断数据类型

**typeof**

可以判断数据类型，它返回表示数据类型的字符串（返回结果只能包括number,boolean,string,function,object,undefined）；

可以使用typeof判断变量是否存在（如if(typeof a!="undefined"){...}）；

Typeof 运算符的问题是无论引用的对象是什么类型    它都返回object

```js
typeof {} // object
typeof  [1,2] // object
typeof /\s/ //object
```



**instanceof**

原理 因为A instanceof B 可以判断A是不是B的实例，返回一个布尔值，由构造类型判断出数据类型

```js
console.log(arr instanceof Array ); // true
console.log(date instanceof Date ); // true
console.log(fn instanceof Function ); // true
//注意： instanceof 后面一定要是对象类型，大小写不能写错，该方法试用一些条件选择或分支
```



**使用`Object.prototype.toString`来判断值的类型**

在任何值上调用`Object.prototype.toString`方法，都会返回一个 `[object NativeConstructorName]`格式的字符串。每个类在内部都有一个 `[[Class]]` 属性，这个属性中就指定了上述字符串中的构造函数名。

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

在 JavaScript 中，每个实例对象都有一个私有属性 `Prototype` ，该属性指向了这个实例对象的原型

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
//更直观的写法
promise.then(function(value) {
 // success
}, function(value) {
 // failure
});
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
1.访问其他函数内部变量
2.保护变量不被内存回收机制回收
3.避免全局变量被污染 方便调用上下文的局部变量 加强封装性

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



### 如何实现数组去重？⭐

https://www.cnblogs.com/wisewrong/p/9642264.html

1、哈希

2、双重 for 循环（最烂）

3、for...of + indexOf()或includes()   ，创建一个空数组，元素不存在时push进去

4、Array.sort()    比较相邻元素是否相等，从而排除重复项

5、new Set([iterable])



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





