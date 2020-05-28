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
