### 4.27晨测
- 谈一谈sort排序
    - 在原数组的基础上对数组的元素进行排序
    - 如果在调用sort的时候没有传入任何参数，则会按照字符串的格式对数组的元素进行排序

    - 如果想按照其他的顺序进行排序，就必须向sort方法中传入比较函数
    - 比较函数有两个参数，比较函数会进行比较这两个参数
    - sort内部
        - a是后边的值，b是前边的值
        - return的值只要是负数则交换顺序,如果是0或者正数则不交换

- 分析splice方法
    - 功能：删除、添加、替换
    - 参数1：删除开始的下标的位置
    - 参数2：从删除位置开始数，删除元素的长度 
    - 后边所有的参数：在删除位置添加的元素
    - 返回：删除的值组成的数组

- 谈一谈 every some filter forEach map方法
    - every方法：判断数组的元素是否全部满足条件，返回布尔值
    - some方法：判断数组的元素是否有满足条件的元素，返回布尔值
    - filter方法：筛选数组中所有符合条件的元素，组成数组返回
    - map方法：映射数组，遍历数组，对数组的每个值进行操作并，返回一个新数组
    - forEach方法：遍历数组

- forEach方法书写格式
    - forEach接收一个回调函数作为参数，数组的值会依次的进入函数执行
    - 回调函数接受三个参数
        - 参数1：当前进入函数的数组的元素
        - 参数2：当前进入函数的数组的元素的下标
        - 参数3：当前数组的引用
    - 案例：
        arr.forEach(function (item, index, array) {});

- 添加和删除数组的元素
    - 添加元素
        - push和unshift:向数组的末尾和头部添加一个或多个元素
        - concat  合并数组 把一个或多个值合并到数组的末尾
        - splice方法：给任意位置添加
    - 删除元素
        - shift和pop:删除数组的第一个和最后一个的值
        - delete删除:只能删除对应的value值，但是下标依然存在，数组的长度不变
        - splice删除：删除任意位置元素

作业提交地址：
https://wss.pet/s/5a7u1wdt630 复制链接到浏览器打开