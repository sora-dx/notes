#### 盒子模型的基本要素

- width：设置元素的宽度。
- height：设置元素的高度。
- background-color：设置背景颜色。
- border：用来设置边框。

#### 元素的显示模式

- 块级元素（block）

  - 独占一行，前面和后面都会有换行，多个块级元素各自新起一行。默认情况下 block 元素宽度自动填充满父元素宽度。
  - 块状元素可以设置宽度和高度，即使设置了宽度和高度，仍然是独占一行。
  - 人为设置自身的宽度的时，可以大于父元素的宽度也可以小于父元素的宽度

  常用的元素：div、h1~h6、p、ul、ol、li、dl、dt、dd、form

- 行内元素（inline）、内联元素

  - 不会独占一行，多个相邻的元素会在一行里面排列。直到一行排不下。
  - 行内元素设置宽度和高度无效。

  常用的元素：span、b、strong、i、em、u、ins、s、del

  行内元素就只是包裹文本的所以没有宽度。

- 行内块级元素(inline-block)

  在内部表现为块状元素，可以设置宽度、高度。外部的排列方式类似于行内元素也就是水平排列。

  常用的元素：img、表单元素

- 更改显示类型

  格式：`display:value`

  - block，显示为块状元素

  - inline，显示为内联元素

  - inline-block，显示为内联块状元素。

  - none，隐藏元素。

    问题解析：HTML 标签中、空格、换行都会当做一个空格来处理，所以行内元素中会有空白（也就是说当成了一行里面的内容了）

  ![2021-03-30_094233](2021-03-30_094233.png)

  ​ 解决方案：

  1. 在源码中将行内元素后面的回车都删除掉。让所有行内元素排在一行。

  2. 将父元素的 font-size 设置为 0px；

#### 文本缩进

格式： `text-indent:value`

* px，像素。
* em，相对于字体大小。

__注意：__

1. text-indent，不能用在行内元素上（块状元素和行内块状元素上面是可以使用的）。
2. 文本缩进时我不管你有多少行，只有第一行才会受到影响。



#### 换行

格式：`white-space:value`，用来处理元素内文本是否允许换行。

* nomral，默认值。`CJK文本`遇到容器边界自动换行，非CJK文本由word-break的值决定。

  CJK：china、japan、korea三国的缩写。

* nowrap，超出容器边界不换行。



我们在换行的时候有些英文单词因为太长所以不能马上换行。`work-break`

格式： `word-break:value`用来标明怎杨进行单词内的断句

* none，浏览器根据默认设置来决定是否换行。
* break-all，超出就会进行换行。
* keep-all，禁止进行换行。



#### 隐藏内容

格式：`overflow:value`

* `visible`，超出元素框的内容是可见的。
* `hidden`，超出元素框的内容被隐藏。
* `scroll`，超出的内容会出现滚动条。
* auto，浏览器自己决定。



#### 水平居中

`text-align:value`，水平对齐的方式。

* left，默认，文字放到左边。
* right，放到右边。
* center，放到中间。 

__注意： __

1. text-align能用于块状元素或行内块状元素（行内块状元素要有多余的空间）
2. text-align用来处理元素中的内容的对齐方式，对于自身没有影响。



#### 关于继承

刚才设置了a链接的颜色（单独设置的），为什么继承下来的颜色不好使。

继承下来的内容没有自身设置的优先级要高（即使是系统自带的也比继承下来的优先级高）

h标签和a标签

* h标签默认对字号进行了设置，所以会覆盖继承下来的字号。
* a标签默认对字体颜色进行了设置，所以会覆盖掉继承下来的颜色。



#### 内联盒子模型

![20210222122944164_1752](readmeimg/20210222122944164_1752.png)

块级元素中通常放置的是一行一行的内容（行内元素），内联盒子模型决定了一行一行的行内元素应该如何摆放。

![20210221190801060_16952](readmeimg/20210221190801060_16952.png)

上面的代码总共形成了3个内联盒子。

类型： 

* 如果内容被行内元素所包含则属于内联盒子（实线部分）。
* 如果内容没有被行内元素所包含，就是光秃秃的内容则属于匿名内联盒子（虚线部分）



内联盒子的组成： 

一个内联盒子由内容区域、上半行间距、下半行间距组成。![20210221224458925_9294](readmeimg/20210221224458925_9294.png)

1. 内容区

   ![20210221215526537_31510](readmeimg/20210221215526537_31510.png)

   `<span style="font-size:15px;">hello</span>`

   font-size与实际看到的字体大小的之间的具体关系由字体的设计者确定。`font-size`只不过确定了一个看不见的框的高度这个框就是字体框（字体框用来区分一个一个的字），它用来确定每个字的位置，这个字体框有可能比实际的字体高，也有可能比实际的字体矮。

   内容区是由元素中各个字的字符框连在一起构成的框。

   ![20210221220551441_11230](readmeimg/20210221220551441_11230.png)

   行内块状元素它的内容区域可以看做内联块状元素本身。

2. 上下半行间距

   行间距是该元素的`行高`（`line-height`）和`内容区域`的差。

   line-height - 内容区 = 行间距。

   半行距：在CSS中，行距分散在当前文字的上方和下方（上半行间距、下半行间距）即使是一行文字也有行距。

行框：每一行就是一个行框盒子，每个行框盒子由一个一个内联盒子组成。

每一行的行框盒子的顶边等于本行的最高内联盒子的上边界，行框的底边放在最低内联盒子的下边界。



#### 行高

line-height:如果放在块状元素上，表示的是每行（每个行框）的最矮的行框高度。

格式： `line-height:value`

value的值：

