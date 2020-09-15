## 原生JS

### ES6 语法知道哪些，分别怎么用

https://fangyinghang.com/es-6-tutorials/

let const 展开运算符 解构赋值 模块导入导出 class继承 promise symbol,set数据类型



### ES6中数组的新方法

1、扩展运算符 ...

2、Array.from()

3、Array,of()    `Array.of`方法用于将一组值，转换为数组。   Array.of(3, 11, 8) // [3,11,8]

4、fill() 填充数组

5、find() 和 findindex()

```
[1, 4, -5, 10].find((n) => n < 0)
// -5
```

6、includes()   返回一个布尔值，表示某个数组是否包含给定的值

7、entries()  /keys()  /values()




### var、let 及 const 区别（相当于变量提升题目）⭐

以下需要记牢（五点）：

* var声明的变量会挂载在window上，而let和const声明的变量不会

* var声明变量存在变量提升，let和const不存在变量提升

  **块级作用域+不允许重复声明+暂存死区**

* let和const声明形成块作用域，而var不存在此作用域

* 同一作用域下let和const不能声明同名变量，而var可以

* let、const存在暂存死区


const 定义的基本数据类型的变量不能修改，但引用类型可以修改指向的内容，但不能修改指针指向


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


为什么要变量提升

1、提高性能，让函数可以在执行时预先为变量分配栈空间

在JS代码执行之前，会进行语法检查和预编译，并且这一操作只进行一次。这么做就是为了提高性能，如果没有这一步，那么每次执行代码前都必须重新解析一遍该变量（函数），而这是没有必要的，因为变量（函数）的代码并不会改变，解析一遍就够了。

2、声明提升还可以提高JS代码的容错性，使一些不规范的代码也可以正常执行


### 为什么0.1+0.2！==0.3

因为 0.1 和 0.2 被转成二进制后会无限循环，由于JS中位数的限制多余的位数会被截掉，就出现了精度损失。
解决方法：**toFixed()，toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。**



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

### null与undefined区别

**null表示"没有对象"，即该处不应该有值。**典型用法是：

```
（1） 作为函数的参数，表示该函数的参数不是对象。

（2） 作为对象原型链的终点。
```

**undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。**典型用法是：

```
（1）变量被声明了，但没有赋值时，就等于undefined。

（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。

（3）对象没有赋值的属性，该属性的值为undefined。

（4）函数没有返回值时，默认返回undefined。
```

摘自阮一峰：

https://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html

undefined !== null  //true
undefined == null  //true







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


### JavaScript 中 Map 和 Object 的区别

1：Object对象有原型， 也就是说他有默认的key值在对象上面， 除非我们使用Object.create(null)创建一个没有原型的对象
2：在Object对象中， 只能把String和Symbol作为key值， 但是在Map中，key值可以是任何基本类型的值或者对象
3：通过Map中的size属性， 可以很方便地获取到Map长度， 要获取Object的长度， 你只能用别的方法了

https://blog.csdn.net/liangchuannan/article/details/70053038　　



### JavaScript数组的迭代方法map,filter。。。

map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

forEach() 方法对数组的每个元素执行一次提供的函数。

some() 和 every() 方法不会改变原始数组。





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
string：基本包装类型


### 基本类型跟引用类型的区别

 **声明变量时不同的内存分配：**一个在栈，一个堆

**不同的内存分配机制也带来了不同的访问机制**：原始类型可以直接访问，引用类型按引用访问

 **复制变量时的不同**：基本类型复制出独立数据，引用类型复制的一个指针





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
**原理**

**所有类在继承Object的时候，改写了toString()方法。** Object原型上的方法是可以输出数据类型的。因此我们想判断数据类型时，也只能使用原始方法。继而有了此方法：`Object.prototype.toString.call(obj)`



### 如何理解js中基本数据类型的值不可变

**在 JavaScript 中，字符串的值是不可变的，这意味着一旦字符串被创建就不能被改变**

栈创建的时候，大小是确定的

而堆的大小是不确定的，需要的话可以不断增加




### javascript对象的几种创建方式

1、字面量方式  {}

2、调用系统的构造函数 new Object()

3、Object.create()也可以用于创建对象

4、自定义构造函数的方式

