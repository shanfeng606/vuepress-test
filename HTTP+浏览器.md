## HTTP/浏览器

### 浏览器内核及其作用

**浏览器内核就是负责读取网页内容，整理讯息，计算网页的显示方式并显示页面.**

| 浏览器  | 内核           | 备注                                                         |
| ------- | -------------- | ------------------------------------------------------------ |
| IE      | Trident        | IE、猎豹安全、360极速浏览器、百度浏览器                      |
| firefox | Gecko          | 可惜这几年已经没落了，打开速度慢、升级频繁、猪一样的队友flash、神一样的对手chrome。 |
| Safari  | webkit         | 从Safari推出之时起，它的渲染引擎就是Webkit，一提到 webkit，首先想到的便是 chrome，可以说，chrome 将 Webkit内核 深入人心，殊不知，Webkit 的鼻祖其实是 Safari。 |
| chrome  | Chromium/Blink | 在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。Blink 其实是 WebKit 的分支。大部分国产浏览器最新版都采用Blink内核。二次开发 |
| Opera   | blink          | 现在跟随chrome用blink内核。                                  |

### 你是怎么理解HTTP协议的

HTTP（HyperText Transfer Protocol）协议是**基于TCP的应用层协议**，它不关心数据传输的细节，主要是用来规定客户端和服务端的数据传输格式，最初是用来向客户端传输HTML页面的内容。默认端口是80。

> 特点：

**1.HTTP协议是无状态的**

就是说每次HTTP请求都是独立的，任何两个请求之间没有什么必然的联系。但是在实际应用当中并不是完全这样的，引入了Cookie和Session机制来关联请求。

**2.多次HTTP请求**

在客户端请求网页时多数情况下并不是一次请求就能成功的，服务端首先是响应HTML页面，然后浏览器收到响应之后发现HTML页面还引用了其他的资源，例如，CSS，JS文件，图片等等，还会自动发送HTTP请求这些需要的资源。现在的HTTP版本支持管道机制，可以同时请求和响应多个请求，大大提高了效率。

**3.基于TCP协议**

HTTP协议目的是规定客户端和服务端数据传输的格式和数据交互行为，并不负责数据传输的细节。底层是基于TCP实现的。现在使用的版本当中是默认持长连接的，也就是多次HTTP请求使用一个TCP连接。



### HTTP请求的内容

**请求行+请求头部+请求数据+空行**

> 请求行   

请求的第一行是：方法、URL、HTTP协议版本    例如：GET /index.html HTTP/1.1

> 请求头(key value形式)  

```
User-Agent：产生请求的浏览器类型。
Accept：客户端可识别的内容类型列表。
Host：主机地址
```

> 请求数据

请求正文中可以包含用户提交的查询信息，在post方法中，将数据以key value形式发送请求

> 空行

发送回车符和换行符，通知服务器以下不再有请求头



### HTTP响应的内容

**响应消息行+响应消息头+响应消息正文**

> 响应消息行

包含协议/版本，响应状态码，对响应状态码的描述

> 响应消息头

服务器与客户端通信的暗码，告诉客户端该怎么执行某些操作

> 响应消息正文

和网页右键“查看源码”看到的内容一样

**HTTP中确定报文结束的方法**:

* **关闭TCP连接**  

* **通过`Content-Length`检测**



### HTTP 状态码知道哪些？分别什么意思？

2XX 成功

* 200 OK
* 204 No Content
* 206 Partial Content 

3XX 重定向

* 301 永久重定向
* 302 临时重定向
* 304 资源未修改

4XX 客户端错误

* 400 请求报文中有语法错误
* 401 请求未经授权
* 403 服务器拒绝访问
* 404 资源未找到
* 405 不允许的方法
* 408 请求超时

5XX 服务器错误

* 500 仅仅告诉你服务器出错了，出了啥错咱也不知道
* 502 错误网关，无效响应
* 503 服务器忙碌无法响应
* 504 网关超时



### HTTP请求方法

GET：获取资源

POST：传输实体文本

HEAD：获得报文首部

PUT：传输文件

DELETE：删除文件

OPTIONS：询问支持的方法

TRACE：追踪路径

CONNECT：要求用隧道协议连接代理



