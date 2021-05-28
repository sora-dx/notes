### 5.7 晨测
- 谈一谈文本内容操作
    innerHTML:可以设置或获取元素的内容  设置的时候可以解析标签 获取的时候可以获取标签
    innerText:可以设置或获取元素的内容 设置的时候不能解析标签 获取的时候获取不到标签

    outerHTML:可以设置或获取元素的内容 和innerHTML类似 但是包含了当前的元素
    outerText:可以设置或获取元素的内容 和innerText类似 但是包含了当前的元素

    textContent:和innerText类似 如果没有标签的情况下 推荐使用textContext

- 自定义属性

    设置节点对象的属性：
        - 如果这个属性是标签自有的属性，则执行通过 ELE.XXX设置或获取，但是有的属性和关键字冲突了需要些许改变，比如class，需要写为className

    设置自定义属性：
       - 设置：setAttribute(key,value)
       - 获取：getAttribute(key)
       - 删除：removeAttribute(key)

    h5自定义属性
        - 每一个DOM节点都有一个dataset属性,dateset属性是一个对象，包含了当前DOM元素上所有的自定义属性
        - h5要求 自定义属性使用data-*前缀
        - 我们只需要操作dataset属性，即可操作元素的自定义属性

- 节点操作
    - 创建元素节点 document.createElement();
    -  插入节点：
        - A.appendChild(B)
        - A.insertBefore(new,old)
    - 复制节点 cloneNode()方法
    - 替换节点  A.replaceChild(new,old)
    - 删除元素 A.removeChild(B)  A.remove()
    
- 系列属性
    offset系列
        offsetWidth/offsetHeight：获取元素的border-box的宽度或高度
        offsetLeft/offsetTop：获取元素边框外边缘 到 最近定位父级的边框内侧 的距离

    client系列：
        clientWidth/clientHeight: 获取元素的padding-box的宽度或高度
        clientLeft/clientTop: 获取元素的做边框或者上边框的宽度

    scroll系列：
        scrollWidth/scrollHeight:获取元素的包含完整内容的宽度或高度
        scrollLeft/scrollTop:获取或设置 元素的滚动条滚过去的距离

    获取文档的高度（没有宽度）
        document.documentElement.offsetHeight

    获取窗口的高度
        document.documentElement.clientHeight

    获取系统滚动条的距离
        document.documentElement.scrollTop
        window.pageYOffset
    
    设置系统滚动条的位置
        document.documentElement.scrollTop
        window.scrollTo(x,y)

-  BOM：
    - window对象：
        - BOM的核心对象，代表浏览器窗口的一个实例
        - Global并没有在浏览器中实现，window扮演Global的角色（全局的方法和变量都是window对象的属性和方法）
    - navigator:客户端信息 有userAgent onLine等属性
    - history：历史记录 有forWard back go等方法
    - location：url地址信息 有href等属性  reload 等方法
    - document：文档

作业提交地址：
https://wss.pet/s/5d2jk2h73c8 复制链接到浏览器打开


​    