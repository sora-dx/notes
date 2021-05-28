鼠标事件：

​	*click:左键单击*

​      *contextmenu: 右键单击*

​      *dblclick: 左键双击*

​      *mousedown:鼠标按下事件*

​      *mouseup:鼠标抬起事件*

​      *mousemove:鼠标移动事件*

​      *mouseover:鼠标移入事件(会触发冒泡)*

​      *mouseout:鼠标移出事件(会触发冒泡)*

​      *mouseenter:鼠标移入事件*

​      *mouseleave:鼠标移出事件*

​	  oncontextmenu：右键默认事件

键盘事件：

​	onkeydown： 键盘事件

​	event 事件对象有一个keyCode属性，代表当前的键码*

销毁事件   
1.DOM0的销毁方式
    将事件属性赋值为null即可

2.DOM2的销毁方式
    使用 removeEventListener()
    - 参数1：事件名
    - 参数2：哪一个事件函数

阻止传播和阻止默认事件
阻止传播：e.stopPropagation();
阻止默认事件：e.preventDefault();  或  return false

​	event事件对象的鼠标位置
​	clientX: 获取事件发生的时候 鼠标 到 窗口边缘的 距离

​	offsetX: 获取事件发生的时候 鼠标 到 目标元素 的距离

​	pageX: 获取事件发生的时候 鼠标 到 文档边缘的 距离

​	screenX: 获取事件发生的时候，鼠标 到 屏幕边缘 的距离

