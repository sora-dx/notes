### 5.12 晨测
- 手写call(合理注释)
- 判断数据类型
    typeof:
        能够检测的类型：number boolean string undefined function symbol bigint

    ===:
        null 和 undefined
        因为null和undefined类型都是只有一个值，所以全等判断只要类型相等，则值一定相等
    
    obejct.toString():
        object的toString方法返回的字符串中拥有当前数据的类型，所以我们可以让其他类型调用object的toString方法进行检测

        Object.prototype.toString.call(value).slice(8, -1).toLowerCase();

- call\apply\bind 分析
    call:
        - 在Function的原型对象上有 call apply bind 三个方法，可以供所有的函数使用
        - 这三个方法是必须函数才能调用，存在意义是改变函数执行时的上下文，再具体一点就是改变函数运行时的this指向
        - call的作用：
            1.改变函数的this执向为自己的第一个参数
            2.调用了函数
        - call的第一个参数有3种情况：
            1.null和undefined：默认就会把this执行window
            2.基本包装类型：把this指向当前数据的包装对象
            3.对象类型：this直接指向该对象
        - call方法从第二个参数开始，依次都是给被调用函数传递的参数
    apply:
        和call类似
        区别：给函数传参的时候
            - call 是第二个参数开始依次传参
            - apply 是 把所有的参数放入一个数组中  然后传入apply的第二个参数
     bind:
        - 语法和call一样
        - bind也是改变函数的上下文this执行
        - bind并不会调用函数，而是返回了一个改变this指向后的函数

- 释放内存：
    - 函数调用以后，函数内部的数据会生成保存在内存中（局部变量和局部方法），当函数执行完成，函数的数据会自动销毁，内存会直接释放
    - 全局变量只有在页面的关闭的时候才能销毁，除非手动销毁
    - 把变量设置为null,当一个对象不再被引用的时候，就变成了垃圾对象，会等待回收

作业提交地址
https://wss.pet/s/5ei1s4tmsa0 复制链接到浏览器打开
