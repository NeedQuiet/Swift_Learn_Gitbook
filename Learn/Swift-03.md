
>基本的运算符和OC等其他语言雷同，就不做介绍了

# 空合运算符

?? 语法：空合运算符
>let username = loginName ?? "Guest" <br>loginName 表示为可选性，如果loginName 为空，则使用默认名称 Guest

  ```swift
  var a = "asd"
  print(Int(a) ?? 100) //很显然a转不了Int，如果转失败就会去取 ??后面的100

  // ?? 等同于精简了以下判断
  print(Int(a) != nil ? Int(a)! : 100)

  // 也等同于：
  if(Int(a) == nil){
    print(100)
  }else{
    print(Int(a)!)
  }
  ```

# 强制解析

！语法：

>当你确定可选类型确实包含值之后，你可以在可选的名字后面加一个感叹号（!）来获取值。这个感叹号表示"我知道这个可选有值，请使用它。"这被称为可选值的强制解析（forced unwrapping）。

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

# 区间运算符

```sw
var a = 1...4
print("范围 = \(a)")

var b = 1..<4
print("范围 = \(b)")

var c = -3..<4
print("范围 = \(c)")

/*
输出：
    范围 = 1...4
    范围 = 1..<4
    范围 = -3..<4
*/
```