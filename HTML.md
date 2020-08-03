## HTML

### 你是如何理解HTML语义化的？⭐

总结：用恰当的标签来标记内容。

比如段落就写 p 标签，标题就写 h1 标签，文章就写article标签，视频就写video标签，等等。

优点：

1.让人更容易读懂（增加代码可读性）

2.让搜索引擎更容易读懂（SEO(搜索引擎优化） 



### Doctype

Doctype声明于文档最前面，告诉浏览器以何种方式来渲染页面，这里有两种模式，严格模式和混杂模式。 严格模式的排版和JS运作模式是 以该浏览器支持的最高标准运行。  混杂模式，向后兼容，模拟老式浏览器，防止浏览器无法兼容页面。



### meta标签

 `<meta>` 元素可提供有关页面的元信息（meta-information），比如页面的描述和关键词，利于搜索引擎检索。

```
<meta name=”description” content=”不超过150个字符”/>       页面描述
 <meta name=”keywords” content=””/>      页面关键词者
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

·常见块级元素有：html、body、div、header、footer、nav、section、aside、article、p、hr、h1~h6、ul、ol、dl、form、table、tbody、thead、tfoot、tr等；

·常见行内元素有：span、a、img、textarea、button、input、br、label、select、canvas、progress、cite、code、strong、em、audio、video等

**而他们明显的区别是：**

**块级元素**：会自动换行，在横向充满其父元素的内容区域，默认独占一行的，可修改宽高；

**行内元素**：不会自动换行，行内元素左右可以有其他元素，行内元素的宽高大多是auto*auto。；

**注意**：行内元素设置宽高无效（但是行内置换元素可以设置宽高，下面有详细解释）、设置上下margin无效，设置上下padding类似无效（不影响文档流排列）



**另外一种分类方式：可替换元素和不可替换元素的分类**

**替换元素**：替换元素根据其标签和属性来决定元素的具体显示内容，<img><input><textarea>等。替换一般有内在尺寸如img默认的src属性引用的图片的宽高，表单元素如input也有默认的尺寸。img和input的宽高可以设定。

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





### 如何进行响应式开发

- 移动端优先。由于移动端页面限制条件比较多，如视口面积小、网速慢、考虑 touch 事件等等因素，从移动端页面扩展到 PC 端页面要更容易一些
- 使用媒体查询根据不同的视口宽度调整样式  @media 
- 使用流式布局来保证布局会随着视口宽度的改变进行调整
- 调整 meta viewport，避免浏览器使用虚拟 viewport