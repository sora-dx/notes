### 5.15 晨测
- 谈一谈封装和多态
    封装：
        - 封装的目的是为了将信息隐藏，分为封装数据和封装实现
        - 封装数据：
            - 依赖作用域来实现封装数据的特性
        - 封装实现：
            - 就是隐藏实现的细节和设计的细节，我们不需要关心内部的实现，使用者只需要知道如何使用即可，封装让对象之前耦合变得松散，只需要通过暴露的API接口来通信

    多态：
        由于js本身就是动态的，所以天生支持多态
        多态：同一个操作作用域不同对象产生不同的结果

- 书写一个构造函数+原型的组合继承


- 谈一谈事件轮询机制 及画图表示
    代码分类：
        - 初始化代码（同步代码）：设置定时器、绑定事件，发送ajax等等
        - 回调执行代码（异步代码）：定时器回调函数，事件回调函数，ajax回调函数
    
    轮询机制：
        - 浏览器先执行同步代码 再执行异步代码
        - 在执行同步代码的时候，把异步代码交给浏览器的管理模块进行管理（事件管理模块、ajax管理模块，定时器管理模块）
        - 当异步代码的回调函数需要执行的时候，会把回调函数放在回调队列中等待执行
        - 当同步代码执行完毕之后，主线程会去回调队列中轮询，依次拿到回调函数执行

- 手写节流

- 手写防抖

- 谈一谈线程和进程
    线程和进程：
        进程：程序的一次执行, 它占有一片独有的内存空间
        线程：进程内的一个独立单元，CPU的基本调度单位

    特点：
        - 一个进程中一般至少有一个运行的线程: 主线程
        - 一个进程中也可以同时运行多个线程, 我们会说程序是多线程运行的
        - 一个进程内的数据可以供其中的多个线程直接共享
        - 多个进程之间的数据是不能直接共享的

- 作业提交地址
https://wss.pet/s/5fcs4ixlr54 复制链接到浏览器打开

