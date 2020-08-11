## webpack



### webpack介绍一下

webpack是一个**模块打包器**（module bundler），webpack视HTML，JS，CSS，图片等文件都是一种 **资源** ，每个资源文件都是一个模块（module）文件，webpack就是根据每个模块文件之间的依赖关系将所有的模块打包（bundle）起来。

**作用**

- 对 CommonJS 、 AMD 、ES6的语法做了兼容
- 对js、css、图片等资源文件都支持打包（适合团队化开发）
- 比方你写一个js文件，另外一个人也写一个js文件，需要合并很麻烦，现在交给webpack合并很简单
- 有独立的配置文件webpack.config.js
- 可以将代码切割成不同的chunk，实现按需加载，降低了初始化时间
- 具有强大的Plugin（插件）接口，大多是内部插件，使用起来比较灵活
- ……







### 前端模块化的了解

#### 什么是模块化

- 将一个复杂的程序依据一定的规则(规范)封装成几个块(文件), 并进行组合在一起
- 块的内部数据与实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信

#### 模块化的好处

- 避免命名冲突(减少命名空间污染)
- 更好的分离, 按需加载
- 更高复用性
- 高可维护性



我们需要重点掌握的是**ES6**和**CommonJS**，AMD与CMD只需了解，现在我们实际开发中已经基本不会用到了。

#### commonjs

在的前端开发中我们经常会用到node，node中的模块化就需要使用commonjs，所以掌握commonjs是必须的。

> 通过module.exports导出模块

```js
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;
 
//同时导出多个
module.exports = {
  x,
  addX
}
```

> 通过require导入模块

```js
var example = require('./example.js');
 
console.log(example.x); // 5
console.log(example.addX(1)); // 6
```



#### **ES6模块化**

ES6推出了自己的模块化规范，使用export和import来进行导出和导入。

```js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;
 
export {firstName, lastName, year};
```

```js
import {firstName, lastName, year} from './profile.js';
```





### 有哪些常见的Loader?他们是解决什么问题的？

* **file-loader**：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
* **url-loader**：和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去
* **css-loader**：加载 CSS，支持模块化、压缩、文件导入等特性
* **sass-loader**
* **style-loader**：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
* **image-loader**：加载并且压缩图片文件
* **babel-loader**：把 ES6 转换成 ES5
* **eslint-loader**：通过 ESLint 检查 JavaScript 代码





### 有哪些常见的Plugin？他们是解决什么问题的？

* **html-webpack-plugin**：简单创建HTML文件，用于服务器访问
* **define-plugin**：定义环境变量
* **commons-chunk-plugin**：提取公共代码
* **uglifyjs-webpack-plugin**：通过`UglifyES`压缩`ES6`代码





### Loader和Plugin的不同？

loader译为加载器，主要用于加载资源文件，webpack默认只支持加载js文件，使用loader可以实现css,less等文件的资源转化 

plugin主要用于拓展webpack的功能，例如打包压缩，定义环境变量等功能





**不同的作用**

- **Loader**直译为"加载器"。Webpack将一切文件视为模块，但是webpack原生是只能解析js文件，如果想将其他文件也打包的话，就会用到`loader`。 所以Loader的作用是**让webpack拥有了加载和解析*非JavaScript文件*的能力**。
- **Plugin**直译为"插件"。Plugin可以**扩展webpack的功能**，让webpack具有更多的灵活性。 在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。

**不同的用法**

- **Loader**在`module.rules`中配置，也就是说他作为模块的解析规则而存在。 类型为数组，每一项都是一个`Object`，里面描述了对于什么类型的文件（`test`），使用什么加载(`loader`)和使用的参数（`options`）
- **Plugin**在`plugins`中单独配置。 类型为数组，每一项是一个`plugin`的实例，参数都通过构造函数传入。





