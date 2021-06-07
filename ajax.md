## XMLHttpRequest对象

> 浏览器内建对象，用于与服务器通信(交换数据) ， 由此我们便可实现对网页的部分更新，而不是刷新整个页面。这个请求是异步的，即在往服务器发送请求时，并不会阻碍程序的运行，浏览器会继续渲染后续的结构。

```
请求由客户端发起，其规范格式为：请求行、请求头、请求主体。 
```

<img src="02-请求规范格式.png">



### 发送get请求

XMLHttpRequest以异步的方式发送HTTP请求，因此在发送请求时，一样需要遵循HTTP协议。

> 使用XMLHttpRequest发送get请求的步骤

```javascript
//1. 创建一个XMLHttpRequest对象
var xhr = new XMLHttpRequest();

//2. 设置请求行
// 第一个参数:请求方式  get/post
// 第二个参数:请求的地址 需要在url后面拼上参数列表
// 第三个参数: 是否异步请求,默认是true  true就是异步,false是同步
xhr.open("get", "http://localhost:5000/test?name=haha");

//3. 设置请求头(get不用设置)
//请求头中可以设置Content-Type,用以说明请求主体的内容是如何编码
//get请求时没有请求体,无需设置请求头

//4. 设置请求体
//get请求的请求体为空,因为参数列表拼接到url后面了
xhr.send(null);
```

注意点 :

- get请求,设置请求行时,需要把参数列表拼接到url后面
- get请求不用设置请求头, 不用说明请求主体的编码方式
- get请求的请求体为null

### 发送post请求

```javascript
var xhr = new XMLHttpRequest();

// 1. 设置请求行 post请求的参数列表在请求体
xhr.open("post", "http://localhost:5000/test");

// 2. 设置请求头, post 请求必须要设置 content-type, 标记请求体内容的解析方式, 不然后端无法解析获取数据
xhr.setRequestHeader( "content-type", "application/x-www-form-urlencoded" );
//在请求发送过程中会对数据进行序列化处理，以键值对形式？key1=value1&key2=value2的方式发送到服务器

// 3. 设置请求体
xhr.send( "name=zs&age=18" );
```

注意点 :

- post请求, 设置请求行时, 不拼接参数列表
- post必须设置请求头中的content-type为application/x-www-form-urlencoded, 标记请求体解析方式
- post 请求需要将参数列表设置到请求体中

### 获取响应 readyState

readyState:记录了XMLHttpRequest对象的当前状态

```
readyState有五种可能的值：
xhr.readyState = 0时，UNSENT open尚未调用
xhr.readyState = 1时，OPENED open已调用
xhr.readyState = 2时，HEADERS_RECEIVED 接收到响应头信息
xhr.readyState = 3时，LOADING 接收到响应主体
xhr.readyState = 4时，DONE 响应完成

不用记忆状态，只需要了解有状态变化这个概念
```



HTTP响应分为3个部分，状态行、响应头、响应体。

```javascript
//给xhr注册一个onreadystatechange事件，当xhr的状态发生状态发生改变时，会触发这个事件。
xhr.onreadystatechange = function () {
  
  if(xhr.readyState == 4){
    
    //1. 获取状态码
    console.log("状态行:"+xhr.status);
    
    //2. 获取响应头
    console.log("所有的响应头:"+xhr.getAllResponseHeaders());
    console.log("指定响应头:"+xhr.getResponseHeader("content-type"));
    
    //3. 获取响应体
    console.log(xhr.responseText);
    
  }
  
}
```

## jQuery中的ajax方法

> jQuery为我们提供了更强大的Ajax封装

### $.ajax({})

参数列表