### HTTPS与HTTP的一些区别

- HTTPS协议需要到CA申请证书，一般免费证书很少，需要交费。
- HTTPS相对于HTTP加入了ssl层，所有传输的内容都经过加密的，安全但是耗时多。
- HTTP和HTTPS使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。

**CA   SSL    端口**



### HTTP2.0的特性

* **内容安全**：http2.0是基于https的

* **二进制格式**：http1.X的解析是基于文本的，http2.0将所有的传输信息分割为更小的消息和帧，并对他们**采用二进制格式编码**
* **多路复用**——只需一个连接即可实现并行（**请求管道化，防止队头阻塞，多个请求合并到一个TCP**）  
* **首部压缩**——使用**首部表**来跟踪和存储之前发送的键值对。对于相同的数据，不再重新通过每次请求和响应发送。每个新的首部键值对要么追加到当前表的末尾，要么替换表中之前的值。



**补充**：HTTP2 主要解决的问题也是 TCP连接复用。但它比 keep-alive 更彻底，类似于通信工程里的时分复用，多个请求可以同时发送（不分先后），同时响应，解决了 队头阻塞（HOL blocking）的问题，极大提高效率。

keep-alive 的 HTTP pipelining 相当于单线程的，而 HTTP2 相当于并发。]

**http如何控制请求的数量**：同一时间针对同一域名下的请求有一定数量限制。超过限制数目的请求会被阻塞



### **HTTP1.0与1.1区别**

* **长连接**  HTTP 1.0需要使用keep-alive参数来告知服务器端要建立一个长连接，而HTTP1.1默认支持长连接。

* **节约带宽** HTTP 1.1支持只发送header信息(不带任何body信息)
* **HOST域**  HTTP1.0是没有host域的，HTTP1.1才支持这个参数。





### 什么是拥塞控制

**拥塞控制，就是在网络中发生拥塞时，减少向网络中发送数据的速度，防止造成恶性循环；同时在网络空闲时，提高发送数据的速度，最大限度地利用网络资源**。

说的简单点，就和堵车差不多，路就这么宽，来的车多了，自然过的就慢，所以在必要的时候要限号。

https://www.cnblogs.com/tuyang1129/p/12439862.html





### TCP建立连接的三次握手过程⭐ 