```js
function Student(name,age,ID,sex){
    this.name=name;
    this.age=age;
    this.ID=ID;
    this.sex=sex;
    this.sayHi=function(){
    	console.log("您好！");
    };
}
        //创建对象--->实例化一个对象，同时对属性进行初始化。
        //    1.开辟空间存储对象
        //    2.把this设置为当前的对象
        //    3.设置属性和方法的值
        //    4.把this对象返回
        var stu3=new Student("小天",18,20181113,"男");
```

5、工厂模式创建对象

```js
function student(name,age,ID,sex){
    var obj = new Object();
    obj.name=name;
    obj.age=age;
    obj.ID=ID;
    obj.sex=sex;
    obj.sayHi=function(){
    	console.log("您好！");
    };
    return obj;
}
var stu4=student("小菊",21,20181114,"女");
```

工厂模式和自定义构造函数创建对象的区别：

![img](https://img-blog.csdn.net/20180622113822343?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NsZWVwd2Fsa2VyXzE5OTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)








### 什么是原型，什么是原型链⭐

**原型**

我们创建的每个函数都有一个 `prototype(原型)` 属性，这个属性是一个指针，指向一个原型对象。其实原型对象就只是个普通对象，里面存放着所有实例对象需要共享的属性和方法！

```js
function Person(name,age){
	this.name = name;	//不需要共享的属性和方法放在构造函数里
}
Person.prototype.sex = 'female';    //prototype属性，存放所有实例共享的属性与方法

var person1 = new Person("Summer");
var person2 = new Person("Lily");

console.log(person1.sex)      // female
console.log(person2.sex)      // female

Person.prototype.sex = 'male';      //修改prototype属性会影响它的所有实例的sex的值！！

console.log(person1.sex)      // male
console.log(person2.sex)      // male
```



**原型链**

当访问一个对象的某个属性时，会先在这个对象本身属性上查找，如果没有找到，则会去它的__proto__隐式原型上查找，即它的构造函数的prototype，如果还没有找到就会再在构造函数的prototype的__proto__中查找，这样一层一层向上查找就会形成一个链式结构，我们称为原型链。
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



### 异步编程方案

1.JS 异步编程进化史：callback -> promise -> generator(*|yield) -> async + await

2.**async/await 函数的实现**，`async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。

* 内置执行器，不需要像generate函数，需要调用next方法

* 更好的语义，`async`表示函数里有异步操作，`await`表示紧跟在后面的表达式需要等待结果
* 更广的适用性。`async`函数的`await`命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）。
* 返回值是 Promise。你可以用`then`方法指定下一步的操作。

3.async/await可以说是异步终极解决方案了。



#### promise对象

1. 作用： 解决异步回调嵌套问题(回调地狱)，将异步的流程用同步的形式表达出来
2. 思想：
   - 给promise设置的三种状态： pending, fullfilled, rejected
   - 通过异步任务的执行结果动态的去修改promise的状态
   - promise状态的改变可以去then方法中的成功或者失败的回调
   - 可以通过resolve，reject调用的时候将数据传递给成功或者失败的回调

```js
let promise = new Promise((resolve, reject) => {
    //初始化promise的状态为pending---->初始化状态
    console.log('1111');//同步执行
    //启动异步任务
    setTimeout(function () {
        console.log('3333');
        //resolve('atguigu.com');//修改promise的状态pending---->fullfilled（成功状态）
        reject('xxxx');//修改promise的状态pending----->rejected(失败状态)
    },1000)
});
promise.then((data) => {
    console.log('成功了。。。' + data);
}, (error) => {
    console.log('失败了' + error);
});
console.log('2222');
```

#### Generator函数

1. 概念：
   1、ES6提供的解决异步编程的方案之一
   2、Generator函数是一个状态机，内部封装了不同状态的数据，
   3、用来生成遍历器对象
   4、可暂停函数`(惰性求值)`,`yield可暂停`，`next方法可启动`。每次返回的是yield后的表达式结果
2. 特点：
   1、function 与函数名之间有一个星号
   2、内部用yield表达式来定义不同的状态
   例如：
   function* generatorExample(){
   let result = yield ‘hello’; // 状态值为hello
   yield ‘generator’; // 状态值为generator
   }
   3、generator函数返回的是指针对象(iterator)，而不会执行函数内部逻辑
   4、调用next方法函数内部逻辑开始执行，遇到yield表达式停止，返回{value: yield后的表达式结果/undefined, done: false/true}
   5、再次调用next方法会从上一次停止时的yield处开始，直到最后
   6、yield语句返回结果通常为undefined， 当调用next方法时传参内容会作为启动时yield语句的返回值。 （此方法过于繁琐不推荐使用）

```js
function* myGenerator(){
    console.log('开始');
    let result=yield;
    console.log(result); //hello
    console.log('暂停了');
    yield  '你好';
    console.log('end');
    return "end";
}
let Mg= myGenerator();
console.log(Mg.next());
console.log(Mg.next('hello'));//需调用next重新启动，并且可以传参。
console.log(Mg.next());
```

#### async函数

1. 作用: 解决异步回调
2. 语法：

```js
async function foo(){
    await 异步操作;
    await 异步操作；
}
```

1. 通常和promise配合使用，
2. async代表异步， await等待异步执行

- 异步任务执行成功以后才会执行后续的代码返回的
- 根据promise实例对象的状态决定的
  注意点：awit返回值，async的返回值为Promise

```js
async function foo(){
    return new Promise((resolve,reject)=>{
        console.log("我是promise");
        setTimeout(resolve,1000);	
    })
}
async function test(){
    console.log("开始执行");
    await foo();
    console.log("执行完毕");
}

test();
```


### async/await 怎么用，如何捕获异常？ 

**async**

ES2017 标准引入了 async 函数，使得异步操作变得更加方便。

async 函数是什么？一句话，它就是 Generator 函数的语法糖。

`async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。

**await**

正常情况下，`await`命令后面是一个 **Promise 对象**，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。

`await`命令只能用在`async`函数之中，如果用在普通函数，就会报错。

`await`命令后面的`Promise`对象，运行结果可能是`rejected`，所以最好把`await`命令放在`try...catch`代码块中。





### Promise原理

阮一峰ES6中的解释：

Promise 是异步编程的一种解决方案，解决了回调地狱的问题

所谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件的结果（通常是一个异步操作）。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

**特点**

* 对象的状态不受外界影响。`Promise`对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）。
* 一旦状态改变，就不会再变



**then**

Promise 实例具有`then`方法，也就是说，`then`方法是定义在原型对象`Promise.prototype`上的。它的作用是为 Promise 实例添加状态改变时的回调函数。前面说过，`then`方法的第一个参数是`resolved`状态的回调函数，第二个参数（可选）是`rejected`状态的回调函数。

`then`方法返回的是一个新的`Promise`实例（注意，不是原来那个`Promise`实例）。因此可以采用**链式写法**，即`then`方法后面再调用另一个`then`方法。


阮一峰原文 https://es6.ruanyifeng.com/#docs/promise



### proxy的理解

proxy代理，扩展（增强）对象的一些功能：比如Vue中拦截等

```js
//语法
new Proxy(target,handler);
let obj=new Proxy(被代理的对象，对代理的对象做什么操作)
handler:{
	set(){},  //设置的时候执行
	get(){},  //获取的时候执行
	deleteProperty(){}
    has(){}
    ...
}
```

```js
//实例
let obj={
	name:'aaa'
}
let newObj=new Proxy(obj,{
	get(target,property){
		return target[property]
	}
})
console.log(newObj.name)
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


### this指向的形式4种

a.如果是一般函数,this指向全局对象window

b.在严格模式下"use strict",为undefined

c.对象的方法里调用,this指向调用该方法的对象

d.构造函数里的this,指向创建出来的实例

e.箭头函数，指向外面




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

2. 如何捡垃圾（**标记清除法和引用计数法**）

   （遍历和计数，只是不同的算法而已）（从全局作用域开始，把所有遇到的变量都标记一下，如果这些变量引用了其他变量，那就再标记，直到早不到新的对象。标记完后将所有没有标记的对象清除掉）（另一种方法计数标记法，引用与否加1减1）

   

   https://www.nowcoder.com/interview/ai/report?roomId=244768



   



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


### JS为啥是单线程的

JavaScript语言的一大特点是单线程，也就是说，**同一时间只能做一件事情**。

这与它的用途有关，作为浏览器脚本语言，JavaScript 的主要用途是与用户互动，以及操作DOM，这决定了它只能是单线程，否则会带来很复杂的同步问题。

比如，假如JavaScript同时有两个线程，一个线程在某个DOM节点上添加了内容，而另一个线程删除了该节点，这时浏览器应该以哪个线程为准？




### 说一下事件循环(Event Loop)？  

* **` js` 是单线程的**，所以一次只能执行一个任务，当一个任务需要很长时间时，主线程一直等待任务的执行完成，在执行下个任务是很浪费资源的。
* JavaScript在处理异步操作时，利用的是**事件循环机制。**

**其执行的顺序是这样的：**（背下来）

1. 首先 JavaScript 引擎会执行一个宏任务，注意这个宏任务一般是指主干代码本身，也就是目前的同步代码
2. 执行过程中如果遇到微任务，就把它添加到微任务任务队列中
3. 宏任务执行完成后，立即执行当前微任务队列中的微任务，直到微任务队列被清空
4. 微任务执行完成后，开始执行下一个宏任务
5. 如此循环往复，直到宏任务和微任务被清空





 所以，`js`中任务就被分成两种，一种是同步任务，一种是异步任务。执行步骤如下图所示：

![img](https://user-gold-cdn.xitu.io/2019/6/23/16b83ece9d14eab0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

为了更精细的区分任务，`js`中可以将异步任务划分为宏任务和微任务。
**宏任务（macro-task）**: 同步 script (整体代码)，setTimeout 回调函数, setInterval 回调函数, ajax请求回调
**微任务（micro-task）**: process.nextTick, Promise 回调函数，Object.observe，MutationObserver



Node.js也是单线程的Event Loop，但是它的运行机制不同于浏览器环境。




### 类数组与数组的区别

类数组是一个普通对象，真实的数组是Array类型

类数组拥有length属性，不具备数组所具有的方法

**三种转换方法**

* `Array.prototype.slice.call(arrayLike)`
* [...arrayLike]
* Array.from(arrayLike)



### 箭头函数和普通函数的区别

* 箭头函数不会创建自己的this
* 箭头函数继承而来的this指向永远不变
* .call()/.apply()/.bind()无法改变箭头函数中this的指向
* 箭头函数不能作为构造函数的,不能使用new
* 箭头函数不绑定arguments,取而代之用rest参数…解决
* 箭头函数没有原型属性prototype
* 箭头函数不能用作Generator函数，不能使用yeild关键字

### 如何判断两个数组相同

**方法一：**

先排序，再利用  `toString()`  方法

**方法二：**

借助JSON的 `stringify()` 方法



###  如何判断两个对象相同

```js
var deepEqual = function (x, y) {
  // 指向同一内存时
  if (x === y) {
    return true;
  }
  else if ((typeof x == "object" && x != null) && (typeof y == "object" && y != null)) {
    if (Object.keys(x).length != Object.keys(y).length)
      return false;
 
    for (var prop in x) {
      if (y.hasOwnProperty(prop))
      {  
        if (! deepEqual(x[prop], y[prop]))
          return false;
      }
      else
        return false;
    }
 
    return true;
  }
  else 
    return false;
}
```





### js中遍历对象和遍历数组的方法

数组：

* 普通for
* forEach
* map
* for in
* for of        ES6新增功能，支持数组，类数组，字符串

对象

* for in （主要用于遍历对象的可枚举属性，包括自有属性、继承自原型的属性）
* Object.keys      (此方法返回一个数组，元素均为对象自有可枚举的属性)
* Object.getOwnPropertyNames     (此方法用于返回对象的自有属性，包括可枚举和不可枚举的属性)







### 实现图片懒加载的原理

1.首先,不要将图片地址放到src属性中,而是放到其它属性(data-src)中

2.页面加载完成后,根据scrollTop判断图片是否在用户的视野内,如果在,则将data-original属性中的值取出存放到src属性中

3.在滚动事件中重复判断图片是否进入视野;如果进入,则将data-original属性中的值取出存放到src属性中



