Schema

```js
let studentsSchema = new Schema({
      stu_id:{
        type:String,//字段类型
        required:true,//必填字段 
        unique:true//唯一（不可重复）字段
      },
      stu_name:{
        type:String,
        required:true,//必填字段
      },
      stu_age:{
        type:Number,
        required:true,//必填字段
      },
      stu_sex:{
        type:String,
        required:true,//必填字段
        default:'男'
      },
      stu_hobby:{
        type:Array,//[String]
      },
      stu_info:{
        type:Schema.Types.Mixed//能接收所有类型的数据
      },
      date:{
        type:Date,
        default:Date.now()//默认值是当前的时间
      },
      enable_flag:{
        type:String,
        default:'Y'
      }
  })
```



 -Create

	   模型对象.create(文档对象，回调函数)
 -Read

	   模型对象.find(查询条件[,投影],callback)不管有没有数据，都返回一个数组
	   模型对象.findOne(查询条件[,投影],callback)找到了返回一个对象，没找到返回null
 -Update

	  模型对象.updateOne(查询条件,要更新的内容[,配置对象],callback)
	  模型对象.updateMany(查询条件,要更新的内容[,配置对象],callback)
 -Delete

	   模型对象.deleteOne(查询条件,callback)
	   模型对象.deleteMany(查询条件,callback)
	   备注：没有delete方法，会报错！

备注： 以上所有方法，如果没有指定回调函数，则返回值是一个Promise对象