[https://www.zhihu.com/search?type=content&q=%E4%B8%89%E6%AC%A1%E6%8F%A1%E6%89%8B%204%E6%AC%A1%E6%8C%A5%E6%89%8B](https://www.zhihu.com/search?type=content&q=三次握手 4次挥手)

**三次握手**：

- 首先服务器端处于LISTEN状态。 
- 当客户端想要建立连接时，他将发送一个SYN包，序列号假如为x。客户端进入SYN_SENT状态。 
- 当服务器端收到了这个SYN包，如果服务器同意建立连接，他将发送一个SYN，ACK包，序列号假如为y，确认号为x+1。服务器端进入SYN_RECD状态。 
- 当客户端收到了服务器端的SYN,ACK包，它将再次确认，向服务器发送一个ACK包，序列号为x+1，确认号为y+1。此时客户端进入ESTABLISHED状态。 
- 当服务器端收到了客户端的ACK包，也将进入ESTABLISHED状态。

**Q:为什么不能是2次握手**

- 为了实现可靠数据传输， TCP 协议的通信双方， 都必须维护一个序列号， 以标识发送出去的数据包中， 哪些是已经被对方收到的。 三次握手的过程即是通信双方相互告知序列号起始值， 并确认对方已经收到了序列号起始值的必经步骤
- 如果只是两次握手， 至多只有连接发起方的起始序列号能被确认， 另一方选择的序列号则得不到确认



### 断开链接四次挥手⭐ 

刚开始双方都处于 establised 状态，假如是客户端先发起关闭请求，则：

* **第一次挥手**：客户端发送一个 FIN 报文，报文中会指定一个序列号x。此时客户端处于**FIN_WAIT1**(终止等待1)状态。

* **第二次挥手**：服务端收到 FIN 之后，会发送 ACK 报文，且把x+ 1 作为 ACK 报文的序列号值，表明已经收到客户端的报文了，此时服务端处于 **CLOSE_WAIT**状态。

* **第三次挥手**：如果服务端也想断开连接了，和客户端的第一次挥手一样，发给 FIN 报文，且指定一个序列号y。此时服务端处于 **LAST_ACK** 的状态。

* **第四次挥手**：客户端收到 FIN 之后，一样发送一个 ACK 报文作为应答，且把服务端的序列号值 y+ 1 作为自己 ACK 报文的序列号值，此时客户端处于 **TIME_WAIT** 状态。需要过一阵子以确保服务端收到自己的 ACK 报文之后才会进入**CLOSED** 状态

* 服务端收到 ACK 报文之后，就处于关闭连接了，处于 **CLOSED** 状态。



### SSL/TLS 握手过程（HTTPS通信过程）

阮一峰的例子：

客户端：爱丽丝   、  服务端：鲍勃

* 第一步，爱丽丝给出协议版本号、一个客户端生成的随机数（Client random），以及客户端支持的加密方法。

* 第二步，鲍勃确认双方使用的加密方法，并给出数字证书、以及一个服务器生成的随机数（Server random）。

* 第三步，爱丽丝确认数字证书有效，然后生成一个新的随机数（Premaster secret），并使用数字证书中的公钥，加密这个随机数，发给鲍勃。

* 第四步，鲍勃使用自己的私钥，获取爱丽丝发来的随机数（即Premaster secret）。

* 第五步，爱丽丝和鲍勃根据约定的加密方法，使用前面的三个随机数，生成"对话密钥"（session key），用来加密接下来的整个对话过程。



### GET 和 POST 的区别

语义上的区别，get用于获取数据，post用于提交数据。

* Post多用于副作用（对服务器的资源进行改变），Get多用于无副作用

* Post 相对 Get 安全一点点，因为GET请求的数据会附在URL之后，以?分割URL和传输数据，参数之间以&相连，

  POST把提交的数据则放置在是HTTP包的包体中。post易于防止CSRF。  

* GET的长度受限于url的长度，而url的长度限制是特定的浏览器和服务器设置的，理论上GET的长度可以无限长。

* Post 支持更多的编码类型且不对数据类型限制，GET 只能进行 URL 编码，只能接收 ASCII 字符

* 私密性的信息请求使用post，查询信息和可以想要通过url分享的信息使用get。

**副作用   参数位置  长度  编码类型**





### 跨域及解决办法

浏览器遵循**同源政策**（scheme(协议)、host(主机)和port(端口)都相同则为同源）

当浏览器向目标 `URI `发` Ajax` 请求时，只要当前 `URL` 和目标 `URL` 不同源，则产生跨域，被称为**跨域请求**。

**目的** 主要是用来防止 CSRF 攻击的。简单点说，CSRF 攻击是利用用户的登录态发起恶意请求。
采用同源策略主要是因为安全。若非同源下的cookie等隐私数据可以被随意获取，非同源下的DOM可以的随意操作，ajax可以任意请求的话，用户的各种隐私势必泄露。


#### **解决**

> 如果是像解决 ajax 无法提交跨域请求的问题，我们可以使用 jsonp、cors、websocket 协议、服务器代理来解决问题。

1. **JSONP** ，允许 script 加载第三方资源    只支持get。JSONP 本质不是 Ajax 请求，是 script 标签请求。JSONP 请求本质上是利用了 “Ajax请求会受到同源策略限制，而 script 标签请求不会” 这一点来绕过同源策略。
2. **CORS** 前后端协作设置请求头部，Access-Control-Allow-Origin 等头部信息
3. **反向代理**（nginx 服务内部配置 Access-Control-Allow-Origin ）
4. 使用 **websocket 协议**，这个协议没有同源限制。

> 如果只是想要实现主域名下的不同子域名的跨域操作，我们可以使用设置 document.domain 来解决。
>
> 比如a.test.com和b.test.com   只需要给页面添加document.domain='test.com'表示二级域名都相等就可以实现跨域

1. document.domain + iframe跨域
2. location.hash
3. window.name + iframe跨域
4. postMessage 跨域



### JSONP的工作原理

JSONP

1. JSONP是通过 script 标签加载数据，获取的数据当做 JS 代码来执行，利用标签没有同源策略的限制（算是一个漏洞），来达到与第三方通信，从而实现跨域。只支持get

2. 提前在页面上声明一个函数，函数名通过接口传参的方式传给后台，后台解析到函数名后在原始数据上「包裹」这个函数名，发送给前端。换句话说，JSONP 需要对应接口的后端的配合才能实现。

```js
<script>
	//jsonp回调方法，一定要写在jsonp请求前面
	function testjson(txt){
		alert(txt);
	}
</script>
<script src ="/demo/testJsonp.shtml?callback=testjson" type="text/javascript" ></script>
```



### CORS(跨域资源共享)

**CORS 全称是跨域资源共享（Cross-Origin Resource Sharing），是一种 AJAX 跨域请求资源的方式。**
 CORS与JSONP的使用目的相同，但是比JSONP更强大。JSONP只支持GET请求，CORS**支持所有类型的HTTP请求**。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。

CORS 需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，因此我们只需要在服务器端配置就行。浏览器将 CORS 请求分成两类：简单请求和非简单请求。

**对于简单请求**，浏览器直接发出 CORS 请求。具体来说，就是会在**头信息之中，增加一个 Origin 字段**。Origin 字段用来说明本次请求来自哪个源。服务器根据这个值，决定是否同意这次请求。对于如果 Origin 指定的源，不在许可范围内，服务器会返回一个正常的 HTTP 回应。浏览器发现，这个回应的头信息没有包含 Access-Control-Allow-Origin 字段，就知道出错了，从而抛出一个错误，ajax 不会收到响应信息。如果成功的话会包含一些以 Access-Control- 开头的字段。

**非简单请求**，浏览器会先发出一次预检请求，来判断该域名是否在服务器的白名单中，如果收到肯定回复后才会发起请求。



浏览器将CORS请求分成两类：**简单请求**和**非简单请求**

只要同时满足以下两大条件，就属于简单请求

- 请求方法是以下三种方法之一：

```
HEAD
GET
POST
```

- HTTP的头信息不超出以下几种字段：

```
Accept
Accept-Language
Content-Language
Last-Event-ID
Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/plain
```

不同时满足上面两个条件，就属于非简单请求。



### CORS和JSONP的区别

* JSONP只能实现GET请求，而CORS支持所有类型的HTTP请求。   
* 使用CORS，开发者可以使用普通的XMLHttpRequest发起请求和获得数据，比起JSONP有更好的错误处理。
* JSONP主要被老的浏览器支持，它们往往不支持CORS，而绝大多数现代浏览器都已经支持了CORS 





### cookie、localStorage、sessionStorage区别与用法

| 特性         | **cookie**                                 | **localStorage**         | **sessionStorage** | **indexDB**              |
| ------------ | ------------------------------------------ | ------------------------ | ------------------ | ------------------------ |
| 数据生命周期 | 一般由服务器生成，可以设置过期时间         | 除非被清理，否则一直存在 | 页面关闭就清理     | 除非被清理，否则一直存在 |
| 数据存储大小 | 4K                                         | 5M                       | 5M                 | 无限                     |
| 与服务端通信 | 每次都会携带在 header 中，对于请求性能影响 | 不参与                   | 不参与             | 不参与                   |

localStorage 和 sessionStorage 都具有相同的操作方法，例如 `setItem()`、`getItem()` 和 `removeItem()` 等

```
//添加修改数据
sessionStorage.setItem('key', 'value');
localStorage.setItem('key', 'value');
```

```
//获取数据
sessionStorage.getItem('key');
localStorage.getItem('key');
```

```
//移除数据
sessionStorage.removeItem('key');
localStorage.removeItem('key');
```

```
//全部清除
sessionStorage.clear();
localStorage.clear();
```

cookie

```
//储存数据
window.document.cookie = 'xxx';
//取出数据
document.cookie
```



### **说一下cookie的内容有哪些**

```js
"key=name; expires=Thu, 25 Feb 2016 04:18:00 GMT; domain=ppsc.sankuai.com; path=/; secure; HttpOnly"
```

**expires**

`expires`选项用来设置“cookie 什么时间内有效”。

`expires` 是 http/1.0协议中的选项，在新的http/1.1协议中`expires`已经由 `max-age` 选项代替，两者的作用都是限制cookie 的有效时间。

**domain 和 path**

`domain`是域名，`path`是路径，两者加起来就构成了 URL，`domain`和`path`一起来限制 cookie 能被哪些 URL 访问。

通过设置domain来实现cookie跨子域的问题

```js
cookie.setDomain("test.com"); 
```

**secure**

`secure`选项用来设置`cookie`只在确保安全的请求中才会发送。当请求是`HTTPS`或者其他安全协议时，包含 `secure` 选项的 `cookie`才能被发送至服务器。

**httpOnly**

这个选项用来设置`cookie`是否能通过 `js` 去访问。如果您在cookie中设置了HttpOnly属性，那么通过js脚本将无法读取到cookie信息，这样能有效的防止XSS攻击



通俗地说，就是当一个用户通过 HTTP 协议访问一个服务器的时候，这个服务器会将一些 Key/Value 键值对返回给客户端浏览器，并给这些数据加上一些限制条件，在条件符合时这个用户下次访问这个服务器的时候，数据又被完整地带回给服务器。


### Cookie跨域设置

网页端中，对于跨域的 `XMLHttpRequest` 请求，需要设置`withCredentials` 属性为 true。

同时服务端的响应中必须携带 `Access-Control-Allow-Credentials: true` 首部。如果服务端的响应中未携带`Access-Control-Allow-Credentials: true` 首部，浏览器将不会把响应的内容返回给发送者。



JSONP

nginx反向代理


### cookie的弊端

* cookie 有大小限制、每条cookie不能超过4kb
* cookies存在安全性问题、有可能被篡改
* 有些数据不能存在客户端、例如表单不能重复提交
* cookie每次发送数据都会发送给服务端、造成不必要的浪费





### **Web storage和cookie的区别**

**----存储大小，服务器交互，方法属性**

1、Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用。
2、除此之外，Web Storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie。
3、但是cookie也是不可以或缺的：cookie的作用是与服务器进行交互，作为HTTP规范的一部分而存在 ，而Web Storage仅仅是为了在本地“存储”数据而生。



### Cookie和Session的区别

1、cookie数据存放在客户的浏览器上，session数据放在服务器上(可以理解为存在服务器上的缓存)。

2、cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session。

3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie。

4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

5、可以考虑将登陆信息等重要信息存放为session，其他信息如果需要保留，可以放在cookie中。

**存放位置，安全，存储大小**

**token认证机制**

token与session的不同主要在①认证成功后，会对当前用户数据进行加密，**生成一个加密字符串token**，返还给客户端（服务器端并不进行保存）

②浏览器会将接收到的token值存储在Local Storage中，（通过js代码写入Local Storage，通过js获取，并不会像cookie一样自动携带）

③再次访问时服务器端对token值的处理：**服务器对浏览器传来的token值进行解密**，解密完成后进行用户数据的查询，如果查询成功，则通过认证，实现状态保持，所以，即时有了多台服务器，服务器也只是做了token的解密和用户数据的查询，它不需要在服务端去保留用户的认证信息或者会话信息，这就意味着基于token认证机制的应用不需要去考虑用户在哪一台服务器登录了，这就为应用的扩展提供了便利，解决了session扩展性的弊端。

**session与token**

方案 A ：我发给你一张身份证，但只是一张写着身份证号码的纸片。你每次来办事，我去后台查一下你的 id 是不是有效。 
方案 B ：我发给你一张加密的身份证，以后你只要出示这张卡片，我就知道你一定是自己人。 
就这么个差别。





### 从输入url到渲染出页面的整个过程⭐ 

DNS域名解析（先查找缓存） –> 发起TCP的3次握手 –> 建立TCP连接后发起http请求 –> 服务器响应http请求，浏览器得到html代码 –> 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等） –> 浏览器对页面进行渲染呈现给用户

**加载过程**

* `DNS`解析：域名 --> IP地址   (递归查询：从根域名服务器到顶级域名服务器再到极限域名服务器依次搜索哦对应目标域名的IP)

* 浏览器根据IP地址向服务器发起`http`请求   (浏览器与服务器建立tcp连接（三次握手）)

* 服务器处理`http`请求，并返回给浏览器

**渲染过程**

* 浏览器解析接收到 `HTML` 文件并转换为 `DOM` 树，确定节点的父子以及兄弟关系。（HTML-Token-DOM树）
* 将 `CSS` 文件转换为 `CSSOM` 树，确定css属性之间的级联关系。
* 生成 `DOM` 树和 `CSSOM` 树以后，就需要将这两棵树组合为渲染树，根据渲染树来进行布局，然后调用 `GPU` 绘制，合成图层，显示在屏幕上。
* 遇到`<script>`则暂停渲染，优先加载并执行JS代码，完成再继续，直至把`Render Tree`渲染完成





### HTML页面的加载顺序

```html
<html>
    <head>
        <!-- 引用外部JS文件 -->
        <script src="..........."></script>
        <!--引用外部css样式 -->
        <link href="............."/>
        <style>
               ..............
        </style>
        <script>
               ..............
        </script>
    </head>
    <body>
        <script>
               ..............
        </script>
    </body>
</html>
```

从上到下运行，先解析head标签中的代码，

（1) head标签中会包含一些引用外部文件的代码，从开始运行就会下载这些被引用的外部文件（css并行加载）

