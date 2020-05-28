#查看Swift版本
终端命令查看当前Swift版本:
```shell
xcrun swift -version
```

输出：

```shell
Apple Swift version 5.2.4 (swiftlang-1103.0.32.9 clang-1103.0.32.53)
Target: x86_64-apple-darwin19.4.0
```


#数据类型
常用的数据类型有 `Int`、`Float`、`Double`、`Bool`、`Character`、`String`、 
```swift
var a:Int = 10 //整形
var b:Float = 1.2 //浮点型（单精度）
var c:Double = 1.5 ////浮点型（双精度）
var d:Bool = true //Bool类型
var e:Character = "e" //字符
var f:String = "Hello, playground" //字符串
```

#变量、常量
- 变量：var

```swift
var a:Int = 10
```

- 常量：let

```swift
let a:Int = 10
```

#类型推断
定义变量/常量时，如果不声明数据类型，那么系统会自动根据其值**`推断`**其数据类型
```swift
var a = "Hello world" //String
// 如果这时给a赋值Int 则会报错：
a = 10 // Cannot assign value of type 'Int' to type 'String'
```

#判断数据类型

```swift
type(of: myStr) // String.Type
```

#输出语句

```swift
print(items: Any...)
print(a,b)
```

#拼接字符串
String和String拼接可以直接用 `+` 号；String和其他类型拼接可以用 `"\(obj)"`
```swift
var a = "Hello "
var b = "world"
let c = 10
let c1 = 11
let d = a + b // "Hello world"
let e = d + " test \(c) \(c1)" // "Hello world test 10 11"
```

#注释
```swift
// 单行注释
/*
    多行注释
*/
```