| 参数名称   | 描述             | 取值                | 示例                              |
| ---------- | ---------------- | ------------------- | --------------------------------- |
| url        | 接口地址         |                     | url:"02.php"                      |
| type       | 请求方式         | get/post            | type:"get"                        |
| timeout    | 超时时间         | 单位毫秒            | timeout:5000                      |
| dataType   | 服务器返回的格式 | json(默认)/xml/text | dataType:"json"                   |
| data       | 发送的请求数据   | 对象                | data:{name:"zs", age:18}          |
| beforeSend | 调用前的回调函数 | function(){}        | beforeSend:function(){ alert(1) } |
| success    | 成功的回调函数   | function (data) {}  | success:function (data) {}        |
| error      | 失败的回调函数   | function (error) {} | error:function(data) {}           |
| complete   | 完成后的回调函数 | function () {}      | complete:function () {}           |



使用示例：

```javascript
$.ajax({
  type:"get",//请求类型
  url:"",//请求地址
  data:{name:"zs", age:18},//请求数据
  dataType:"json",//希望接受的数据类型
  timeout:5000,//设置超时时间
   // 发送ajax前,会调用的函数, 
   // 如果这个函数返回 false,(注意: 必须返回false) 这次请求就不发送了
   // 一般 beforeSend 中用于表单校验
  beforeSend:function () {
    //alert("发送前调用");
      return false;
  },
  success:function (data) {
    //alert("成功时调用");
    console.log(data);
  },
  error:function (xhr) {
    //alert("失败时调用");
    console.log(xhr);
  },
    // 不管成功失败,都会调用这个函数
  complete:function () {
    //alert("请求完成时调用");
  }
});
```

### 其他api(了解)

```javascript
//$.post(url [,data][,success][,dataType]);只发送post请求
//$.get(url [,data][,success][,dataType]); 只发送get请求
```

## 同源与跨域

### 同源

#### 同源策略的基本概念

> 1995年，同源政策由 Netscape 公司引入浏览器。目前，所有浏览器都实行这个政策。
> 同源策略：最初，它的含义是指，A网页设置的 Cookie，B网页不能打开，除非这两个网页"同源"。所谓"同源"指的是"三个相同"。

```javascript
协议相同
域名相同
端口相同
```

举例来说，这个网址`http://www.example.com/dir/page.html`协议是`http://`，

域名是`www.example.com`，端口是`80`（默认端口可以省略）。它的同源情况如下。

```javascript
http://www.example.com/dir2/other.html：同源

file:///F:/phpStudy/WWW/day01/04-demo/04.html 不同源(协议不同)
http://v2.www.example.com/dir/other.html：不同源（域名不同）
http://www.example.com:81/dir/other.html：不同源（端口不同）


//来源: http://127.0.0.1:5000/index.html
// ajax地址: http://localhost:5000/test
```

#### 同源策略的目的

> 同源政策的目的，是为了保证用户信息的安全，防止恶意的网站窃取数据。

#### 同源策略的限制范围

> 随着互联网的发展，“同源策略”越来越严格，目前，如果非同源，以下三种行为都将收到限制。

```javascript
1. Cookie、LocalStorage 和 IndexDB 无法读取。
2. DOM 无法获得。
3. AJAX 请求不能发送。
```

虽然这些限制是很有必要的，但是也给我们日常开发带来不好的影响。比如实际开发过程中，往往都会把服务器端架设到一台甚至是一个集群的服务器中，把客户端页面放到另外一个单独的服务器。那么这时候就会出现不同源的情况，如果我们知道两个网站都是安全的话，我们是希望两个不同源的网站之间可以相互请求数据的。这就需要使用到**跨域** 。

### 跨域

#### 解决跨域问题

##### jsonp( 无兼容性问题 )

> JSONP(JSON with Padding)、可用于解决主流浏览器的跨域数据访问的问题。
>
> 原理：服务端返回一个定义好的js函数的调用，并且将服务器的数据以该函数参数的形式传递过来，这个方法需要前后端配合

`script` 标签是不受同源策略的限制的，它可以载入任意地方的 JavaScript 文件。类似的还有`img`和`link`标签