​     当**遇到script标签**的时候，加载并执行JS代码


（2）当head中代码解析完毕，会开始解析body中的代码

​     如果此时head中引用的外部文件没有下载完，将会继续下载

​     浏览器解析body代码中的元素，会按照head中声明一部分样式去解析

​     如果此时遇到body标签中的`<script>`，同样会将控制权交给JavaScript引擎来解析JavaScript

​     解析完毕后将控制权交还给浏览器渲染引擎。

​     **当body中的代码全部执行完毕、并且整个页面的css样式加载完毕后，css会重新渲染整个页面的html元素。**

（3）按照之前的描述，**`<script>`写到body标签内靠后比较好，**

​     因为JavaScript 会操作html元素， 如果在body加载完之前写JavaScript 会造成JavaScript 找不到页面元素

​     但是我们经常将`<script>`写到head中，body中不会有大量的js代码，body中的html代码结构会比较清晰

​     window.onload： 等待页面中的所有内容加载完毕之后才会执行

​     $(document).ready()： 页面中所有DOM结构绘制完毕之后就能够执行

​     可以这样理解：window.onload 和 $(document).ready()/$(function(){}); 相当于  写在body 内  最靠后的`<script> `代码段







### DNS域名解析的过程

解析流程就是**分级查询**

以[www.163.com]为例:

