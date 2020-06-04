# 属性计算(set/get)

以结构体为例：

```sw
struct Person{
    // private关键字代表私有
    private var _name = ""

    var name:String{
        // 可以这样写
//        set(param){
//            _name = param
//            print("set - " + param)
//        }

        // 或者省略param，用系统的newValue代替
        set{ // 如果不写set，那就是只读属性
            _name = newValue
            print("set - " + newValue)
        }
        get{
            print("get")
            return _name + " iOS"
        }
    }
    
}
var p = Person()
p.name = "swift" // set - swift
print(p.name)    // get / swift iOS
```

# 属性观察(willSet/didSet)

>跟OC里的KVO一样

可以不给willSet和didSet传值，有默认的值newValue/oldValue

```sw
struct Person{
    var name:String = "unknow"{
        // willSet(new_value)
        willSet
        {
            // print("wiilSet -" + new_value)
            print("wiilSet -" + newValue)
        }
        //didSet(old_value)
        didSet
        {
            // print("didSet -" + old_value)
            print("didSet -" + oldValue)
        }
    }

     // 也可以用 初始化器 设定初始值
     /**
     init(name:String) {
         self.name = name
     }
     */
}

var person = Person()
person.name = "hello"
person.name = "world"
/*
 输出：
     wiilSet -hello
     didSet -unknow
     wiilSet -world
     didSet -hello
 */
```
