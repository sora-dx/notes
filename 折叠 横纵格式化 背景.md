#### 外边折叠

* 情况一： 盒子的底部margin和下一个兄弟的顶部margin，会产生外边距折叠。

  块状元素的上、下外边距会折叠。折叠的时候谁大用谁。

  解决方法：设置第一个元素`display:inline-block`或直接设置某一边的`margin`。

* 情况二：父盒子和子盒子之间的margin。

  ![2021-04-01_091907](2021-04-01_091907.png)

  产生的原因：margin之间直接接触了，没有阻隔。

  解决方法：父元素设置边框、内边距。或者父元素设置`overflow:hidden;`

  浏览器产生折叠的原因：就是为了页面排版美观。



#### 行内元素的外边距

* 行内元素上设置上、下外边距对行高没有影响。
* 行内元素上设置左、右外边距对内容是有影响的。
* 行内块状元素的上、下、左、右外边距都可以正常使用。



#### 横向格式化

![20210302065733455_10097](20210302065733455_10097.png)

* 默认情况下普通文档块级框各个组成的横向尺寸始终等于容纳块的宽度。

  容纳块：离的最近的块级元素。

  容纳块宽度=子元素的margin-left + 子元素的border-left + 子元素的padding-left + 子元素的width + 子元素的padding-right + 子元素的border-right + 子元素的margin-right

  上面的7个属性中只有子元素的width、子元素的margin-left、子元素的margin-right可以设置为auto。其他的属性只能设置具体指或使用默认值（默认值为0）

* 情况一：width、margin-left、margin-right，其中两个设置为具体指，一个为auto。

  这种情况下设置为auto的值的那个属性必须满足上面所说的公式，auto理解为补全总和所缺的尺寸。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body{
              margin:0;
          }
          #f{
              width:300px;
              height:300px;
              border:1px solid green;
          }

          #z{
              /* 300 - 100 - 10 -2  */
              width:100px;
              height:100px;
              margin-left:10px;
              margin-right: auto;

              border:1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
      </div>
  </body>

  </html>
  ```

  width、margin-left、margin-right，其中margin-left和margin-right都设置为具体的值，width的值为auto，这种情况下auto的值也需要满足上面所说的公式，宽度会被自动拉开。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {

              width: auto;
              height: 100px;
              margin-left: 10px;
              margin-right: 20px;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
      </div>
  </body>

  </html>
  ```

* 情况二：width、margin-left、margin-right其中两个为auto。

  * 如果margin-left和margin-right都为auto，那么两个外边距相等，元素在父元素中间显示。

    ```html
    <!DOCTYPE html>
    <html>

    <head>
        <title></title>
        <style>
            body {
                margin: 0;
            }

            #f {
                width: 300px;
                height: 300px;
                border: 1px solid green;
            }

            #z {
                /*
                
                (300-100-1-1 ) / 2
                */
                width:100px;
                height: 100px;
                margin-left: auto;
                margin-right: auto;

                border: 1px solid blue;
            }
        </style>
    </head>

    <body>
        <div id="f">
            <div id="z"></div>
        </div>
    </body>

    </html>
    ```

  * 将某一外边距和width设置为auto时。外边距为auto的那个值等于0。width被设置为填满容纳块所需要的值。

    ```html
    <!DOCTYPE html>
    <html>

    <head>
        <title></title>
        <style>
            body {
                margin: 0;
            }

            #f {
                width: 300px;
                height: 300px;
                border: 1px solid green;
            }

            #z {
                width:auto;
                height: 100px;
                margin-left: auto;
                margin-right: 10px;

                border: 1px solid blue;
            }
        </style>
    </head>

    <body>
        <div id="f">
            <div id="z"></div>
        </div>
    </body>

    </html>
    ```