- 客户端打开浏览器，输入一个域名。比如输入[www.163.com]，这时，客户端会发出一个DNS请求到**DNS本地服务器**。本地DNS服务器一般都是你的网络接入服务器商提供，比如中国电信，中国移动。
- 查询[www.163.com]的DNS请求到达本地DNS服务器之后，本地DNS服务器会首先查询它的缓存记录，如果缓存中有此条记录，就可以直接返回结果。如果没有，本地DNS服务器还要向**DNS根服务器**进行查询。
- 根DNS服务器没有记录具体的域名和IP地址的对应关系，而是告诉本地DNS服务器，你可以到**域服务器**上去继续查询，并给出域服务器的地址。
- 本地DNS服务器继续向域服务器发出请求，在这个例子中，请求的对象是.com域服务器。.com域服务器收到请求之后，也不会直接返回域名和IP地址的对应关系，而是**告诉本地DNS服务器，你的域名的解析服务器的地址**。
- 最后，本地DNS服务器向**域名的解析服务器**发出请求，这时就能收到一个域名和IP地址对应关系，本地DNS服务器不仅要把IP地址返回给用户电脑，还要把这个对应关系保存在缓存中，以备下次别的用户查询时，可以直接返回结果，加快网络访问。






### 浏览器缓存的读取规则⭐ 

