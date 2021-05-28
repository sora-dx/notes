#### td中的两个属性

* colspan：规定单元格横跨的列数。
* rowspan：规定单元格竖跨的行数。



![W20210216095704642_23012](img/20210216095704642_23012.png)

![20210216095652306_26682](img/20210216095652306_26682.png)



#### 内框架

`<iframe>`标签，创建包含另外一个文档的框架。

格式：`<iframe></iframe>`

* src属性：载入框架时要载入的文档的地址。
* frameborder属性：是否显示边框，设置为0时不显示。
* width、height设置框架的宽度和高度。
* name属性：给这个iframe起个名字，可以配合a标签的target属性使用。

`a`的`target`属性也可以用`_parent`指的是在父窗口打开，还可以是`_top`。

![20210216185925113_24386](Z:/vShare/20210216185925113_24386.png)

#### 表单

* `<form>`标签告诉浏览器这个双标签中包含的内容是表单的内容。

  * action属性：提交数据提交到哪里，里面写的是你要提交的地址。

  * method属性：指定提交的方法，默认值是get，你可以改为post。get的方式是使用查询字符串在URL上面传值。POST的方式会将值和URL分开传输。

    ​

* `<input />`标签：定义输入框

  * type属性：定义输入框的类型（根据type的值是多少配合使用其他属性）

    * `text`值：表示一个文本输入框。

      * `name`属性：表示该文本框传递到服务器上的标识。

      * `value`属性：默认值。

      * `maxlength`属性：输入的最大字符。

      * `disabled`属性：表示禁用此输入框。完整格式：`disabled="disabled"`

      * `readonly`属性：只读。完整格式：`readonly="readonly"`

        只读和禁用的区别在于禁用的值不会传递到服务器，只读的值会传递到服务器。

    * `password`值：表示一个密码框。

      * `name`属性，表示该密码框传递到服务器上的标识。

      __注意：__ 提交密码框的值时使用的是明文提交。

    * `submit`值：表示一个提交按钮。

      * `value`属性：更改按钮显示的值。

    ![20210216111413434_27255](img/20210216111413434_27255.png)

    * radio值：表示一个单选框，只能选择一个。

      * name属性：该单选框传递到服务器上的标识。（也用来进行分组）
      * value属性：选中后传递到服务器上的值。
      * `checked`属性：默认选中该单选框，可以写为`checked="checked"`也可以写为`checked`

      __注意： __

      1. 同一组的多个单选框中他们的name的值必须相同，否则不会出现单选效果。

    * `checkbox`值：复选框，多选框，可以选择多个。

      * name属性：传递到服务器上的标识。
      * value属性：每个选项的值。
      * checked属性：默认选中该多选框，可以写为`checked="checked"`也可以写为`checked`

      __注意：__

      1. 因为用户不能输入所以我们需要使用value属性给这个多选框指定一个值。
      2. checked可以有多个。

    * file值： 上传框

      * `multiple`属性：加上该属性之后可以通过按住ctrl键一次选择多个文件。

    * reset值：重置(不用)


#### `<label>`标签：用来为`<input/>`标签定义标注

* for属性：用来和input进行绑定，值要和input输入框的id的值相同。



#### `<select>`标签：定义一个下拉列表@@@@

* name属性：给下拉列表定义名字。
* disabled属性：禁用整个下拉列表`disabled="disabled"`

#### `<option>`标签：定义下拉列表中的每一项@@@@

* value属性：给服务器的值。
* disabled属性：禁用该option选项。`disabled="disabled"`
* selected属性：默认选中。`selected="selected"`

#### `<optgroup>`对option进行分组。

* label属性：说明这个分组的描述。
* disbaled，禁用整个分组。

#### 多选

* multiple属性：是否可以多选。
* size属性：用来控制显示多少个。

#### `文本域`

`<textarea>`标签：用来输入大段的文字。

* name属性：传输的标识。

如果是简短的文字没有换行你就用`input type="text"`如果是大段的文字你就用textarea。

`textarea`中间包含的内容会作为默认值存在(包括其中的空格也是一样)。



#### button标签：用来表示一个按钮

* type属性：button、submit、reset

type属性的默认值在每个浏览器中不同，有些浏览器中是submit有些是button。



![2021-03-27_160423](2021-03-27_160423.png)

```html
http://localhost/0323/03/10.html?email=1111&passwd=222&rePasswd=222&upload=captura.exe&sex=1&hobby=ds&hobby=dy&country=j
```