* normal，默认值，浏览器自己去计算。

* px，像素

* number，将数值作为行高度。根据当前的font-size大小来进行计算。

  `font-size:20px; line-height:1.5`

  `1.5* 20 = 30px;`

line-height是具有继承性的。



不设置块状元素高度的情况下，其line-height改变会撑高盒子，文字始终垂直居中与盒子，也就是该盒子的高度与行高是相同的（撑开盒子的是行高而不是内容）

```html
<!DOCTYPE html>
<html>

<head>
    <style>
        div {
            /* background-color: yellow; */
            border:1px solid green;
            line-height:5px;
        }
    </style>
</head>

<body>
    <div>
        我打算买手机，我媳妇不让我买。然后我就撒娇。
    </div>
</body>

</html>
```

当设置了块状元素的高度的情况下，其line-height改变只会将文字在垂直方向上的位置改变，盒子的高度不会改变。



当像让一个行文本垂直居中与当前元素时，行高等于元素的高度。（但是只是单行文本才会生效）。

多行文本不能让`line-height=height`



#### 内联盒子中内容区域的构造

![20210222003533136_27258](readmeimg/20210222003533136_27258.png)

* baseline（基线），基线是小写字母x的下边缘。为了排列整齐用的。而且他是其他线的根本。

  行内块状元素的基线就是元素的底部。

* x-height，表示该字体中x的高度。

* 中线，内容区域的1/2处的一条线。

* 上、下边线，内容区域的上边线和内容区域的下边线。



#### 垂直居中

格式：`vertical-align:value`

* baseline，默认值，基线对齐。

* bottom，内联盒子的底边与行框的底边对齐。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <style>
          #s1{
              font-size:32px;
              vertical-align: bottom;
          }
          #s2{
              font-size:108px;
          }
      </style>
  </head>

  <body>
      <span id="s1">x1</span>
      <span id="s2">x2</span>
  </body>

  </html>
  ```

* top，将内联盒子的顶边与行框的顶边对齐。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <style>
          #s1{
              font-size:32px;
              vertical-align: top;
          }
          #s2{
              font-size:108px;
          }
      </style>
  </head>

  <body>
      <span id="s1">x1</span>
      <span id="s2">x2</span>
  </body>

  </html>
  ```

* `middle`，元素的垂直中心点和父元素的x-height的1/2处对齐。

#### 垂直居中出现问题

1. 块状元素只包含一张图片时会有不知名的空白。

   ![2021-03-30_163258](2021-03-30_163258.png)

   __问题解析：__

   1. 在HTML5文档声明，行内元素的所有解析和渲染表现如同每个行框盒子前面有一个`空白节点`，这个节点透明，不占据任何宽度，也没有办法通过脚本获取。但是只在HTML5中并且使用`<!DOCTYPE htmL>`声明时才会有。
   2. 根据上面所说的`空白节点`就是在图片前面有一个看不到的内容。既然有内容那么默认就是采用vertical-algin:baseline对齐。图片是行内块状元素其基线是图片的底部，所以才会导致下面有一段空白。

   __解决方法： __

   * 方法一：图片块状化，没有基线，没有基线就没有基线对齐。

     ```html
     <!DOCTYPE html>
     <html>

     <head>
         <style>
             #pho{
                 border:1px solid green;
             }
             img{
                 display:block;
             }
         </style>
     </head>

     <body>
         <div id="pho">
             <img src="./img/Frederik-the-Great1.jpg" style="width:200px;height:200px;" />
         </div>
     </body>

     </html>
     ```

   * 方法二： 将图片改为底线对齐

     ```html
     <!DOCTYPE html>
     <html>

     <head>
         <style>
             #pho{
                 border:1px solid green;
             }
             img{
                 vertical-align: bottom;
             }
         </style>
     </head>

     <body>
         <div id="pho">
             <img src="./img/Frederik-the-Great1.jpg" style="width:200px;height:200px;" />
         </div>
     </body>

     </html>
     ```

   * 方法三： 将行高调的足够小。

     ```html
     <!DOCTYPE html>
     <html>

     <head>
         <style>
             #pho{
                 border:1px solid green;
                 line-height:10px;
             }

         </style>
     </head>

     <body>
         <div id="pho">
             <img src="./img/Frederik-the-Great1.jpg" style="width:200px;height:200px;" />
         </div>
     </body>

     </html>
     ```

   * 方法四：font-size设置为0。让乱七八糟的线都重叠。

     ```html
     <!DOCTYPE html>
     <html>

     <head>
         <style>
             #pho{
                 border:1px solid green;
                 font-size:0;
             }

         </style>
     </head>

     <body>
         <div id="pho">
             <img src="./img/Frederik-the-Great1.jpg" style="width:200px;height:200px;" />
         </div>
     </body>

     </html>
     ```


2. 莫名其妙的移动

   ```html
   <!DOCTYPE html>
   <html>

   <head>
       <style>
           #pho{
               width:500px;
               border:1px solid green;

           }
           img{
             	/*为什么给image设置vertical-middle时好像x-baseline这个文字向上移动了*/
               vertical-align: middle;
           }

       </style>
   </head>

   <body>
       <div id="pho">
           <img src="./img/Frederik-the-Great1.jpg" style="width:200px;height:200px;" />
           x-baseline
       </div>
   </body>

   </html>
   ```

   ​


扩展作业： 

1. 已知父元素宽度、高度时其中的图片要求水平、垂直居中。
2. 已知父元素宽度、高度时其中的多行文本要求水平、垂直居中。
3. 已知父元素宽度、高度时其中的多行文本和图片要求水平、垂直居中。