它们的**优先级**是：(由上到下寻找，找到即返回；找不到则继续)

1. Service Worker   运行在 JavaScript 主线程之外，虽然由于脱离了浏览器窗体无法直接访问 DOM，但是它可以完成离线缓存、消息推送、网络代理等功能。
2. Memory Cache（内存中的缓存）
3. Disk Cache（硬盘中的缓存）
4. 网络请求

####  强缓存：

不会向服务器发送请求，直接从缓存中读取资源，状态码200。

强缓存可以通过设置两种 HTTP Header 实现：`Expires` 和 `Cache-Control` 。

`Expires`设置一个日期，资源会过期，但受限于本地时间

`Cache-Control：max-age=30`  资源会在30秒后过期   `no-cache`必须先与服务器确认返回的响应是否被更改

####  协商缓存：

当强制缓存失效(超过规定时间)时，就需要使用协商缓存，由服务器决定缓存内容是否失效。

流程上说，浏览器先请求缓存数据库，返回一个缓存标识。之后浏览器拿这个标识和服务器通讯。如果缓存未失效，则返回 HTTP 状态码 304 表示继续使用，于是客户端继续使用缓存；如果失效，则返回新的数据和缓存规则，浏览器响应数据后，再把规则写入到缓存数据库。

协商缓存有 2 组字段(不是两个)：

