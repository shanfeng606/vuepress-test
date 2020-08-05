## Vue



### vue的两个核心点

答：**数据驱动、组件系统**
数据驱动：ViewModel，保证数据和视图的一致性。MVVM
组件系统：应用类UI可以看作全部是由组件树构成的。

MVVM 的核心是 ViewModel 层，它就像是一个中转站，负责转换 Model 中的数据对象来让数据变得更容易管理和使用，该层向上与视图层进行双向数据绑定，向下与 Model 层通过接口请求进行数据交互，起承上启下作用。





### watch 和 computed 和 methods 区别是什么？

**computed和watch的区别**

computed:

   * **多个数据影响一个数据**

* 具有**缓存性**，页面重新渲染值不变化,计算属性会立即返回之前的计算结果，而不必再次执行函数

* 最典型的栗子： 购物车商品结算的时候

watch:

* **一个数据影响多个数据**

* **无缓存性**，页面重新渲染时值不变化也会执行

* 栗子：搜索数据



**computed 和 methods**

`computed`是计算属性，`methods`是方法，都可以实现对 data 中的数据加工后再输出。不同的是 `computed` 计算属性是基于它们的依赖进行缓存的， 只有在它的相关依赖发生改变时才会重新求值。

数据量大，需要缓存的时候用 `computed` ；每次确实需要重新加载，不需要缓存时用 `methods` 。





### Vue 有哪些生命周期钩子函数？分别有什么用？

* **beforeCreate**  是new Vue()之后触发的第一个钩子，在当前阶段data、methods、computed以及watch上的数据和方法都不能被访问。

* **created**   在实例创建完成后发生，当前阶段已经完成了数据观测，也就是可以使用数据，更改数据，在这里更改数据不会触发updated函数。可以做一些初始数据的获取，在当前阶段无法与Dom进行交互，如果非要想，可以通过vm.$nextTick来访问Dom。

* **beforeMount**   发生在挂载之前，当前阶段虚拟Dom已经创建完成，即将开始渲染。在此时也可以对数据进行更改，不会触发updated。

* **mounted**   真实的Dom挂载完毕，数据完成双向绑定，可以访问到Dom节点，使用$refs属性对Dom进行操作。

* **beforeUpdate **  数据更新时会调用的钩子函数，此时虽然响应式数据更新了，但是对应的真实 DOM 还没有被渲染

* **updated**    此时 DOM 已经根据响应式数据的变化更新了。

* **beforeDestroy**    发生在实例销毁之前，这时进行善后收尾工作，比如清除计时器。

* **destroyed**    Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。





### **Vue中组件生命周期调用顺序说一下**

组件的调用顺序都是`先父后子`,渲染完成的顺序是`先子后父`。

组件的销毁操作是`先父后子`，销毁完成的顺序是`先子后父`。

**加载渲染过程**

`父beforeCreate -> 父created-> 父beforeMount-> 子beforeCreate-> 子created-> 子beforeMount- > 子mounted-> 父mounted`

**子组件更新过程**

`父beforeUpdate->子beforeUpdate->子updated->父updated`

**父组件更新过程**

`父 beforeUpdate -> 父 updated`

**销毁过程**

`父beforeDestroy->子beforeDestroy->子destroyed->父destroyed`







### Vue 如何实现组件间通信？⭐ 

**方法一：`props`/`$emit`**

父组件A通过props的方式向子组件B传递，B to A 通过在 B 组件中 $emit, A 组件中 v-on 的方式实现。

**方法二：eventBus**

`eventBus` 又称为事件总线，在vue中可以使用它来作为沟通桥梁的概念, 就像是所有组件共用相同的事件中心，可以向该中心注册发送事件或接收事件， 所以组件都可以通知其他组件。

创建一个eventBus

```js
import Vue from 'vue'
export const EventBus = new Vue()
//在要用的组件中导入
import {EventBus} from './event-bus.js'
```

发送事件

```js
methods:{
    additionHandle(){
      EventBus.$emit('addition', {
        num:this.num++
      })
    }
  }
```

接受事件

```js
mounted() {
    EventBus.$on('addition', param => {
      this.count = this.count + param.num;
    })
  }
```

**方法三：`provide`/`inject`**

```
// A.vue
export default {
  provide: {
    name: '传递内容'
  }
}
```

```
// B.vue
export default {
  inject: ['name'],
  mounted () {
    console.log(this.name);  // 传递内容
  }
}
```

**方法四：Vuex**

