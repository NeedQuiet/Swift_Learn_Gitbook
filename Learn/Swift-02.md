# 类型别名
`typealias`:给类型起一个别名，例如：

```swift
typealias dog = Int //定义一个名称为dog的Int类型
var a:dog = 10 //实际上a还是Int型
```

# 类型转换
类型() 和 ?? 语法

- 类型()，例如String()

  ```swift
  var a = 10
  var b = String(a) // 将Int型的a 转为 String型的b
  ```

- ?? 语法：空合运算符
>let username = loginName ?? "Guest" <br>loginName 表示为可选性，如果loginName 为空，则使用默认名称 Guest

  ```swift
  var a = "asd"
  print(Int(a) ?? 100) //很显然a转不了Int，如果转失败就会去取 ??后面的100
  ```

# 可选类型
Swift 的可选（Optional）类型，用于处理值缺失的情况。可选表示"那儿有一个值，并且它等于 x "或者"那儿没有值"。

Swift里，直接给变量赋值为nil是不可以的
```swift
var a = nil // 这样会报错
```

正确的做法是:
```swift
var a:Int? = nil // 一个Int类型的空值

var b: String? // 声明b，为String类型，可以为nil
b = nil
```

# 强制解析
当你确定可选类型确实包含值之后，你可以在可选的名字后面加一个感叹号（!）来获取值。这个感叹号表示"我知道这个可选有值，请使用它。"这被称为可选值的强制解析（forced unwrapping）。

```swift
var myString:String?
myString = "Hello, Swift!"
if myString != nil {
   // 强制解析
   print( myString! )
}else{
   print("myString 值为 nil")
}
```

执行结果为：

```sw
Hello, Swift!
```

# 元组类型
其实就是数组。只不过OC里是 `[]`，而swift里是 `()`。
取值是直接用 `.索引`，不像OC里 `[索引]`
```sw
var a = (1,2,3,"asdasd",true)
var b:(Int,String) = (10,"test")
print(a,b,a.0,b.1) // (1, 2, 3, "asdasd", true) (10, "test") 1 test
```

也可以给元素命名，类似字典
```sw
var c = (name1:"ttttt",name2:"xxxxx")
print(c.name1,c.name2) // ttttt xxxxx
```

也可以给value规定类型
```sw
var b:(name1:Int,name2:String) = (10,"test")
print(b) // (name1: 10, name2: "test")
```