**Last-Modified & If-Modified-Since**

1. 服务器通过 `Last-Modified` 字段告知客户端，资源最后一次被修改的时间

2. 下一次请求相同资源时时，浏览器从自己的缓存中找出“不确定是否过期的”缓存。因此在请求头中将上次的 `Last-Modified` 的值写入到请求头的 `If-Modified-Since` 字段

3. 服务器会将 `If-Modified-Since` 的值与 `Last-Modified` 字段进行对比。如果相等，则表示未修改，响应 304；反之，则表示修改了，响应 200 状态码，并返回数据。

但是他还是有一定缺陷的：

- 如果资源更新的速度是秒以下单位，那么该缓存是不能被使用的，因为它的时间单位最低是秒。
- 如果文件是通过服务器动态生成的，那么该方法的更新时间永远是生成的时间，尽管文件可能没有变化，所以起不到缓存的作用。

**Etag & If-None-Match**

为了解决上述问题，出现了一组新的字段 `Etag` 和 `If-None-Match`

`Etag` 存储的是文件的特殊标识(一般都是 hash 生成的)，服务器存储着文件的 `Etag` 字段。之后的流程和 `Last-Modified` 一致，只是 `Last-Modified` 字段和它所表示的更新时间改变成了 `Etag` 字段和它所表示的文件 hash，把 `If-Modified-Since` 变成了 `If-None-Match`。服务器同样进行比较，命中返回 304, 不命中返回新资源和 200。

**Etag 的优先级高于 Last-Modified**

**LM与Etag区别**

LM根据文件修改时间来判断是否要重新返回整个文件，对应请求头 IF-M-S ，服务端和客户端进行对比，但是时间只能精确到秒，假如在这一秒之间恰好发生了变化就GG了。
E-tag则是对文件求MD5或者哈希值，绝对精确，只要有任何变化都能体现出来，这个算法貌似是server配置的


### AJAX的优缺点

优点：

* 最大的一点是**页面无刷新**，在页面内与服务器通信，给用户的体验非常好 

* 使用**异步**方式与服务器通信，不需要打断用户的操作，具有更加迅速的响应能力 

* **减轻服务器和带宽的负担** ，前端和后端负载平衡



缺点：

* AJAX干掉了Back和History功能，即对浏览器机制的破坏 

* AJAX安全问题
* 对搜索引擎支持较弱




### 使用`Ajax`解决浏览器缓存问题

我们都知道ajax能提高页面载入的速度主要的原因是通过ajax减少了重复数据的载入，也就是说在载入数据的同时将数据缓存到内存中，一旦数据被加载其中，只要我们没有刷新页面，这些数据就会一直被缓存在内存中，当我们提交 的`URL`与历史的`URL`一致时，就不需要提交给服务器，也就是不需要从服务器上面去获取数据，虽然这样降低了服务器的负载提高了用户的体验，但是我们不能获取最新的数据。为了保证我们读取的信息都是最新的，我们就需要禁止他的缓存功能。

**禁止浏览器缓存功能有如下几种方法：**

