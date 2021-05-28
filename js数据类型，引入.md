### 晨测
- js外部引入方式（画图）
    默认情况：碰到js先下载并立马执行

    defer：(异步+延迟)碰到js 可以进行异步下载（不停止解析html），等待html全部解析完成，才执行js
        ：如果加载多个js，最后还是按照js书写顺序执行（保证顺序）

    async：(异步)碰到js 异步下载，js下载完成后立马执行
        ：因为下载完立马执行，js大小不一，所以可能不能按照书写顺序执行js

- 标识符
    标识符：指的是变量、函数名、属性名、函数的参数的名字
    命名规范：
        - 以字母 $ _ 为开头  
        - 后边可以是 数字 字母
        - 不能出现空格
        - 区分大小写  a和A不是同一个变量
        - 不能用关键字和保留字

- 数据类型
    检测数据类型：
        typeof:检测一个数据的类型 并返回
        typeof(数据)  或者  typeof 数据

    typeof可以检测出的值有：
        - typeof检测并不能完全正确检测出结果
        - typeof可以得到的值：number string boolean undefined object function
        - typeof可以正确检测的类型：number string boolean undefined

    js数据类型：
        - 5种基本类型：number string boolean undefined null
        - 1种复杂类型：object（数组 对象 函数）

- 谈一谈undefined
    - Undefined类型只有一个值 是  undefined
    - undefined代表未定义，一般我们不会设置一个值为undefined，而是一种错误的结果undefined

    - 出现的场景：
        - 声明变量没有赋值 当使用的变量的时候，这个变量是undefined
        - 函数需要参数，但是调用函数没有传参的时候，返回undefined
        - 获取对象属性值，但是没有这个属性的时候，返回undefined
        - 当函数没有返回值的之后，返回的是undefined

- 谈一谈null
    Null类型：
        Null类型：只有一个值 是null
        代表空的意思

    出现的场景：
        - 当现在需要定义一个变量，但是未来才赋值的时候，可以把变量的值设置为null
        - 当函数需要参数，但是不想传递的时候，可以传递一个null
        - 把一个对象变成垃圾对象，可以将变量赋值为null
        - 原型链终点是null


作业提交地址：
    https://wss.pet/s/57xnlr3qcfi 
                

    