**方法五：`$children` / `$parent`**



### Vuex是什么？

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。

核心概念：State  Getter Mutation Action Moudle

**state** => 提供唯一的公共数据源，所有共享的数据都要统一放到Store的state中进行储存。`this.$store.state.名称`
**getters** => 用于对store中的数据进行加工处理形成新的数据，类似于Vue中的计算属性，当store中数据发生变化时，getter也会发生变化`this.$store.getters.名称`

**mutations** => 提交更改数据的方法，同步！`this.$store.commit('add')`    --只能通过mutation变更Store数据，不可以直接操作Store的数据
**actions** => 像一个装饰器，包裹mutations，使之可以异步。 `this.$store.dispatch('add')`
**modules** => 模块化Vuex







### MVC与MVVM区别⭐ 

**MVC**(单向通信)

* `View` 传送指令到 `Controller`

* `Controller` 完成业务逻辑后，要求 `Model` 改变状态

* `Model` 将新的数据发送到 `View`，用户得到反馈

![img](https://upload-images.jianshu.io/upload_images/2376645-920ecb14e5f74278.png?imageMogr2/auto-orient/strip|imageView2/2/w/434/format/webp)

**MVVM**(双向通信)

MVVM是`Model-View-ViewModel`缩写，也就是把`MVC`中的`Controller`演变成`ViewModel`。Model层代表数据模型，View代表UI组件，ViewModel是View和Model层的桥梁。`View`和`ViewModel` 是进行绑定的，`View`的变动，自动反映在 `ViewModel`，反之亦然。

而`View` 会把事件传递给`ViewModel`，`ViewModel`去对`Model`**进行操作并接受更新**。从而实现双向通信。

![img](https://upload-images.jianshu.io/upload_images/2376645-66197c4cd472faf2.png?imageMogr2/auto-orient/strip|imageView2/2/w/434/format/webp)









### Vue 数据响应式怎么做到的？⭐ 

Vue在初始化数据时，会使用**`Object.defineProperty`**重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集(收集当前组件的`watcher`)如果属性发生变化会通知相关依赖进行更新操作(`发布订阅`)。

要点

1. 使用 Object.defineProperty 把对象属性全部转为 getter/setter。这些 getter/setter 对用户来说是不可见的，但是在内部它们让 Vue 能够追踪依赖，在 property 被访问和修改时通知变更。
2. Vue 不能检测到对象属性的添加或删除，解决方法是手动调用 Vue.set 或者 this.$set



### Vue.set 是做什么用的？

https://cn.vuejs.org/v2/guide/reactivity.html

Vue 无法检测 property 的添加或移除。由于 Vue 会在初始化实例时对 property 执行 getter/setter 转化，所以 property 必须在 `data` 对象上存在才能让 Vue 将它转换为响应式的。例如：

```js
var vm = new Vue({
  data:{
    a:1
  }
})

// `vm.a` 是响应式的

vm.b = 2
// `vm.b` 是非响应式的
```

对于已经创建的实例，Vue 不允许动态添加根级别的响应式 property。但是，可以使用 `Vue.set(object, propertyName, value)` 方法向嵌套对象添加响应式 property。例如，对于：

```js
Vue.set(vm.someObject, 'b', 2)
```

您还可以使用 `vm.$set` 实例方法，这也是全局 `Vue.set` 方法的别名：

```js
this.$set(this.someObject,'b',2)
```

有时你可能需要为已有对象赋值多个新 property，比如使用 `Object.assign()` 或 `_.extend()`。但是，这样添加到对象上的新 property 不会触发更新。在这种情况下，你应该用原对象与要混合进去的对象的 property 一起创建一个新的对象。

```js
// 代替 `Object.assign(this.someObject, { a: 1, b: 2 })`
this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })
```



### Vue的单向数据流

**数据从父级组件传递给子组件，只能单向绑定**

父级 `prop` 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态

**子组件内部不能直接修改从父级传递过来的数据**。

这个 `prop` 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 `prop` 数据来使用。在这种情况下，最好定义一个本地的 `data` 属性并将这个 `prop` 用作其初始值：





### Vue的slot的理解

Vue的插槽slot，分为3种

- 匿名插槽   （默认）
- 具名插槽    `<slot name="xxx"></slot>`  `<template v-slot:xxx></templete>`
- 作用域插槽

前两种很好理解，无论就是子组件里定义一个slot占位符，父组件调用时，在slot对应的位置填充模板就好了。

作用域插槽的慨念，文档却只有一句简单的描述

**有的时候你希望提供的组件带有一个可从子组件获取数据的可复用的插槽。**



### **keep-alive了解吗**

`keep-alive`是`vue2.0`加入的一个特性， 能缓存某个组件，或者某个路由。

1、节省性能消耗，避免一个组件频繁重新渲染，节省开支

2、保存用户状态，比如说：我们在填写收货地址的页面，需要跳转到另一个页面通过定位选择地址信息再返回继续填写，这时候需要缓存收货地址页面，避免跳转页面导致用户数据丢失。

**他有2个属性**

- include - 字符串或正则表达，只有匹配的组件会被缓存
- exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

```html
<keep-alive include="a">
  <component>
    <!-- name 为 a 的组件将被缓存！ -->
  </component>
</keep-alive>
```

**钩子函数**

我们都知道`vue`组件的生命周期会触发`beforeCreate、created 、beforeMount、 mounted`这些钩子函数，但是被缓存的组件或者页面在第一次渲染之后，再次进入不会再触发上面的钩子函数了，而是触发`activated`钩子函数，可以将逻辑放到这里面去做。

同理：离开缓存组件的时候，`beforeDestroy和destroyed`并不会触发，可以使用`deactivated`离开缓存组件的钩子来代替。





### v-show与v-if区别⭐ 

`v-show` 只是在 `display: none` 和 `display: block` 之间切换。无论初始条件是什么都会被渲染出来，后面只需要切换 CSS，DOM 还是一直保留着的。所以总的来说 `v-show` 在初始渲染时有更高的开销，但是切换开销很小，更适合于频繁切换的场景。

`v-if` 的话，当属性初始为 `false` 时，组件就不会被渲染，直到条件为 `true`，并且切换条件时会触发销毁/挂载组件，所以总的来说在切换时开销更高，更适合不经常切换的场景。



### 如何获取dom?

ref="domName"   用法;this.$refs.domName







### v-model的原理

v-model用于表单数据的双向绑定，其实它就是一个语法糖，这个背后就做了两个操作：

* 给当前元素绑定一个`value`属性；
* 给当前元素绑定`input`事件。

```html
<input type="text"   :value="price"   @input="price=$event.target.value">
```









### Vue Router

单页面跳转

https://router.vuejs.org/zh/guide/#html



###  NextTick的理解⭐ 

当你修改了data的值然后马上获取这个dom元素的值，是不能获取到更新后的值，
你需要使用`$nextTick`这个回调，让修改后的data值渲染更新到dom元素之后在获取，才能成功。

使用

```js
<button @click="change()">按钮</button><h1 ref="gss">{{msg}}</h1>
//JS
export default{
    name:"app",
    data(){
        return {
            msg:"123"
        }
    },
    methods:{
        change(){
            this.msg = "456";
            console.log(this.refs["gss"].innerHTML)//123
            this.$nextTick(function(){
                console.log(this.refs["gss"].innerHTML)//456
            })
        }
    }
    
}
```





### data为什么必须是一个函数？

一个组件被复用多次的话，也就会创建多个实例。本质上，**这些实例用的都是同一个构造函数**。如果data是对象的话，对象属于引用类型，改动一个实例会影响到其他所有的实例。所以为了保证组件不同的实例之间data不冲突，data必须是一个函数。。



### vue常用的修饰符

.stop：等同于JavaScript中的event.stopPropagation()，防止事件冒泡；
.prevent：等同于JavaScript中的event.preventDefault()，防止执行预设的行为（如果事件可取消，则取消该事件，而不停止事件的进一步传播）；
.capture：与事件冒泡的方向相反，事件捕获由外到内；
.self：只会触发自己范围内的事件，不包含子元素；
.once：只会触发一次。





### Vue单页面应用（SPA）

> 单页面应用(SPA)

指一个系统只加载一次资源，然后下面的操作交互、数据交互是通过router、ajax来进行，页面并没有刷新；

Vue只有一个html页面，跳转的方式是组件之间的切换

优点：**页面切换快**（页面每次切换跳转时，并不需要做`html`文件的请求，这样就节约了很多`http`发送时延）

缺点：**首屏时间慢**（首屏时需要请求一次`html`，同时还要发送一次`js`请求，两次请求回来了，首屏才会展示出来。相对于多页应用，首屏时间慢。），**SEO差**（搜索引擎只认识`html`里的内容，不认识`js`的内容，而单页应用的内容都是靠`js`渲染生成出来的，搜索引擎不识别这部分内容）



> 多页应用(MPA)

每一次页面跳转的时候，后台服务器都会给返回一个新的`html`文档，这种类型的网站也就是多页网站，也叫做多页应用。

优点：首屏时间快，SEO效果好

缺点：页面切换慢





### Vue监测数组和对象的变化

由于 JavaScript 的限制，Vue **不能检测**数组和对象的变化。尽管如此我们还是有一些办法来回避这些限制并保证它们的响应性。

**对于对象**

对于已经创建的实例，Vue 不允许动态添加根级别的响应式 property。但是，可以使用 **`Vue.set(object, propertyName, value)`** 方法向嵌套对象添加响应式 property。例如，对于：

```
Vue.set(vm.someObject, 'b', 2)
```

还可以使用 `vm.$set` 实例方法，这也是全局 `Vue.set` 方法的别名：

```
this.$set(this.someObject,'b',2)
```

**对于数组**

Vue 不能检测以下数组的变动：

* 当你利用索引直接设置一个数组项时，例如：`vm.items[indexOfItem] = newValue`

解决办法：

```
// Vue.set
Vue.set(vm.items, indexOfItem, newValue)
```

```
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)
```



* 当你修改数组的长度时，例如：`vm.items.length = newLength`

解决办法

```
vm.items.splice(newLength)
```





### 虚拟DOM

**虚拟DOM**简单讲就是讲真实的dom节点用JavaScript来模拟出来，而Dom变化的对比，放到 Js 层来做

具体讲，就是把真实的DOM操作放在内存当中，在内存中的对象里做模拟操作。

当页面打开时浏览器会解析HTML元素，构建一颗DOM树，将状态全部保存起来，在内存当中模拟我们真实的DOM操作，操作完后又会生成一颗dom树，再根据diff算法比较两颗DOM树不同的地方，只渲染一次不同的地方。



**优点：**

- **保证性能下限：**框架的虚拟 DOM 需要适配任何上层 API 可能产生的操作，他的一些 DOM 操作的实现必须是普通的，所以它的性能并不是最优的；但是比起粗暴的 DOM 操作性能要好很多，因此框架的虚拟 DOM 至少可以保证在你不需要手动优化的情况下，依然可以提供还不错的性能，即保证性能的下限。
- **无需手动操作 DOM：**我们不再需要手动去操作 DOM ，只需要写好 View-Model 的代码逻辑，框架会根据虚拟 DOM 和数据双向绑定，帮我们以可预期的方式更新视图，极大提高我们的开发效率。
- **跨平台：**虚拟 DOM 本质上是 javascript 对象，而 DOM 与平台强相关，相比之下，虚拟 DOM 可以进行更方便的跨平台操作，例如服务器渲染、weex 开发等等。

**缺点：**

- **无法进行极致优化：**虽然虚拟 DOM + 合理的优化，足以应对绝大部分应用的性能需求，但在一些性能要求极高的应用中，虚拟 DOM 无法进行针对性的极致优化。比如 VScode 采用直接手动操作 DOM 的方式进行极端的性能优化。





### Diff算法

**diff算法**：找出有必要更新的节点更新，没有更新的节点就不要动

内容：

- 只比较同一级，不跨级比较
- tag不相同，直接删掉重建，不再深度比较
- tag和key，两者都相同，则认为是相同节点，不在深度比较



之前在Virtual DOM中讲到当状态改变了，vue便会重新构造一棵树的对象树，然后用这个新构建出来的树和旧树进行对比。这个过程就是patch。比对得出「差异」，最终将这些「差异」更新到视图上。



https://juejin.im/post/5c4a76b4e51d4526e57da225



### 为什么要使用key？

vue是通过比对组件自身新旧vdom进行更新的。

key的作用是key来给每个节点做一个唯一标识，辅助判断新旧vdom节点在逻辑上是不是同一个对象。

**作用主要是为了更高效的更新虚拟DOM**





### vue-router的两种模式

**hash（默认）**—— 即地址栏 URL 中的 # 符号

* 原理是onhashchage事件，可以在window对象上监听这个事件

```javascript
window.onhashchange = function(event){
  console.log(event.oldURL, event.newURL)
  let hash = location.hash.slice(1)
}
```

**history**

- 利用了HTML5 History Interface 中新增的pushState()和replaceState()方法。
- 需要后台配置支持。如果刷新时，服务器没有响应响应的资源，会刷出404



