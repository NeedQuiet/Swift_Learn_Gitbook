# 普通初始化器

```sw
class Test{
    var name:String
    
    init(name:String) {
        self.name = name
    }
}
```

# 可失败初始化器

```sw
class Test{
    var name:String
    
    init?(name:String) {
        if name == "unknow" {
            return nil
        }
        self.name = name
    }
}

var t:Test? = Test(name: "unknow")

if let P = t {
    print(P.name)
}else{
    print("初始化失败")
}
// 输出： 初始化失败
```

# 必要初始化器(required)

>required 关键字 ,强制子类也进行初始化

```sw
class Test{
    var name:String
    
    required init(name:String) {
        self.name = name
    }
}

class T:Test{
    required init(name: String) {
        super.init(name: name)
    }
}

var t = T(name: "hello")
print(t.name) // hello
```

# 结构体成员初始化器

>结构体中可以省略初始化器，结构体会自动根据成员列表生成初始化器

```sw
struct Test{
    var name:String
    
//    init(name:String) {
//        self.name = name
//    }
}

var t = Test(name: "hello")
```

# 闭包设置属性初始值

详细的可以参考： [Swift 闭包](https://www.runoob.com/swift/swift-closures.html)

```sw
class Test{
    var name:String = {return "swift"}()
    var age:Int = {
        var a = 10
        var b = 20
        return a + b
    }()
}

var t = Test()
print(t.name,t.age)
// 输出： swift 30
```