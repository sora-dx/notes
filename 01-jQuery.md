# jQuery基础

## 介绍

- 它的作者是 John Resig ,于2006年创建的一个开源项目

![img](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdx5nyyghzj308m02n0sm.jpg)

- jQuery 是一个 JavaScript 库(仓库)，它通过封装原生的 JavaScript 函数得到一整套定义好的方法



## 为什么要学jQuery?

它使诸如HTML文档遍历和操纵，事件处理，动画和Ajax等事情变得更简单，使用易于使用的API，可在多种浏览器中使用.结合多功能性和可扩展性，jQuery改变了数百万人编写JavaScript的方式

**通俗理解: ** 让我们操作页面/浏览器变得更加简单,并且没有兼容性问题 (write less, do more)

**写js原生的一些问题:**

- 实现同一功能,代码量相对较大
- 有兼容性问题

**jQuery :**

- 实现同一功能,代码量更少
- 处理了兼容性问题

**代码示例: **

```javascript
//需求: 
//点击div,改变div中的文本

//html
<div id="box">我女朋友长的好看,你有女朋友嘛?</div>

//js原生
var box = document.getElementById('box');
box.addEventListener('click',function(){ 
    this.innerText = '不好意思,刚才吹牛X了';
}, false);

//jQuery
$('#box').on('click',function(){
    $(this).text('jQuery就是屌');
})
```



## jQuery历史

- 从 2005 年 8 月开始,进入公共开发阶段,随之而来的新框架于 2006 年 1 月 14 正式以 jQuery 的名称发布。

- 2013 年 4 月发布了 jQuery 2.0,  5 月发布了 jQuery 2.0.2, 一个重大更新版本,不在支持 IE6/7/8,体积更小,速度更快

  ![img](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdx78906u3j30la07s0sx.jpg)



- jQuery3版本的改动：
  - 移除旧的IE工作区
  - jQuery 3.0运行在Strict Mode下
  - 引进for...of循环
  - 动画方面采用新的API
  - 延迟对象现在与JS Promises兼容
  - 。。。

## jQuery的使用

### jQuery 下载

- 官网: http://jquery.com/download/
- 第三方: http://www.jq22.com/jquery-info122

```js
标准版: 
Download the compressed, production jQuery 3.6.0    压缩混淆版

Download the uncompressed, development jQuery 3.6.0  开发版

Download the map file for jQuery 3.6.0  开发版和压缩混淆版的映射文件


瘦身版:
Download the compressed, production jQuery 3.6.0 slim build 

Download the uncompressed, development jQuery 3.6.0 slim build
```

### jQuery引入

```html
<script src="jquery.js"></script>
```



## jQuery对象模型

### jQuery执行时机

|          | **window.onload**                                        | **$(document).ready()**                               |
| -------- | -------------------------------------------------------- | ----------------------------------------------------- |
| 执行时机 | 必须等待网页全部加载完毕(包括 图片等),然后再执行包裹代码 | 只需要等待网页中的DOM结构 加载完毕,就能执行包裹的代码 |
| 执行次数 | 只能执行一次,如果第二次,那么 第一次的执行会被覆盖        | 可以执行多次,第N次都不会被覆盖                        |
| 简写方案 | 无                                                       | $(function () { });                                   |



### jQuery对象和DOM对象

#### 什么是DOM对象

DOM对象，即是我们用传统的方法(javascript)获得的元素对象。

#### 什么是jQuery对象

jQuery对象即是用jQuery类库的选择器获得的对象，jQuery对象就是通过jQuery包装DOM对象后产生的对象，它是jQuery独有的。如果一个对象是jQuery对象，那么就可以使用jQuery里的方法

#### jQuery对象和DOM对象的互相转换

- jquery对象和dom对象是不一样的！比如jquery对象不能使用dom的方法，dom对象不能使用jquery方法，

- jquery对象转换成 dom对象：即[index]和get(index)。jquery对象就是一个类数组对象

  ```js
  //html
  <ul>
      <li>one</li>
  	<li>two</li>
  	<li>three</li>
  </ul>
  
  //js
  console.log($('li')[0]) //  <li>one</li>
  ```

  ```js
  //html
  <ul>
      <li>one</li>
  	<li>two</li>
  	<li>three</li>
  </ul>
  
  //js
  console.log($('li').get(0)) //  <li>one</li>
  ```

- dom对象转换成jquery对象：对于一个dom对象，只需要用`$()`把dom对象包装起来，就可以获得一个jquery对象了，方法为$(dom对象);

  ```js
  //html
  <ul id="ul">
      <li>one</li>
  	<li>two</li>
  	<li>three</li>
  </ul>
  
  //js
  var ul = document.getElementById('ul')
  var $ul = $(ul) //$ul就是一个jquery对象
  ```

  



##  jQuery选择器

jQuery 选择器是 jQuery 库中非常重要的部分之一。它支持网页开发者所熟知的CSS 语法，快速轻松地对页面进行设置

