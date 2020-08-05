## HTML

### 你是如何理解HTML语义化的？⭐

总结：用恰当的标签来标记内容。

比如段落就写 p 标签，标题就写 h1 标签，文章就写article标签，视频就写video标签，等等。

优点：

1.让人更容易读懂（增加代码可读性）

2.让搜索引擎更容易读懂（SEO(搜索引擎优化） 



### Doctype

Doctype声明于文档最前面，告诉浏览器以何种方式来解析文档，这里有两种模式，**标准模式**和**兼容模式**。

在标准模式下，浏览器的解析规则都是按照最新的标准进行解析的。而在兼容模式下，浏览器会以向后兼容的方式来模拟老式浏览器的行为，以保证一些老的网站的正确访问。



### meta标签

 `<meta>` 元素可提供有关页面的元信息（meta-information），比如页面的描述和关键词，利于搜索引擎检索。

```
页面描述
<meta name=”description” content=”不超过150个字符”/> 
页面关键词者
<meta name=”keywords” content=””/>     
网页作者
<meta name=”author” content=”name, email@gmail.com”/>    
```

**meta viewport 是做什么用的，怎么写？**

viewport 是对移动网页的优化

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1">
```

width：控制 viewport 的大小,如 device-width 为设备的宽度

maximum-scale=1,minimum-scale=1,即不允许用户缩放



### 行内元素和块级元素的区别

补充问：为什么图片能设置宽高

·常见块级元素有：`html、body、div、header、footer、nav、section、aside、article、p、hr、h1~h6、ul、ol、dl、form、table、tbody、thead、tfoot、tr`等。

·常见行内元素有：`span、a、img、textarea、button、input、br、label、select、canvas、progress、cite、code、strong、em、audio、video`等。

**而他们明显的区别是：**

**块级元素**：会自动换行，在横向充满其父元素的内容区域，默认独占一行的，可修改宽高。

**行内元素**：不会自动换行，行内元素左右可以有其他元素，行内元素的宽高大多是`auto*auto`。

**注意**：行内元素设置宽高无效（但是行内置换元素可以设置宽高，下面有详细解释）、设置上下margin无效，设置上下padding类似无效（不影响文档流排列）



**另外一种分类方式：可替换元素和不可替换元素的分类**

**替换元素**：替换元素根据其标签和属性来决定元素的具体显示内容，`<img><input><textarea>`等。替换一般有内在尺寸如img默认的src属性引用的图片的宽高，表单元素如input也有默认的尺寸。img和input的宽高可以设定。

**不可替换元素**：即将内容直接表现给用户端。

**注意**：几乎大部分的替换元素都是行内元素，所以说如input、img、textarea是行内元素但是是可以设置宽高的说法。







### 你用过哪些 HTML 5 标签？

header  网站标志、主导航、搜索框、全站链接

nav   导航

main 页面主要内容

section 具有相似主题的一组内容

aside  侧栏，友链，广告

article  包含像报纸一样的内容，表示文档、页面 或一个独立的容器

footer 页脚

其他像pre预格式化文本，strong，em标记重点内容

特别的：video标签

属性有：autoplay/preload:自动播放/预加载，controls控制条，muted静音



### `<img>`的`title`和`alt`有什么区别

1. `title`是[全局属性，用于为元素提供附加的 提示信息。通常当鼠标滑动到元素上的时候显示。
2. `alt`是`<img>`的特有属性，是图片内容的等价描述，用于图片无法加载时显示。可提图片高可访问性，除了纯装饰图片外都必须设置有意义的值，搜索引擎会重点分析。



### script标签的async 和 defer 的作用是什么？有什么区别？

* 脚本没有 defer 或 async，浏览器会立即加载并执行指定的脚本，也就是说不等待后续载入的文档元素，读到就加载并执
  行。

* defer 属性表示延迟执行引入的 JavaScript，即这段 JavaScript 加载时 HTML 并未停止解析，这两个过程是并行的。
  当整个 document 解析完毕后再执行脚本文件，在 DOMContentLoaded 事件触发之前完成。多个脚本按顺序执行。

* async 属性表示异步执行引入的 JavaScript，与 defer 的区别在于，如果已经加载好，就会开始执行，也就是说它的执
  行仍然会阻塞文档的解析，只是它的加载过程不会阻塞。多个脚本的执行顺序无法保证。



### 如何进行响应式开发

- 移动端优先。由于移动端页面限制条件比较多，如视口面积小、网速慢、考虑 touch 事件等等因素，从移动端页面扩展到 PC 端页面要更容易一些
- 使用媒体查询根据不同的视口宽度调整样式  @media 
- 使用流式布局来保证布局会随着视口宽度的改变进行调整
- 调整 meta viewport，避免浏览器使用虚拟 viewport