* 情况三：如果三个属性都设置为auto，那么两边的外边距为0，width要多宽有多宽。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {
              width:auto;
              height: 100px;
              margin-left: auto;
              margin-right: auto;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
      </div>
  </body>

  </html>
  ```

* 情况四：width、margin-left、margin-right，三个都设置为具体的值。这种情况叫过渡约束。这种情况下margin-right右边距看不到效果（右边没有其他内容）

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {
              width:100px;
              height: 100px;
              margin-left: 10px;
              margin-right: 20px;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
      </div>
  </body>

  </html>
  ```

#### 纵向格式化

块状元素的内容决定元素的默认高度。

容纳块高度公式：容纳块高度（height） = 子元素margin-top + 子元素border-top + 子元素padding-top + 子元素height + 子元素padding-bottom + 子元素border-bottom + 子元素margin-bottom

height和上、下外边距可以设置为auto。

* 块级框的margin-top或margin-bottom设置为auto时，自动计算为0。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {
              width:100px;
              height: 100px;

              margin-top:auto;
              margin-bottom:auto;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
      </div>
  </body>

  </html>
  ```

* 块级框的margin-top、margin-bottom、都设置为具体的值，height的值为auto，高度不会被自动拉开。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {
              width:100px;
              height: auto;

              margin-top:10px;
              margin-bottom:10px;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
      </div>
  </body>

  </html>
  ```

* 某一边和height为auto时，为auto的那边外边距等于0。height被设置为内容高度。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {
              width:100px;
              height: auto;

              margin-top:auto;
              margin-bottom:10px;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z">1234</div>
      </div>
  </body>

  </html>
  ```

* height、margin-top、margin-bottom都设置为具体的值。

  ```html
  <!DOCTYPE html>
  <html>

  <head>
      <title></title>
      <style>
          body {
              margin: 0;
          }

          #f {
              width: 300px;
              height: 300px;
              border: 1px solid green;
          }

          #z {
              width:100px;
              height: 100px;

              margin-top:100px;
              margin-bottom:10px;

              border: 1px solid blue;
          }
      </style>
  </head>

  <body>
      <div id="f">
          <div id="z"></div>
          <span>1111</span>
      </div>
  </body>

  </html>
  ```

#### 调整宽度和高度的计算方式

默认情况下，块级框的宽度等于内容区的宽度，高度等于内容区的高度。我们可以使用`box-sizing`来进行调整。

格式： `box-sizing:value`

* content-box，默认值，内容区域宽等于width，高等于height，内边距和边框都在这个尺寸的基础上进行增加。(w3c盒子模型的计算方式)
* border-box，宽度、高度等于内容区+内边距+边框，相应的内容区将会被缩小。（IE盒子模型，怪异盒子模型）

#### 背景色

`background-color:value`

* transparent，透明。元素的默认背景色是透明的（包括HTML和body标签的）

  1. body和html都不是整个页面，body是由内容撑开，html由body撑开。
  2. 为什么我将背景色同时应用在body和html上面那整个页面都发生了修改。
     1. 整个层次`body -》 html -》 页面画布`
     2. 最终整体的背景颜色由页面画布决定（所有的内容都在页面画布上渲染出来）
     3. 最终画布颜色的决定规则：有html的颜色就用html的，如果没有就找body的，如果还没有使用画布本身的颜色透明（最终  页面的背景颜色由浏览器自己决定，但是大多数浏览器都比较人性化都会将背景色设置为白色。）

  可以给图片设置背景颜色，但是加上内边距才能显示出来，因为图片的内容区域就是图片本身。

  __背景从内容区开始经过内边距、边框一直延伸到边框的外边界。__



#### 背景图

格式：`background-image:value`

* none，没有背景图
* `url(url)`，设置背景图像的URL地址。

背景图和我们元素的大小没有直接的关系：如果背景图比元素大那么就显示一部分，如果比元素小那么就开始平铺。

通常我们可以让盒子大小和背景图大小相同。

#### 背景重复方式

格式： `background-repeat:value`

* repeat，默认值，横向、纵向平铺。
* `repeat-x`，横向平铺
* `repeat-y`，纵向平铺
* `no-repeat`，不平铺。

#### 背景定位

格式：`background-position:value`

* 关键字

  * left
  * right
  * top
  * bottom
  * center

  关键字通常使用两个值：第一个指定横向的位置，第二个指定纵向的位置。如果只写了一个关键字，那么另外一个假定是center。

  如果你指定两个横向的关键字或两个纵向关键字那么整个值将会被忽略。

* px，像素

  相对于元素内边距的外边界来进行定位（是左上角）



精灵图（雪碧图，CSS Sprites），是一种网页图片的应用处理方式，允许将一个页面中很多零星的小图片包含到一张大图里面去，当页面访问的时候就不会一张一张的请求显示图片。



优点：当今的网速越来越快，下载一张大图和小图所需的时间差不多，但是服务器的请求连接数是有限制的，此时为了减少对服务器的压力，提升网页的加载速度，我们将一张张小图拼接在一张大图里，一次下载。



#### 图标字体

图标字体也是一种字体，就像宋体、微软雅黑。

阿里巴巴矢量字体库。`https://www.iconfont.cn/`



使用步骤： 

1. 定义图标字体。

   让浏览器可以从web服务器上下载字体，这样就意味着不比依赖用户机器中的字体确保用户可以看到CSS中设定的字体。

   ```css
   @font-face {
     font-family: 'iconfont';//定义了一个字体的名字。
     src: url('iconfont.eot');//引入的字体的资源地址。
     src: url('iconfont.eot?#iefix') format('embedded-opentype'),
         url('iconfont.woff2') format('woff2'),
         url('iconfont.woff') format('woff'),
         url('iconfont.ttf') format('truetype'),
         url('iconfont.svg#iconfont') format('svg');
   }
   ```

2. 使用图标字体

   ```css
   .iconfont {
     font-family: "iconfont" !important;
     font-size: 16px;
     font-style: normal;
     -webkit-font-smoothing: antialiased;//CSS3中的属性让字体抗锯齿，让字体看起来更加清晰。
     -moz-osx-font-smoothing: grayscale;
   }
   ```

3. 挑选对应图标并且获取字体编码，应用到页面中。 

   `<span class="iconfont">&#x33;</span>`



#### 厂商前缀（供应商前缀）

如果在源码中发现类似`-webkit-`开头的代码，这种东西叫厂商前缀，浏览器厂商用它来标记实验性或者专属的一些属性。但是目前厂商前缀的使用趋势有所减缓。

* `-moz-`，火狐浏览器
* `-ms-`，微软
* `-o-`，欧朋
* `-webkit-`，chrome和safari。

#### 列表

#### 表格