![img](https://tva1.sinaimg.cn/large/007S8ZIlgy1gdx7n6l540j31cy0h4aa4.jpg)

### 基础选择器

| **选择器**                         | **描述**                                  | **返回** | **示例**                                                     |
| ---------------------------------- | ----------------------------------------- | -------- | ------------------------------------------------------------ |
| #id                                | 根据给定的id匹配一个元素                  | 单个元素 | $("#test")选取 id 为 test 的元素                             |
| .class                             | 根据给定的类名匹配元素                    | 集合元素 | $(".test")选取所有 class 为 test 的元素                      |
| element                            | 根据给定的元素名匹配元素                  | 集合元素 | $("p")选取所有的元素                                         |
| *                                  | 匹配所有元素                              | 集合元素 | $("*")选取所有的元素                                         |
| selector1,selector2, ...,selectorN | 将每一个选择器匹配到的元 素合并后一起返回 | 集合元素 | $("div,span,.myClass")选取所有div和span，以及拥有class为myClass 的标签的一组元素 |

### 层次选择器

如果想通过 DOM 元素之间的层次关系来获取特定的元素，例如后代元素，子元素，相邻元素和兄弟元素等，那么层次选择器是一个非常好的选择。



| **选择器**         | **描述**                             | **返回** | **示例**                                                    |
| ------------------ | ------------------------------------ | -------- | ----------------------------------------------------------- |
| $("parent child")  | 选取 parent元素里所有child(后代)元素 | 集合元素 | $(“div span”)选取div里的所有的span元素                      |
| $("parent>child")  | 选取 parent 元素下的child (子)元素   | 集合元素 | $(“div>span”)选取div元素下元素名是span的子元素              |
| $("prev+next")     | 选取紧接在 prev 元素后的 next 元素   | 集合元素 | $(“.one+div”)选取 class 为 one 的下一个 div兄弟元素         |
| $("prev~siblings") | 选取prev元素之后的所有siblings元素   | 集合元素 | $(“#two~div”)选取 id 为 two 的元素后面所有名为div的兄弟元素 |

### 过滤选择器

| **选择器**                           | **描述**                                                     | **返回**     | **示例**                                                     |
| ------------------------------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| :first                               | 选取第1个元素                                                | 单个元素     | $(“div:first”)选取所有 `<div>` 元素 中第一个 `<div>` 元素    |
| :last                                | 选取最后1个元素                                              | 单个元素     | $(“div:last”)选取所有 `<div>` 元素 中最后一个 `<div>` 元素   |
| :not(selector)                       | 去除所有与给定选择器 匹配的元素                              | 集合元素     | $(“input:not(.myClass)”)选取 class 不是 myClass 的 `<input>` 元素 |
| :even                                | 选取索引(从0开始)是偶数的所有元素                            | 集合元素     | $("input:even")选取索引是偶数的 `<input>`元素                |
| :odd                                 | 选取索引(从0开始)是奇数的所有元素                            | 集合元素     | $(“input:odd”)选取索引是奇数的 `<input>` 元素                |
| :eq(index)                           | 选取索引(从0开始)等于 index 的元素                           | 单个元素     | $(“input:eq(1)”)选取索引等于1的 `<input>` 元素               |
| :gt(index)                           | 选取索引(从0开始)大于 index的元素                            | 集合元素     | $(“input:gt(1)”)选取索引大于1的 `<input>` 元素               |
| :lt(index)                           | 选取索引(从0开始)小于 index的元素                            | 集合元素     | $(“input:lt(1)”)选取索引小于1的 `<input>` 元素               |
| :header                              | 选取所有的标题元素，即`<h1>`到`<h6>`                         | 集合元素     | $(":header")选取页面中所有的标题元素                         |
| :contains(text)                      | 选取含有文本内容为 text 的元素                               | 集合元素     | $("div:contains('test')")选取含有文本内容为 test 的`<div>`元素 |
| :empty                               | 选取不包含子元素或文本的空元素                               | 集合元素     | $(“div:empty”)选取不包含子元素或文本的空 `<div>` 元素        |
| :has(selector)                       | 选取含有给定选择器 匹配的子元素的元素                        | 集合元素     | $(“div:has(.myClass)”)选取 子元素中包含了class 为 myClass 的元素的 `<div>` 元素 |
| :parent                              | 选取含有子元素或文本的元素                                   | 集合元素     | $(“div:parent”)选取含有子元素或文本的 `<div>` 元素           |
| :first-child                         | 选取第1个子元素                                              | 集合元素     | $(“div :first-child”)选取 为第一个子元素`<div>`              |
| :last-child                          | 选取最后1个子元素                                            | 集合元素     | $(“div :last-child”)选取是最后一个子元素的`<div>`            |
| :only-child                          | 选取是唯一子元素的元素                                       | 集合元素     | $(“div :only-child”)选择 `<div>` 是唯一子元素的元素          |
| :nth-child(index/ even/odd/equation) | 选取每个父元素下的第index(索引值为奇数/ 索引值为偶数/索引值等于某个表达式)个子元素，index 从1开始 | **集合元素** | $(“div:nth-child(1)”)选取每个div **中第一个子元素**          |

### 属性过滤选择器

| **选择器**                           | **描述**                          | **返回** | **示例**                                                     |
| ------------------------------------ | --------------------------------- | -------- | ------------------------------------------------------------ |
| [attribute]                          | 选取拥有此属性的元素              | 集合元素 | $(“div[id]”)选取拥有属性 id 的元素                           |
| [attribute=value]                    | 选取属性的值为value的元素         | 集合元素 | $(“div[title=test]”)选取属性 title 为 test 的`<div>`元素     |
| [attribute!=value]                   | 选取属性的值不等于value的元素     | 集合元素 | $(“div[title!=test]”)选取属性 title 不等于 test 的`<div>`元素 |
| [attribute^=value]                   | 选取属性的值以value开始的元素     | 集合元素 | $(“div[title^=test]”)选取属性 title 以 test 开始的`<div>`元素 |
| [attribute$=value]                   | 选取属性的值以 value结束的元素    | 集合元素 | $(“div[title$=test]”)选取属性 title 以 test 结束的 `<div>` 元素 |
| [attribute*=value]                   | 选取属性的值含有 value 的元素     | 集合元素 | $(“div[title*=test]”)选取属性 title 含有 test 的 `<div>` 元素 |
| [selector1][selector2]...[selectorN] | 选取匹配以上所有属性 选择器的元素 | 集合元素 | $(“div[id][title*=test]”)选取拥有属性 id ，且属性 title 含有 test 的`<div>` 元素 |

### 表单选择器

- 表单选择器是为了能更加容易地操作表单，表单选择器是根据元素类型来定义的

| **选择器** | **描述**                                                     | **返回** | **示例**                                                     |
| ---------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| :enabled   | 选取所有可用元素                                             | 集合元素 | $(“input:enabled")选取页面内所有可用元素                     |
| :disabled  | 选取所有不可用元素                                           | 集合元素 | $(“input:disabled")选取页面内所有不可用元素                  |
| :checked   | 选取所有被选中的元素(单选框、复选框)                         | 集合元素 | $(“input:checked”)选取所有被选中的 `<input> ` 元素           |
| :selected  | 选取所有被选中的选项元素(下拉列表)                           | 集合元素 | $("select option:selected")选取所有被选中的选项元素          |
| :input     | 选取所有的 `<input>`、 `<textarea>`、 `<select>`和 `<button>`元素 | 集合元素 | $(":input")选取所有的`<input>`、`<textarea>`、`<select>`和`<button>`元素 |
| :text      | 选取所有的单行文本框                                         | 集合元素 | $(":text")选取所有的单行文本框                               |
| :password  | 选取所有的密码框                                             | 集合元素 | $(":password")选取所有的密码框                               |
| :radio     | 选取所有的单选框                                             | 集合元素 | $(":radio")选取所有的单选框                                  |
| :checkbox  | 选取所有的多选框                                             | 集合元素 | $(":checkbox")选取所有的多选框                               |
| :submit    | 选取所有的提交按钮                                           | 集合元素 | $(":submit")选取所有的提交按钮                               |

### 筛选方法

**注意: 上面的选择器只要根据传入字符串不同来区分,而筛选选择器是一些方法**

| **名称**               | **用法**                    | **描述**                                                     |
| ---------------------- | --------------------------- | ------------------------------------------------------------ |
| **children(selector)** | $('ul').children('li')      | 找到自己的所有符合条件的直接子元素 <br />当前于子代选择器$(“ul>li”); |
| **find(selector)**     | $('ul').find('li')          | 找到自己的所有符合条件的后代元素 <br />当前于后代选择器$(“ul li”); |
| **siblings(selector)** | $(“#first”).siblings(“li”); | 查找兄弟元素，不包括自己本身。                               |
| **parent()**           | $(“#first”).parent();       | 查找直接父亲元素                                             |
| **eq(index)**          | $(“li”).eq(2);              | 找到所有符合条件的li里面对应下标的元素,索引从0开始           |
| **next()**             | $('#first').next()          | 下一个兄弟                                                   |
| **index()**            | $('li').index()             | 返回对应的索引                                               |



## jQuery样式操作

### 操作行内样式方法

> 描述:设置或者修改样式，操作的是style属性。

####  设置单个样式

**语法: **jQuery对象.css('属性名', '属性值')

```javascript
//html
<div id="box"></div>

//js
$("#box").css("background","gray");//将背景色修改为灰色

//js代码运行完毕的结果
<div id="box" style="background: gray"></div>
```

#### 设置多个样式

**语法: **jQuery对象.css({

​					属性名: 属性值,

​					属性名: 属性值

​				   })

```javascript
//html
<div id="box"></div>

//js
$("#one").css({

    "backgroundColor":"gray",

    "width":"400px",

    "height":"200px",
    "fontSize": "30px"

});

//js执行完毕的结果
<div id="box" style="background:gray; width:400px; height:200px"></div>



```



- 获取行内样式

  **语法:**jQuery对象.css('属性名')

  ```javascript
  //html
  <div id="box" style="background: gray width:100px"></div>
  
  $("#box").css("background-color"); //返回的是 rgb(128, 128, 128) --> gray
  $("#box").css("width"); //返回100px
  ```

  

### 操作class样式方式

#### 添加样式类

**语法:**jQuery对象.addClass('类名') 

**注意: **传入的参数,不需要加点

```javascript
//html
<div id="box" ></div>

//js
$('#box').addClass('one');

//执行完之后的结果
<div id="box" class="one"></div>

//======================================================================================

//如果想要同时添加多个
//html
<div id="box" ></div>

//js
$('#box').addClass('two three');

//结果
<div id="box" class="two three"></div>
```



#### 移除所有样式类

**语法:**jQuery对象.removeClass('类名')

- 如果不传参数,那么会移除所有的类名

  ```javascript
  //html
  <div id="box" class="one two three"></div>
  
  //js
  $('#box').removeClass();
  
  //执行完毕的结果
  <div id="#box" class></div>
  ```

  

- 如果传入参数,删除指定的类名

  ```javascript
  //html
  <div id="box" class="one two three"></div>
  
  //js
  $('#box').removeClass('one');
  
  //执行完毕的结果
  <div id="#box" class="two three"></div>
  
  //======================================================================================
  
  //如果想同时删除多个类名
  //html
  <div id="box" class="one two three"></div>
  //js
  $('#box').removeClass('one three');
  //结果
  <div id="#box" class="two"></div>
  ```


#### 判断是否有样式类

**语法:**jQuery对象.hasClass('类名')  返回的是true/false

```javascript
//html
<div id="box" class="one"></div>

//js
$('#box').hasClass('one'); //返回 true
$('#box').hasClass('two'); //返回 false

```

#### 切换样式类

**作用: **如果有这个类名，则移除该样式，如果没有，添加该类名。

**语法:**jQuery对象.toggleClass('类名')

```javascript
//html
<div id="box"></div>

//js
$('#box').toggleClass('one');

//执行完的结果
<div id="box" class="one"></div>

//此时再执行一次toggleClass('one');
$('#box').toggleClass('one');

//执行完的结果
<div id="box" class></div>

```



## jQuery中的隐式迭代

> 迭代: 就是循环的意思



**需求:**现在我们有三个盒子,背景默认是透明的.我们现在想要给他们三个都设置黄色的背景颜色

<img src="media\隐式迭代.png">

```html
<!-- html结构 -->
<div style="border:5px solid red"></div>
<div style="border:5px solid green"></div>
<div style="border:5px solid blue"></div>

```

```css
/*css*/
div{
    width: 200px;
    height: 200px;
    float:left;
    margin-left:20px;
 }
```

**js原生解决:**

```javascript
//js
var divs = document.getElementsByTagName('div');

for(var i = 0; i < divs.length; i++){
    divs[i].style.background = 'yellow';
}

//执行完毕之后,这三个div的背景颜色都变成了黄色
```

**如果我们使用jQuery来做这件事情:**

```javascript
$('div').css('background-color', 'yellow'); //只需要这一行代码就可以了
```

<img src="media\jQuery隐式迭代图解.png">

### 小结:

隐式迭代: jQuery内部会帮我们遍历DOM对象,然后给每一个DOM对象实现具体的操作



### 思考题:

js代码执行返回值是什么?

```javascript
//html
<div style="border:5px solid red"></div>
<div style="border:5px solid green"></div>
<div style="border:5px solid blue"></div>

//js

$('div').css('border'); //5px solid rgb(255, 0, 0)   返回的是第一个div的行内样式


```

**说明: **当我们要获取元素某些属性值的的时候,jQuery对象中可能有多个DOM对象,而每个DOM对象的属性值可能都不一样,jQuery不会返回所有的属性值,只会返回第一个DOM对象中的属性值



## jquery操作DOM

### 创建元素

**语法:** $('html形式的字符串')

```javascript
$('<span>这是一个span元素</span>'); //创建了一个jQuery包装的span,此时并没有添加到DOM树上
var span = document.createElement('span')
$(span)
```

### 添加元素

#### append方法

**语法: **jQuery对象.append(参数)   

##### 传入一个jQuery对象

```javascript
//html
<div id="box"></div>
<div ></div>
    
//js
var $span = $("<span>这是一个span元素</span>");
$("#box").append($span);

//执行完的结果
<div id="box">
    <span>这是一个span元素</span>
</div>
<div ></div>

//思考:如果执行下面这行代码,结果是什么?
$("div").append($span);

```

**注意: 如果添加已经存在的元素**

```javascript
//html
<div></div>
<p></p>

//js
var $p = $('p');
$('div).append($p);
  
//执行之后的结果
<div>
  <p></p> 
</div>
 //注意：如果添加的是已经存在的元素,会有剪切的效果。


```



#####  传入一个html形式的字符串

```javascript
//html
<div></div>

//js
$('div').append('<span>这是一个span元素</span>');

//执行之后的结果
<div>
    <span>这是一个span元素</span>
</div>
```

##### 传入一个dom对象

```javascript
//html
<div></div>
<p id="p"></p>

//js
var p = document.getElementById('p');
$('div').append(p);
  
//执行之后的结果
<div>
  <p></p> 
</div>
//注意：也会有剪切的效果。
```

#### 其他跟append类似的方法 

- prepend   在前面添加子元素
- after  放到自己的后面(变为兄弟元素)
- before 放到自己的前面(变为兄弟元素)



#### 调用html方法

**语法: **jQuery对象.html('html形式的字符串')

```javascript
//html
<div>
    div里面的文本
	<p></p>
</div>

//js
$('div').html('<span>这是一段内容</span>');

//执行完的结果
<div>
    <span>这是一段内容</span>
</div>
//注意: 会有覆盖的作用


```

#### 小结:  

- append(jQuery对象/ 'html字符串'/DOM对象)  有剪切效果
- html('html字符串')  会覆盖以前的内容





#### html()的其他作用

##### html()  不传参数  用于获取内容

```javascript
//html
<div>
    <p></p>
	<span></span>
	文本
</div>

//js
console.log($('div').html()); // 返回   <p></p> 
                					  <span></span>
				                       文本
```

##### html('') 传入一个空的字符串

> 不推荐使用,因为子元素的事件没有被清除,会造成内存泄露

**语法: **jQuery对象.html('') 传递进来一个空的字符串

```javascript
//html
<div>
    <p></p>
	<span></span>
</div>

//js
$('div).html('');

//执行完的结果
<div></div>

```

### 清空元素

#### empty方法

>清空指定节点的所有子节点  (推荐使用，会清除子元素上绑定的内容)

**语法: **jQuery对象.empty()

```javascript
//html
<div>
    <p></p>
	<span></span>
</div>

//js
$('div).empty();
  
//执行完的结果
<div></div>
```

### 删除元素

>把自己删除掉

**语法:** jQuery.remove();

```javascript
//html
<p></p>
<div>
   <span></span>
   文本
</div>

//js
$('div').remove();

//执行之后的结果
<p></p>
```



### 克隆元素

**语法: ** jQuery对象.clone([boolean])

#### 不传参数

>不传参数相当于传入一个false,会复制所有

```javascript
//html
<div id="box"></div>
<p>
    <span>span元素</span>
</p>

//js
var newP = $('p').clone();
$('#box').append(newP);

//执行完的结果
<div id="box">
   <p>
     <span>span元素</span>
   </p> 
 </div>
<p>
    <span>span元素</span>
</p>

```

#### 传true

>传true会克隆所有内容,并且注册的事件也一起克隆下来

```javascript
//html
<div id="box"></div>
<p>
    <span>span元素</span>
</p>

//js
$span = $('span');
//这是jQuery中注册事件的方式,后面会仔细讲
$span.on('click', function(){
      console.log('span')
})
var newP = $('p').clone(true);
$('#box').append(newP);

//执行完的结果
<div id="box">
   <p>
     <span>span元素</span>   //点击会打印span
   </p> 
 </div>
<p>
    <span>span元素</span>    //点击会打印span
</p>
```

#### clone(true),无法克隆用原生方式注册的事件

```javascript
//html
<div id="box"></div>
<p>
    <span>span元素</span>
</p>

//js
var span = document.getElementsByTagName('span')[0];
span.onclick = function(){
    console.log('span')
}
var newP = $('p').clone(true);
$('#box').append(newP);

//执行完的结果
<div id="box">
   <p>
     <span>span元素</span>   //点击不打印span
   </p> 
 </div>
<p>
    <span>span元素</span>    //点击会打印span
</p>
```



## jQuery动画

> jquery提供了三组基本动画，这些动画都是标准的、有规律的效果，jquery还提供了自定义动画的功能。

### 显示与隐藏

- show([speed],[easing],[callback])  显示
- hide([speed],[easing],[callback])   隐藏
- toggle([speed],[easing],[callback])  显示隐藏的切换

<img src="media\显示隐藏.gif">

### 滑入与滑出

- slideDown([speed],[easing],[callback])  滑入
- slideUp([speed],[easing],[callback])  滑出
- slideToggle([speed],[easing],[callback])  滑入滑出切换

<img src="media\滑入滑出.gif">

### 淡入与淡出

- fadeIn([speed],[easing],[callback])  淡入
- fadeOut([speed],[easing],[callback])  淡出
- fadeToggle([speed],[easing],[callback])  淡入淡出切换

<img src="media\淡入淡出.gif">



**参数详解：**

- speed(可选)：动画的执行时间

​     1.如果不传，就没有动画效果。

​     2.单位是毫秒值(比如1000),动画在1000毫秒执行完成(**推荐**)

​     3.固定字符串，slow、normal、fast，如果传其他字符串，则默认为normal。

- easing(可选) : 用来指定切换效果，默认是"swing"，可用参数"linear"

  - swing 秋千  先快 再慢, 再快
  - linear 线性

  <img src="media\easing.gif">

  

- callback(可选):执行完动画后执行的回调函数



### 小结

	1. jQuery给我们提供了三组动画，show/hide、slideDown/slideUp、fadeIn/fadeOut
	2. show/slideDown/fadeIn三个是显示效果、hide/slideUp/fadeOut三个是隐藏效果。
	3. show/hide修改的是元素的height,width,opacity。slide系列方法修改的是元素的height。fade系列方法修改的是元素的opacity。这三种方法修改的这些值，都是带数字的，因为带了数字才能做渐变。

### 自定义动画

#### 为什么要学习自定义动画?

> 因为我们实际开发中jQuery提供的三组基础动画不能满足需求

#### 如何自定义动画

**语法:** jQuery对象.animate(json,[speed],[easing],[callback])

**参数详解: **

- json：要执行动画的CSS属性，带数字（必选）

- speed：执行动画时长（必选，默认normal）

- easing：控制动画的效果 

  ​     1.swing：摇摆、秋千(默认) 

  ​     2.linear:匀速

- callback：动画执行完后立即执行的回调函数（可选）

动画支持的属性(必须带数字)：

​    <http://www.w3school.com.cn/jquery/effect_animate.asp>



### 动画队列问题

<img src="media\动画队列导致的问题.gif">

#### 为什么会出现这个问题?

在同一个元素上添加多个动画，那么对于这些动画会被放到动画队列中，等前面的动画执行完成了才会执行下一个动画.

<img src="media\动画队列图解.png">



### 停止动画

**语法:** jQuery对象.stop([clearQueue], [jumpToEnd])

**作用: **停止当前正在执行的动画效果

**参数详解**

- clearQueue：是否清除动画队列  默认false
- jumpToEnd：是否跳转到当前动画的最终效果 默认fasle
- 如果不传,默认就是false
  - stop() --> stop(fasle,false)
  - stop(true) --> stop(true,false)

<img src="media\stop方法传入不同的参数.gif">



## jQuery操作元素的属性

### 设置单个属性

**语法: **jQuery对象.attr('属性名', '属性值');

```javascript
//html
<div></div>

//js
$('div').attr('id', 'box');
$('div').attr('a', 1);
//执行完的结果
<div id="box" a="1"></div>    //w3c标准和自定义的都可以

```



### 设置多个属性

**语法: **jQuery对象.attr({

​	属性名: 属性值,

​	...

});

```javascript
//html
<div></div>

//js
$('div').attr({
    id : 'box',
    a : 1
});

//执行完的结果
<div id="box" a="1"></div>    //w3c标准和自定义的都可以
```





### 获取属性的值

**语法: **jQuery对象.attr('属性名');   返回属性的值, 如果没有这个属性,会返回undefined

```javascript
//html
<div id="box" a = "1" ></div>

//js
$('div').attr('id');  //box
$('div').attr('a');   //1
$('div').attr('index');  //undefined

```



### 移除属性

**语法: **jQuery对象.removeAttr('属性名');   返回不传就什么都不做

```javascript
//html
<div id="box" a = "1" ></div>

//js
$('div').removeAttr('id');

//执行完的结果
<div  a = "1" ></div>
```



### prop方法 

注意：在jQuery1.6之后，对于checked、selected、disable这类boolean类型的属性来说，如果使用attr方法获取属性值，得到的不是true和false，而是checked以及undefined。，使用prop方法来获取或者设置checked、selected、disable这类的值。prop方法使用跟attr方法一样,但是prop无法操作自定义的属性。

- 设置属性

**语法: **jQuery对象.prop('属性名', 属性值);  

**语法: **jQuery对象.prop({

​	属性名 : 属性值,

​	...

});  

- 获取属性

**语法: **jQuery对象.prop('属性名');   返回true/false





### 小结:

attr 方法可以操作自定义的属性

prop 操作checked、selected、disable这类boolean值类型的属性,不可以操作自定义的属性



## jQuery操作文本和内容

### val方法

**作用: ** val方法用于设置和获取表单元素的值，例如input、select、textarea的值

- 设置值

  **语法: ** jQuery对象.val('值')


- 获取值

  **语法: ** jQuery对象.val()



### html方法

- 设置内容

  **语法: ** jQuery对象.html('html字符串')


- 获取内容

  **语法: ** jQuery对象.html()

### text方法

- 设置内容

  **语法: ** jQuery对象.text('文本字符串')

- 获取内容

  **语法: ** jQuery对象.text()

### 小结

- val操作表单元素
- html 会识别html结构
- text 只识别文本





## jQuery操作尺寸

在jquery里面可以非常方便的操作元素或者窗口的尺寸。

- height()与width()：设置或者返回元素的宽度及高度,返回结果是数值类型。(content宽高)
- innerWidth()与innerHeight()：返回元素的宽度及高度（content + padding）
- outerWidth()与outerHeigth()：返回元素的宽度及高度（content + padding + border）
- outerWidth(true)与outerHeight(true)：返回元素的宽度及高度（content + padding + border + margin）



## jQuery操作坐标值

### offset方法

**作用: **设置或者获取元素相对于文档document的位置。

- 设置位置

  **语法: ** jQuery对象.offset({left:num, top: num})



- 获取位置

  **语法: ** jQuery对象.offset()

**注意：**使用offset操作，如果元素没有设置定位(默认position:static)，则会把position修改为relative.会修改left、top

### position方法

**作用: ** 获取相对于其最近的有定位的父元素的位置。

**语法: ** jQuery对象.position()    返回值为对象：{left:num,top:num}

**注意：**position方法只能获取，不能设置

![position](media\position.png)

### scrollTop 方法

**作用: ** 设置或获取元素的内容相对顶部滚动出去的距离

- 设置距离

  **语法: ** jQuery对象.scrollTop(num);

$(selector).scrollTop(100);

- 获取距离

  **语法: ** jQuery对象.scrollTop(); //返回num

### scrollLeft 方法

**作用: ** 设置或获取元素的内容相对左侧滚动出去的距离

- 设置距离

  **语法: ** jQuery对象.scrollLeft(num);

$(selector).scrollTop(100);

- 获取距离

  **语法: ** jQuery对象.scrollLeft(); //返回num

### 小结:

- offset 相对文档的坐标
- position相对定位父元素的坐标,只读
- scorllleft, scrolltop 元素内容滚动出去的距离





## jQuery的事件

>JavaScript中已经学习过了事件，但是jQuery对JavaScript事件进行了封装，增加并扩展了事件处理机制。jQuery不仅提供了更加优雅的事件处理语法，而且极大的增强了事件的处理能力。

### 注册事件

#### 简单事件绑定

click(handler)             单击事件

mouseenter(handler)       鼠标进入事件

mouseleave(handler)       鼠标离开事件

scroll(handler)                 滚动事件

**缺点：**一次只能绑定一个事件

#### on方法

> on 方法 jQuery1.7之后，jQuery用on统一了所有事件的处理方法。

**语法: **jQuery对象.on('事件类型', [ '选择器' ], [data] ,'事件处理函数')

**参数详解:**

-  第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件
-  第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
-  第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
-  第四个参数：handler，事件处理函数

```javascript
//html
<div id="box">
    <span></span>
	<span></span>
</div>


//js
// 表示给$(selector)绑定代理事件，但必须是它的内部元素span才能触发这个事件
//只有点击span的时候才会触发这个事件
$('#box').on('click', 'span', function () {
    console.log(this); //span
});


// 表示给$(selector)绑定事件，并且由自己触发。
//点击box就会触发
 $('#box').on('click',function () {
     console.log(this); //div
 })

```



### 解绑事件

> off方法

**语法: ** jQuery对象.off(参数)

- 不传参数

  **作用:  **解绑匹配元素的所有事件

```javascript
//html
 <div id="box">
     <span>span1</span>
	 <span>span2</span>
 </div>

//js
$('#box').on('click mouseenter', 'span', function () {
    console.log(this); 
});

//解绑所有的事件
$('#box').off();

```



- 传入对应的事件类型

  **作用: **解绑匹配元素对应的事件

```javascript
//html
 <div id="box">
     <span>span1</span>
	 <span>span2</span>
 </div>

//js
$('#box').on('click mouseenter', 'span', function () {
    console.log(this); 
});


$('#box').off('click');  //click解绑, mouseenter没有解绑
```



- 传入off( “click”, “**” ); 

  **作用: **解绑所有代理的click事件，元素本身的事件不会被解绑

```javascript
//html
 <div id="box">
     <span>span1</span>
	 <span>span2</span>
 </div>

//js
$('#box').on('click mouseenter', 'span', function () {
    console.log(this);  //span的click不会触发
});
$('#box').on('click mouseenter',function () {
        console.log(this); //不影响
});
 $('#box').off('click', '**');
```



###  事件触发

- 简单事件触发

  **作用: **手动触发我们给元素绑定的事件

  **语法: **jQuery对象.click(); //触发click事件

- trigger方法触发事件

  **作用: **根据传入的参数手动触发我们给元素绑定的事件

  **语法: **jQuery对象.trigger('事件名'); //触发指定的事件事件


- triggerHandler触发 

  **作用: **触发指定事件，不触发浏览器行为,也不会产生冒泡

  **语法: **jQuery对象.triggerHandler('事件名'); 





### jQuery事件对象

| **对象属性**                | **解释**                                           |
| --------------------------- | -------------------------------------------------- |
| **event.type**              | 事件类型                                           |
| **event.data**              | 存储绑定事件时传递的附加数据                       |
| **event.target**            | 点了谁就是谁                                       |
| **event.currentTarget**     | 当前DOM元素，等同于this                            |
| **event.delegateTarget**    | 代理对象                                           |
| **screenX和screenY**        | 对应设备屏幕最左上角的值                           |
| **offsetX和offsetY**        | 点击的位置距离元素的左上角的位置                   |
| **clientX和clientY**        | 距离可视区左上角的位置                             |
| **pageX和pageY**            | 距离页面最顶部的左上角的位置（会计算滚动条的距离） |
| **event.keyCode**           | 键盘码                                             |
| **event.stopPropagation()** | 阻止事件冒泡行为                                   |
| **event.preventDefault()**  | 阻止浏览器默认行为                                 |

## 其他内容

### jQuery事件拓展

#### jQuery事件的发展历程

> 简单事件绑定>>bind事件绑定>>delegate事件绑定>>on事件绑定**(推荐)**

#### bind事件绑定

> 可以绑定多个事件,不支持动态代理。  
>
> 不推荐使用，jQuery1.7版本后被on取代 

**语法: ** jQuery.bind('事件类型', 事件处理函数)

```javascript
$("p").bind("click mouseenter",function(){

    //code...

});
```

#### delegate事件绑定

> 比bind强大, 支持动态绑定事件

**语法: ** jQuery.delegate('选择器','事件类型' ,事件处理函数);

**参数详解:**

- 第一个参数：selector，要绑定事件的元素
- 第二个参数：事件类型
- 第三个参数：事件处理函数

```javascript
$(".parentBox").delegate("p","click", function(){

    //为 .parentBox下面的所有的p标签绑定事件

});

```

#### bind和delegate解绑事件的方式

- unbind() 方式

```javascript
$(selector).unbind(); //解绑所有的事件

$(selector).unbind(“click”); //解绑指定的事件

```

- undelegate() 方式

```javascript
$( selector ).undelegate(); //解绑所有的delegate事件

$( selector).undelegate( “click” ); //解绑所有的click事件

```

#### one绑定事件

- 不管是 bind() 还是 on() ,绑定事件后都不是自动移除事件,需要通过 unbind()和 off() 来手工移除。jQuery 提供了 one() 方法,绑定元素执行完毕后自动移除事件,方法仅触发一次的事件。
  - **type:** 添加到元素的一个或多个事件。
  - **data:** 将要传递给事件处理函数的数据映射
  - **fn**: 每当事件触发时执行的函数。

### 链式编程

通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 this。

```javascript
//html
<div><div>

//js
$('div').addClass('one').attr('id',1);

//执行完的结果
<div class="one" id="1"><div>
```



### end方法

**作用: **筛选选择器会改变jQuery对象的DOM对象，想要返回到上一次的状态，并且返回匹配元素之前的状态。

```javascript
//html
<div>
	<span></span> 
	<span></span>
</div>

//js
console.log($('div').attr('id', 'box').children()) //返回$('span)
console.log($('div').attr('id', 'box').children().end()) //返回$('div')


```



### each方法

有了隐式迭代，为什么还要使用each函数遍历？

大部分情况下是不需要使用each方法的，因为jQuery的隐式迭代特性。

如果要对每个元素做不同的处理，这时候就用到了each方法

**语法:** jQuery对象.each(function(index,element){})

- 回调函数的第一个形参 表示当前元素在所有匹配元素中的索引号
- 回调函数的第二个形参 表示当前元素（DOM对象）



### 多库共存

我们知道jQuery占用了这个`$`标识符，如果引用的其他库也用到这个标识符，这时候为了保证每个库都能正常使用，这时候就存在了多库共存的问题。

后引入的库的`$`的会覆盖掉先引入的库中的$。

- 如果先引用的jQuery,后引用其他的库

  解决办法：jQuery库中 $ 和 jQuery这个变量是一样的

  ```javascript
  console.log($ === jQuery);//true
  
  console.log(jQuery('div') === $('div')) //true
  ```

- 如果先引入其他的库,后引入的jQuery库

  解决办法： 可以让jquery交出`$`符的控制权.

```javascript
console.log($);//function(selector, context){}

$.noConflict();//释放$的控制权

console.log($);//undefined

jQuery(function () {
  
    jQuery("div").html("我是div的内容");
  
});
```

