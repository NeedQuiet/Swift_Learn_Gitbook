# 类型别名
`typealias`:给类型起一个别名，例如：

```swift
typealias dog = Int //定义一个名称为dog的Int类型
var a:dog = 10 //实际上a还是Int型
```

# 类型转换

类型()，例如String()

```swift
var a = 10
var b = String(a) // 将Int型的a 转为 String型的b
```

# 元组类型
类似数组。只不过数组里是 `[]`，而元组是 `()`。
取值是直接用 `.索引`，不像数组 `[索引]`
```sw
var a = (1,2,3,"asdasd",true)
var b:(Int,String) = (10,"test")
print(a,b,a.0,b.1) // (1, 2, 3, "asdasd", true) (10, "test") 1 test
```

也可以给元素命名，类似字典:
```sw
var c = (name1:"ttttt",name2:"xxxxx")
print(c.name1,c.name2) // ttttt xxxxx
```

也可以给value规定类型:
```sw
var b:(name1:Int,name2:String) = (10,"test")
print(b) // (name1: 10, name2: "test")
```

通过 `_` 忽略:
```sw
let (_ ,_, name1) = ("1","2","3");
print(name1)
```

# 函数类型

参考[10.函数-函数类型](./Swift-10.md#函数类型)