# 一、客户端与服务器

### 1.1上网的目的

通过互联网的形式来获取和消费资源



### 1.2服务器

上网的过程中，负责存放和对外提供资源的电脑，叫做服务器



### 1.3客户端

上网的过程中，负责获取和消费资源的电脑，叫做客户端





# 二、URL地址

### 2.1概念

`URL`（`UniformResourceLoader`），统一资源定位符，用于表示互联网上每个资源的唯一存放位置。浏览器只有通过`URL`地址，才能正确定位资源的位置，从而成功访问到对应的资源。

常见的`URL`举例阿巴巴



### 2.2URL地址的组成部分

URL地址由三部分组成

- 客户端和服务器之间的**通信协议**
- 存有该资源的**服务器名称**
- 资源在服务器上的具体的**存放位置**





# 三、网页打开过程

### 3.1客户端服务器通信过程

客户端和服务器的通信过程

客户端：

1. 打开浏览器
2. 输入要访问的网站地址
3. 回车，向服务器发送资源请求

服务端：

1. 服务器接收到客户端发来的资源请求
2. 服务器在内部处理这次请求，找到相关资源
3. 服务器把找到的资源，响应（发送）给客户端

注意：

- 客户端与服务器之间的通信过程，分为请求-处理-响应三个步骤
- 网页中的每一个资源，都是通过请求-处理-响应的方式从服务器获取回来的



### 3.2浏览器的开发者工具

开发者工具—Network—Doc—点击请求页签





# 四、服务端资源

### 4.1列举网页中常见的资源

- 文字内容
- image图片
- audio音频
- video视频



### 4.2数据也是资源

- 股票数据
- 各行业的排行榜



### 4.3数据是网页的灵魂

- HTML结构
- CSS表现
- JavaScript行为
- **数据是网页的灵魂**



### 4.4网页中如何请求数据

数据也是服务器对外提供的一种资源

只要是资源，必然要通过请求-处理-响应的方式从服务器获取

如果要在网页中请求服务器上的数据资源，则需要用到`XMLHttpRequest`对象

`XMLHttpRequest`（简称`xhr`）是浏览器提供的`js`成员，通过`xhr`可以请求服务器上的数据资源

```js
var xhrObj = new XMLHttpRequest()
```



### 4.5资源的请求方式

客户端请求服务器时，请求的方式有很多种，常见为`get`和`post`请求

`get`请求常用于获取服务器资源

`post`请求常用于向服务器提交数据
