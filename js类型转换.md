### 4.20晨测
- js的构成
    - ECMAScript:js基础语法
    - DOM：文档对象模型，控制页面的元素
    - BOM：浏览器对象模型，控制浏览器

- number类型的值    
    1. 数字直接量 a = 1
    2. 二进制 0b111
    3. 八进制 0o100
    4. 十六进制 0xff
    5. 科学计数法 1.23E+10
    6. 无穷 Infinity：无穷大  -Infinity：无穷小
    7. NaN（not a number）当强制将一些无法转为数字的类型转换数字的时候，直接变为NaN

- 其他类型转boolean
        - 使用Boolean()方法可以进行转换布尔值
        1.number转boolean
            - 非0为true  0为false
            - NaN为false

        2.string转boolean
            - 空为false 非空为true
        
        3.undefined和null 都 为 false

        4.object转boolean 都为true

- 其他类型转number
    - 使用Number方法转数字

    - 字符串转数字  
        - 能转就转 不能转就是NaN 空的和空白字符的就是0

    - boolean转数字
        true为1 false为0

    - null和undefined 转数字
        null是0  undefined是NaN

    - 对象转数字
        - 空数组是0 ，只有一位的数组，把这一位转数字
        - 其他全部是NaN


- 逗号运算符：
    1.一条语句执行多个操作
    2.一条语句先执行逗号左侧，再执行逗号右侧，最后整条语句返回逗号右侧的值


- 赋值运算符
    - = :把等号右侧的值赋值给等号左侧的变量
    - 可以连续赋值
    - 赋值运算符 返回等号右侧的值


- 加减乘除求模规则
    - 减乘除求模：所有全部转为number运算
    - 加法：只要两个操作数出现有一个字符串，则都转为字符串方式拼接；只要出现对象，则转为字符串拼接


作业提交地址：
https://wss.pet/s/587wxxyd960 复制链接到浏览器打开


    