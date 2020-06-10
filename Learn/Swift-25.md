
# 泛型类型限定

我们前面了解过 [泛型](./Swift-17.md#泛型)

这里我们再简单了解一下泛型的类型限定，首先我们举个泛型的例子：

>这里我们可以看到，play的入参的类型为`Any`，无法使用Data的属性，这还是一个多肽的概念，我们在使用的时候需要将其[向下类型转换](./Swift-16.md#类型转换向上下、可选)

```sw
class Data{
    var name:String
    
    init(name:String) {
        self.name = name
    }
}

func play<T:Any>(param:T){
    let data = param as! Data
    print(data.name)
}

play(param: Data(name: "hello"))
```

所以我们引入了类型限定的概念，其实就是把Any改为目标类型（感觉有点多此一举）

```sw
func play<T:Data>(param:T){
    print(param.name)
}
```

# 协议限定(associatedtype)
从字面上来理解，就是相关类型。意思也就是被associatedtype关键字修饰的变量，相当于一个占位符，而不能表示具体的类型。具体的类型需要让实现的类来指定。

在实现中的转换很多时候并没有太多的意义，而且将责任扔给了运行时。好的做法是让编译的时候就确定类型，这种情况就可以用associatedtype。

```sw
class Data{
    var name:String
    
    init(name:String) {
        self.name = name
    }
}

protocol Test{
    associatedtype D
    func play(param:D)
}

class Student:Test{
    func play(param: Data) {
        print(param.name)
    }
}

var s = Student()
s.play(param: Data(name: "hello"))
```


