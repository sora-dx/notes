通过ID

 document.getElementById("id");



  通过标签名

​        document.getElementsByTagName("tagname");

​        得到的是：HTMLCollection对象 类数组

​        因为获取的是一个集合而不是某一个DOM节点，所以我们需要通过下标获取到某一个节点才能操作



  通过类名获取(IE678不兼容)

​        document.getElementsByClassName("class")

​        得到的是：HTMLCollection对象 类数组

​        因为获取的是一个集合而不是某一个DOM节点，所以我们需要通过下标获取到某一个节点才能操作



selectors API:

​        HTML5提供两个新接口用来获取元素，可以使用css选择器的方式获取

​        document.querySelector("选择器") 无论选择器选择多少个元素，永远只获取第一个 单个

​        document.querySelectorAll("选择器");无论选择器选择多少个元素，永远获取的是一个nodeList对象，需要使用下标来获取具体元素



​    旧方法

​    **var** oBtn = document.getElementById('btn');

​    **var** oBox = document.getElementById('box');

​    **var** oBoxLis = oBox.getElementsByTagName("li");

​    

​      getElementsByTagName返回的是HTMLConllection对象

​      HTMLConllection是动态的，只要元素发生变化，这个对象的内容也会跟着变化

 

​    oBtn.onclick = **function** () {

​      **for** (**var** i = 0; i < oBoxLis.length; i++) {

​        *//创建一个li标签*

​        **var** newLi = document.createElement("li");

​        *//把创建的li插入到box的内部的最后边*

​        oBox.appendChild(newLi);

​      }

​    }

​    新方法

​    **var** oBtn = document.getElementById('btn');

​    **var** oBox = document.getElementById('box');

​    **var** oBoxLis = oBox.querySelectorAll("li");

​    

​      querySelectorAll返回的是nodeList对象

​      nodeList是静态的，无论将来元素发生怎样的变化，这个对象的内容永远不会改变

点击事件

​	click:左键单击

​      contextmenu: 右键单击

​      dblclick: 左键双击

键盘事件：

​        keydown:键盘按下

​        keyup: 键盘抬起

​        两种绑定：

​          \- 给可输入表单绑定

​          \- 直接给document绑定，然后再事件函数中操作被控制元素

表单事件

​        *input:当表单内容发生变化的时候触发*

​        *change:当表单内容发生变化并且失去焦点的时候触发*



滚动条事件:

- -绑定给某个有滚动条的元素scroll
    -绑定给系统滚动条（绑定给window或者document）

load事件（预加载）：

是当资源加载完成以后触发，绑定给img、audio等

window.onload:当节点全部加载完成，并且所有的资源也全部加载完成以后触发



offset系列

​        offsetWidth/offsetHeight：获取元素的border-box的宽度或高度

​        offsetLeft/offsetTop：获取元素边框外边缘 到 最近定位父级的边框内侧 的距离



​      client系列：

​        clientWidth/clientHeight: 获取元素的padding-box的宽度或高度

​        clientLeft/clientTop: 获取元素的做边框或者上边框的宽度



​      scroll系列：

​        scrollWidth/scrollHeight:获取元素的包含完整内容的宽度或高度

​        scrollLeft/scrollTop:获取或设置 元素的滚动条滚过去的距离



​      获取文档的高度（没有宽度）

​        document.documentElement.offsetHeight



​      获取窗口的高度

​        document.documentElement.clientHeight



​      获取系统滚动条的距离

​        document.documentElement.scrollTop

​        window.pageYOffset

​      

​      设置系统滚动条的位置

​        document.documentElement.scrollTop

​        window.scrollTo(x,y)