1. 在`ajax`发送请求前加上 `anyAjaxObj.setRequestHeader("If-Modified-Since","0")`。
2. 在`ajax`发送请求前加上 `anyAjaxObj.setRequestHeader("Cache-Control","no-cache")`。
3. 在`URL`后面加上一个随机数：`"fresh=" + Math.random()`;。
4. 在`URL`后面加上时间戳：`"nowtime=" + new Date().getTime()`;。
5. 如果是使用`jQuery`，直接这样就可以了`$.ajaxSetup({cache:false})`。这样页面的所有`ajax`都会执行这条语句就是不需要保存缓存记录。


### Fetch与AJAX

XMLHttpRequest 是一个设计粗糙的 API，不符合关注分离（Separation of Concerns）的原则，配置和调用方式非常混乱，而且基于事件的异步模型写起来也没有现代的 Promise，generator/yield，async/await 友好。[·](http://caibaojian.com/fetch-ajax.html)

Fetch 的出现就是为了解决 XHR 的问题

缺点：

* 有兼容问题的

- Fetch 请求默认是不带 cookie 的，需要设置 `fetch(url, {credentials: 'include'})`

- 服务器返回 400，500 错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject。




### TCP和UDP的区别(位于传输层)

- TCP 是面向连接的，UDP 是面向无连接的
- UDP程序结构较简单
- TCP 是面向字节流的，UDP 是基于数据报的
- TCP 保证数据正确性，UDP 可能丢包
- TCP 保证数据顺序，UDP 不保证

**什么是面向连接，什么是面向无连接**

在互通之前，面向连接的协议会先建立连接，如 TCP 有三次握手，而 UDP 不会

**TCP 为什么是可靠连接**

- TCP 报文头里面的序号能使 TCP 的数据按序到达

- 报文头里面的确认序号能保证不丢包，累计确认及超时重传机制

- TCP 拥有流量控制及拥塞控制的机制

  

总结：**UDP面向无连接  不可靠性  高效**



### OSI七层模型

osi七层模型可以说是面试必考基础了    **物理系有一个人叫数据链路在网络上传输了一个会话来表示应用**

从上到下分别是：

应用层：特定应用的协议（电子邮件协议，远程登录协议，文件传输协议）  HTTP HTTPS  FTP DNS SMTP

表示层：数据格式转换  

会话层：建立，解除会话

--------------------------------

传输层：建立端口到端口的通信，TCP或UDP传输数据

网络层：建立主机到主机的通信，将数据传送到目标地址   IP

数据链路层：物理层面上的通信传输 ARP协议

物理层：负责0,1比特流与电压高低，光的闪灭之间的互换



TCP/IP模型四层架构从下到上分别是链路层，网络层，传输层，应用层
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191015164008520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JveWFhYm95,size_16,color_FFFFFF,t_70)

基于TCP的应用层协议：HTTP、FTP、SMTP、TELNET、SSH

基于UDP的应用层协议：DNS、TFTP（简单文件传输协议）、SNMP：简单网络管理协议




### window.onload 和 DOMContentLoaded 的区别

DOMContentLoaded：仅当DOM加载完成，不包括样式表，图片，flash

window.onload：页面完全加载触发，样式表，脚本，图片，flash都已经加载完成了。





### 请介绍下fetch发送2次请求的原因

用fetch的post请求的时候，导致fetch第一次发送了一个Options请求，询问服务器是否支持自定义的请求头，如果服务器支持，则在第二次中发送真正的请求。





### 浏览器中的常驻线程

GUI渲染线程  (页面重绘回流时执行，当JS引擎执行时被挂起)

js引擎线程

定时触发器线程

事件触发线程

异步http请求线程



3D变换`translate3d`，`transform: translateZ(0)` 来开启硬件加速 。



### 网站的登录态是如何保持的，一个完整的登录流程是怎样实现的？

通过cookies来保持的，cookie面面存储token，每次请求到后端服务器都会带上token。从而验证用户是否登录。
输入用户、密码—>点击登录，发送到服务端—>服务端验证密码，生成token—>写入到cookies，返回成功


### CDN原理

由于用户访问源站业务有性能瓶颈，通过cdn技术**把源站的内容缓存到多个节点**。用户向源站域名发起请求时，请求会被调度至**最接近用户的服务节点**，直接由服务节点直接快速响应，有效降低用户访问延迟，提升可用性。