#### 固定定位

`position:fixed`，固定定位的元素从文档流中删除，相对于视口来进行定位。

opacity属性：指定了一个元素的透明度。当该属性的值被应用到某个元素上的时候是把这个元素当成一个整体来看待（内容、背景色、前景色-文字、边框），这个元素和其子元素也会有透明度。

opacity的值：0为完全透明，1位完全不透明。可以使用小数。

`display:none`

格式：`visibility:value`

* visible，可见
* hidden，元素不可见，但是依然像可见时影响文档的布局。

__display:none__ 和__visibility:hidden__ 的区别，display:none时完全从文档中移除，对布局不再有影响。但是visibility:hidden依然会影响布局。



#### 层叠顺序

从左到右是x轴，从上到下是y轴，从后到前z轴。我们可以使用`z-index`来设置z轴。

格式：`z-index:value`

value的值：

* `auto`，可以当做0来处理。

  元素一旦定位，z-index就会自动生效。这个时候你可以将z-index当做默认的0。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <meta charset="utf-8" />
      <style>
          div {
              position:absolute;
              z-index:auto;
              top:0;
              left:0;
              
              width: 100px;
              height: 100px;
              border: 1px solid green;
          }

          #f1 {
              background-color: green;
          }

          #f2 {
              background-color: pink;
          }
      </style>
  </head>

  <body>
      <div id="f1"></div>
      <div id="f2"></div>
  </body>

  </html>
  ```

  当元素层叠水平一致。层叠顺序相同，源代码后面的元素会覆盖前面的元素。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <meta charset="utf-8" />
      <style>
          div {
              position: absolute;
              z-index: auto;
              top: 0;
              left: 0;

              width: 100px;
              height: 100px;
              border: 1px solid green;
          }

          #f2 {
              background-color: pink;
          }

          #f1 {
              position: static;
              background-color: green;
          }

      </style>
  </head>

  <body>
      <div id="f2"></div>
      <div id="f1"></div>

  </body>

  </html>
  ```

  定位元素在非定位元素上面。z-index只能用在定位元素上。

* 数值，值为整数（正数或负数），值越大离我们越近。

  多个元素之间的z-index的值无需连续。


先有鸡还是先有蛋。 





HTML5新增了什么东西。新增了语义化标签、标签属性、新增本地存储、图形绘制、地理位置等等。 （IE9部分支持，IE10大面积支持）



#### 什么是语义化标签



所谓语义化就是你写的`HTML`结构，是用相对应的有一定语义的标签表示、标记的，因为HTML本身就是标记语言。



#### 为什么要用语义化标签

1. HTML语义化让页面内容结构化，便于浏览器、搜索引擎解析。
2. 即使在没有CSS样式的情况下也能以一种文档格式显示，并且是容易阅读的。

#### section标签

`section`标签表示页面中的一个内容区块，比如章节、页眉、页脚或页面中的其他部分。它可以与`h1`、`h2`、`h3`、`h4`、`h5`、`h6`等标签结合使用，标示文档结构。



内容区块将HTML页面按照逻辑进行分隔后的单位。



一个section通常由内容和标题组成。


#### header标签

`header`标签表示页面中一个内容区块（`section`）或整个页面的标题。

`header`标签是一种具有引导和导航作用的结构标签，通常用来放置整个页面或页面内的一个内容区块的标题，但也可以包含其他内容，例如数据表格、搜索表单或相关的`LOGO图片`。



1. 用在整个网页上。
2. 用在某个区块上面。



一个header标签中也应该有标题标签。

### footer标签

`footer`标签可以作为其上层父级内容区块或一个根区块的脚注。`footer`通常包括其相关区块的脚注信息，如作者、相关阅读链接以及版权信息等。



和header标签一样一个页面也可以出现多个footer。

#### nav标签

`nav`标签是一个可以用来作为页面导航的链接组，其中的导航标签链接到其他页面或当前页面的其他部分。并不是所有的链接组都要放进`nav`标签，只需要将主要的、基本的链接组放进`nav`标签即可。



一个页面当中可以拥有多个nav标签。



* 侧边栏导航。
* 导航菜单
* 翻页操作
* Nav可以用在你觉得重要的所有的导航链接中。



#### article标签

`article标签`代表文档、页面或应用程序中独立的、完整的、可以独自被外部引用的内容。它可以是一篇博客或报章杂志中的文章、一篇论坛帖子、一段用户评论或一个独立的插件，或者其他任何独立的内容。



article标签可以看成是一种特殊种类的section，它比section更加强调独立性。



section标签强调分段或分块，article强调独立性。



#### aside标签

`aside`标签，`aside`标签用来表示当前页面或文章的附属信息部分，它可以包含与当前页面或主要内容相关的引用、侧边栏、广告、导航条，以及其他类似的有别于主要内容的部分。

