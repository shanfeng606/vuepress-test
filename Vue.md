## Vue



### vue的两个核心点

答：**数据驱动、组件系统**
数据驱动：ViewModel，保证数据和视图的一致性。MVVM
组件系统：应用类UI可以看作全部是由组件树构成的。

MVVM 的核心是 ViewModel 层，它就像是一个中转站，负责转换 Model 中的数据对象来让数据变得更容易管理和使用，该层向上与视图层进行双向数据绑定，向下与 Model 层通过接口请求进行数据交互，起承上启下作用。



### MVC与MVVM区别

**MVC**(单向通信)

* `View` 传送指令到 `Controller`

* `Controller` 完成业务逻辑后，要求 `Model` 改变状态

* `Model` 将新的数据发送到 `View`，用户得到反馈

![img](https://upload-images.jianshu.io/upload_images/2376645-920ecb14e5f74278.png?imageMogr2/auto-orient/strip|imageView2/2/w/434/format/webp)

**MVVM**(双向通信)

又称状态机制，`View`和`ViewModel` 是进行绑定的，`View`的变动，自动反映在 `ViewModel`，反之亦然。

而`View` 会把事件传递给`ViewModel`，`ViewModel`去对`Model`**进行操作并接受更新**。

![img](https://upload-images.jianshu.io/upload_images/2376645-66197c4cd472faf2.png?imageMogr2/auto-orient/strip|imageView2/2/w/434/format/webp)





### watch 和 computed 和 methods 区别是什么？

**computed 和 methods**

`computed`是计算属性，`methods`是方法，都可以实现对 data 中的数据加工后再输出。不同的是 `computed` 计算属性是基于它们的依赖进行缓存的。计算属性 `computed` 只有在它的相关依赖发生改变时才会重新求值。

数据量大，需要缓存的时候用 `computed` ；每次确实需要重新加载，不需要缓存时用 `methods` 。

**computed和watch的区别**

computed:

   * **多个数据影响一个数据**

* 具有**缓存性**，页面重新渲染值不变化,计算属性会立即返回之前的计算结果，而不必再次执行函数

* 最典型的栗子： 购物车商品结算的时候

watch:

* **一个数据影响多个数据**

* **无缓存性**，页面重新渲染时值不变化也会执行

* 栗子：搜索数据



### Vue 有哪些生命周期钩子函数？分别有什么用？

beforeCreate  钩子函数调用时，是获取不到props或者data中的数据的，因为这些数据初始化都在initState中

created   这一步可以访问之前不能访问的数据（data跟methods），但这时候组件还没有被挂载，所以是看不到的

beforeMount   

mounted（实例挂载到 DOM上，此时可以通过 DOM API 获取到 DOM 节点，$el 属性可以访问。）

beforeUpdate   数据更新时会调用的钩子函数,此时虽然响应式数据更新了，但是对应的真实 DOM 还没有被渲染

updated    此时 DOM 已经根据响应式数据的变化更新了。

beforeDestroy（还没真正被销毁，所有的data，methods，指令，过滤器。。。仍可用）

destroyed    Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。



### Vue 如何实现组件间通信？⭐ 

https://juejin.im/post/5cde0b43f265da03867e78d3

父子：父组件A通过v-on传递数据，子组件B通过props接收父组件A传递的数据， B 组件中通过 $emit 向父组件通信

爷孙：使用两次 v-on 通过爷爷爸爸通信，爸爸儿子通信实现爷孙通信

祖先对所有后代：provide/inject

任意组件：使用 eventBus = new Vue() 来通信，eventBus.$on 和 eventBus.$emit 是主要API

任意组件：使用 Vuex 通信



### Vue 数据响应式怎么做到的？

同vue的双向绑定原理

`vue`是通过`Object.defineProperty()`来实现数据劫持的。

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



### v-show与v-if区别⭐ 

`v-show` 只是在 `display: none` 和 `display: block` 之间切换。无论初始条件是什么都会被渲染出来，后面只需要切换 CSS，DOM 还是一直保留着的。所以总的来说 `v-show` 在初始渲染时有更高的开销，但是切换开销很小，更适合于频繁切换的场景。

`v-if` 的话就得说到 Vue 底层的编译了。当属性初始为 `false` 时，组件就不会被渲染，直到条件为 `true`，并且切换条件时会触发销毁/挂载组件，所以总的来说在切换时开销更高，更适合不经常切换的场景。



### 如何获取dom?

ref="domName"   用法;this.$refs.domName



### 为什么要使用key？

需要使用key来给每个节点做一个唯一标识，diff算法就可以正确的识别此节点。

**作用主要是为了更高效的更新虚拟DOM**

diff的比较方式:

当页面的数据发生变化时，Diff算法只会比较同一层级的节点：

**如果节点类型不同，直接干掉前面的节点，再创建并插入新的节点，不会再比较这个节点以后的子节点了。**

**如果节点类型相同，则会重新设置该节点的属性，从而实现节点的更新。**



### v-model的使用。

v-model用于表单数据的双向绑定，其实它就是一个语法糖，这个背后就做了两个操作：
v-bind绑定一个value属性；
v-on指令给当前元素绑定input事件。

```html
<input type="text"   :value="price"   @input="price=$event.target.value">
```





### Vuex是什么？

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。

核心概念：State  Getter Mutation Action Moudle

**state** => 提供唯一的公共数据源，所有共享的数据都要统一放到Store的state中进行储存。`this.$store.state.名称`
**getters** => 用于对store中的数据进行加工处理形成新的数据，类似于Vue中的计算属性，当store中数据发生变化时，getter也会发生变化`this.$store.getters.名称`

**mutations** => 提交更改数据的方法，同步！`this.$store.commit('add')`    --只能通过mutation变更Store数据，不可以直接操作Store的数据
**actions** => 像一个装饰器，包裹mutations，使之可以异步。 `this.$store.dispatch('add')`
**modules** => 模块化Vuex







###  NextTick⭐ 

当你修改了data的值然后马上获取这个dom元素的值，是不能获取到更新后的值，
你需要使用`$nextTick`这个回调，让修改后的data值渲染更新到dom元素之后在获取，才能成功。



### vue组件中data为什么必须是一个函数？

因为JavaScript的特性所导致，在component中，data必须以函数的形式存在，不可以是对象。

组件中的data写成一个函数，数据以函数返回值的形式定义，这样每次复用组件的时候，都会返回一份新的data，相当于每个组件实例都有自己私有的数据空间，它们只负责各自维护的数据，不会造成混乱。而单纯的写成对象形式，就是所有的组件实例共用了一个data，这样改一个全都改了。



### vue常用的修饰符

.stop：等同于JavaScript中的event.stopPropagation()，防止事件冒泡；
.prevent：等同于JavaScript中的event.preventDefault()，防止执行预设的行为（如果事件可取消，则取消该事件，而不停止事件的进一步传播）；
.capture：与事件冒泡的方向相反，事件捕获由外到内；
.self：只会触发自己范围内的事件，不包含子元素；
.once：只会触发一次。