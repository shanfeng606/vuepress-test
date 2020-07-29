## HTML

### 你是如何理解HTML语义化的？

总结：用恰当的标签来标记内容。

比如段落段落就写 p 标签，标题就写 h1 标签，文章就写article标签，视频就写video标签，等等。

优点：

1.让人更容易读懂（增加代码可读性）

2.让搜索引擎更容易读懂（SEO(搜索引擎优化）


### Doctype

Doctype声明于文档最前面，告诉浏览器以何种方式来渲染页面，这里有两种模式，严格模式和混杂模式。 
严格模式的排版和JS运作模式是 以该浏览器支持的最高标准运行。  
混杂模式，向后兼容，模拟老式浏览器，防止浏览器无法兼容页面。

### meta标签

 `<meta>` 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
**meta viewport 是做什么用的，怎么写？**

viewport 是对移动网页的优化

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1">
```

width：控制 viewport 的大小,如 device-width 为设备的宽度

maximum-scale=1,minimum-scale=1,即不允许用户缩放



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