```html
<!--不受同源策略限制的标签-->
<img src="http://www.api.com/1.jpg" alt="">
<link rel="stylesheet" href="http://www.api.com/1.css">
<script src="http://www.api.com/1.js"></script>
```



```js
// 浏览器端:
  let btn = document.getElementById('btn')
  btn.addEventListener('click',function () {
    //1.动态生成一个script节点
    let scriptNode = document.createElement('script')
    //2.全局定义一个函数
    window.getData = function (data) {
      console.log(data)
    }
    //3.指定请求地址
    scriptNode.src = 'http://localhost:3000/test?callBack=getData'
    
    //4.添加节点
    document.body.appendChild(scriptNode)
    
  })

// 服务器端: 
app.get('/test',(req,res)=>{
    let {callBack} = req.query
    let arr = [{name:'kobe',age:12},{name:'wade',age:13}]
   // res.send(arr)
    let str = callBack+'('+JSON.stringify(arr)+')'
    //getData([{name:'kobe',age:12},{name:'wade',age:13}])
    //res.send('alert2(0)')
    res.send(str)
})
```



1. 说白了，jsonp的原理就是 借助了script标签 src 请求资源时, 不受同源策略的限制.
2. 在服务端返回一个函数的调用，将数据当前调用函数的实参。
3. 在浏览器端，需要程序要声明一个全局函数，通过形参就可以获取到服务端返回的对应的值

jsonp原理大家需要知道，面试中经常会问到，实际工作中不用纠结, 因为jquery已经帮我们封装好了，我们使用起来非常的方便。

##### jquery对于jsonp的封装

**注意: jsonp 仅支持get请求**

```javascript
//使用起来相当的简单，跟普通的get请求没有任何的区别，只需要把dataType固定成jsonp即可。
$.ajax({
  type:"get",
  url:"",
  dataType:"jsonp",
  data:{
    uname:"zs",
    upass:"123456"
  },
  success:function (info) {
    console.log(info);
  }
});
```

#### 跨域资源共享(CORS) ( 兼容性IE10+ )

##### cors的使用

> 新版本的XMLHttpRequest对象，可以向不同域名的服务器发出HTTP请求。这叫做["跨域资源共享"](http://en.wikipedia.org/wiki/Cross-Origin_Resource_Sharing)（Cross-origin resource sharing，简称CORS）。

跨域资源共享（CORS）的前提

- 浏览器支持这个功能( 兼容性IE10+ )
- 服务器必须允许这种跨域。

服务器允许跨域的代码：

```php
//允许所有的域名访问这个接口
header("Access-Control-Allow-Origin:*");
//允许www.study.com这个域名访问这个接口
header("Access-Control-Allow-Origin:http://www.study.com");
```

##### CORS的具体流程（了解）

1. 浏览器发送跨域请求

2. 服务器端收到一个跨域请求后，在响应头中添加Access-Control-Allow-Origin Header资源权限配置。发送响应

3. 浏览器收到响应后，查看是否设置了`header('Access-Control-Allow-Origin:请求源域名或者*');`

   如果当前域已经得到授权，则将结果返回给[JavaScript](http://lib.csdn.net/base/javascript)。否则浏览器忽略此次响应。

结论：

1. **跨域行为是浏览器行为，响应是回来了, 只是浏览器安全机制做了限制,  对于跨域响应内容进行了忽略。**
2. **服务器与服务器之间是不存在跨域的问题的**

##### jsonp与cors的对比

- jsonp兼容性好，老版本浏览器也支持，但是jsonp仅支持get请求，发送的数据量有限。使用麻烦
- cors需要浏览器支持cors功能才行。但是使用简单，**只要服务端设置允许跨域，对于客户端来说，跟普通的get、post请求并没有什么区别。**
- 跨域的安全性问题：**因为跨域是需要服务端配合控制的** ，也就是说不论jsonp还是cors，如果没有服务端的允许，浏览器是没法做到跨域的。

图灵机器人的接口文档: http://www.tuling123.com/help/h_cent_webapi.jhtml?nav=doc

