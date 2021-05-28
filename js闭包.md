### 5.14晨测
- 谈一谈闭包
    闭包的条件：
        - 函数嵌套函数
        - 内部函数使用外部函数的变量
        - 调用外部函数

    闭包到底是什么：
        - 通俗的理解：函数内部嵌套的函数
        - 浏览器查看后理解：内部函数的Scopes中，包含引用外部函数变量的一个对象

    闭包的作用：
        - 延长了局部变量的生命周期
        - 在外部控制局部变量

    闭包的缺点：
        - 局部变量会长期驻留在内存中，可能会造成内存泄漏(IE9以下)

    解决闭包带来的缺点：
        - 减少使用闭包
        - 及时释放

- 创建一个 类，要求方法共享 并创建实例化对象
     function Student(name, sex) {
        this.name = name;
        this.sex = sex;
    }

    Student.prototype.do = function () {
        console.log('html5');
    }
    Student.prototype.eat = function () {
        console.log('jwy');
    }


    var s1 = new Student("laoyan", "nan");

- 公有私有静态特权概念
    - 公有属性和公有方法：
        是设置给实例化对象的属性和方法  

    - 私有属性和私有方法
        是因为一些逻辑，在构造函数中声明的变量或函数

    - 静态属性和方法
        是把构造函数当做对象，扩展的属性和方法

    - 特权方法
        如果直接设置给实例化对象的方法，被称作特权方法

- 分析new 并手写new
    - new做了什么？
        - 创建了一个对象，并把这个对象返回
        - 把构造函数的this指向这个创建的对象
        - 将这个对象的原型链修改，将隐式原型指向构造函数的显式原型
    - 手写new
        function myNew(constur) {
            //1.创建一个对象
            var obj = {};
            //2.调用构造函数，并把构造函数的this指向当前的对象
            var arg = Array.from(arguments).slice(1);
            //re就是函数调用后的返回值
            var re = constur.apply(obj, arg);
            //3.修改原型链，让obj的隐式原型指向构造函数的显式原型
            obj.__proto__ = constur.prototype;

            //4.返回对象之前，判断构造函数的返回值是基本类型还是对象类型
            //如果是对象类型，则直接返回构造函数的返回值，否则返回obj
            if (typeof re === "object" && re !== null || typeof re === 'function') {
                //如果是object类型 则直接返回re
                return re;
            }

            //如果不符合上边的条件，则返回obj对象
            return obj;
        }

        var p2 = myNew(Person, "xiaowang", 20);

- 手写深拷贝
    function deepClone(o) {
        //先判断o的类型是什么
        if (checkType(o) === "object") {
            //如果拷贝的是对象，则创建一个新对象
            var newObj = {};
        } else if (checkType(o) === "array") {
            //如果拷贝的是数组，则创建一个新数组
            var newObj = [];
        } else {
            // 如果是其他类型，则可以直接赋值，不需要拷贝
            return o;
        }

        //开始拷贝
        for (var key in o) {
            newObj[key] = deepClone(o[key])
        }

        return newObj;

    }

    var re = deepClone(obj);

- 作业提交地址
https://wss.pet/s/5f2kosss12m 复制链接到浏览器打开