####  `<mark>` 标签，定义带有记号的文本（加上背景颜色）。

用来加上背景颜色，用来提醒用户。当前标记出来的内容是和用户当前的操作有关的。



#### `<abbr>`：缩写标签



* title属性：表示这个缩写的全称是什么。

当光标移动到这个标记出来的文本上时会出现一个提示框。



#### 表单新增的标签

```html
<input autocomplete="off" list="cars"/>
<datalist id="cars">
  <option value="BMW">
  <option value="Ford">
  <option value="Volvo">
  <option value="a">
  <option value="aa">
  <option value="abc">
  <option value="x">
</datalist>
```

1. input标签的`autocomplete`属性关闭浏览器自带的提交记录。

   `autocomplete`的值：

   * on，显示提交列表。
   * off，关闭提交列表
   * 不指定，不指定那么按照浏览器的默认设置。

2. 使用了input的list属性，用来绑定`datalist`标签。

3. `datalist`标签中设定的option标签为其设定value值表示提示列表的每一项。



#### 表单新增的属性

* `<input />`，type新增的属性值

  * email：表示输入的内容必须是一个邮箱地址。否则不允许提交。

    emial不检查是否为空，如果要检查需要加上required属性。

  * url，表示输入的内容必须是一个url地址，否则不允许提交。

    url不检查是否为空，如果要检查需要加上required。

  * number，输入数值。

    * min，允许的最小值
    * max，允许的最大值。
    * step，步长（允许的间隔值）

  * date，选择年、月、日

  * time，选择时间。

  * search，搜索

  * range，在浏览器中以滑动条方式选择值。

    * min，设定的最小值
    * max，设定的最大值。
    * step，每次拖动的间隔值。

* __`autofocus`__，让画面打开时让某个拥有该属性的输入框自动获得焦点。

* __`placeholder`__，提示用户可以输入的内容（未输入时显示要输入的信息）



#### 音频、视频

* 音频标签

  `<audio></audio>`

  * `src`属性：要播放的音频的URL地址
  * `controls`属性：是否显示自带的控制条。
  * `muted`属性：静音
  * `autoplay`，自动播放。（浏览器有可能禁用掉）
  * `loop`，循环播放。

  支持格式：mp3、ogg、wav

* 视频标签

  `<video></video>`

  - `src`属性：要播放的视频的URL地址
  - `controls`属性：是否显示自带的控制条。
  - `muted`属性：静音
  - `autoplay`，自动播放。（浏览器有可能禁用掉）
  - `loop`，循环播放。
  - `poster`，替代图片。

#### CSS3

`选择器-》属性`

#### 层次选择器

* `E F`，后代选择器。可以选择子元素、孙子、重孙子。。。。。
* `E > F`，子选择器，选择匹配的F元素且匹配的F元素是E元素的子元素。
* `E + F`，相邻兄弟选择器，选择匹配的F元素且匹配的F元素仅位于匹配的E元素的后面。
* `E~F`，兄弟选择器，选择匹配的F元素，且位于匹配的E元素的后面的所有的F元素。

#### 属性选择器

* `E[attr]`，选择匹配具有attr的E元素，其中的E表示的是HTML标签，attr表示的是html标签所属的属性。

  可以使用`E[attr1][attr2]`的方式来选择同时具有attr1和attr2属性的E元素。

* `E[attr='val']`，选择匹配具有attr的E属性，并且attr的值为val。(完全匹配)

  * val的值严格区分大小写。

* `E[attr*='val']`，选择匹配具有属性`attr`的E元素，且`attr`的属性值包含了val（任意位置）

* `E[attr^='val']`，选择匹配的E元素，E元素定义了属性attr，属性的值需要以val开头。

* `E[attr$='val']`，选择匹配的E元素，E元素定义了属性attr，属性的值需要以val结尾。



#### 伪类选择器

* `E:first-child`，选择父元素的第一个子元素且元素为E的元素。

* `E:first-of-type`，选择父元素的第一个E元素。

* `E:last-child`

* `E:last-of-type`

* `E:nth-child(n)`，选择父元素的第n个子元素且元素为E的元素。

  n的值可以是数字、关键词、公式

  * 数字

  * 关键词

    even偶数

    odd奇数

  * 公式

    * n，相当于全选
    * `Mn`，n和上面的意思相同，M表示的是n的倍数。

* `E:nth-of-type(n)`，选择父元素的第n个出现的为E的子元素。



​	`*-child`，选择第几个并且第几个得是某个元素。

​	`*-of-type`，只选择你是第几个出现的某个元素。



* `E:focus`，选择匹配的E元素，且匹配的元素获得焦点的时候会被触发。
* `E:target`，选择匹配的E的所有元素，且匹配的元素被相关的URL指向。（锚点指向时生效）