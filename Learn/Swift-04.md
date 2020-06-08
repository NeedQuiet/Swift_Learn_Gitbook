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

# 可选绑定

>使用可选绑定（optionals binding）来判断可选绑定是否包含值，如果包含就把赋值给一个临时的变量或常量。可选绑定可以用在if和while语句中来对可选类型值进行判断，并把值赋值给一个常量或者变量。

```sw
let a:Int? = 10
if let value = a {
    print("vlaue = \(value)")
}

// 输出：vlaue = 10
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

# 隐式展开
隐式解析可选类型（implicitly unwrapping  optionals）
>当可选类型被第一次赋值之后就可以确定之后一直有值的时候，隐式解析可选类型非常有用。一个隐式可选类型其实就是一个普通的可选类型，但是可以被当作非可选类型来使用，并不需要每次都使用解析来获取值，下面的例子展示可选类型String? 和隐式可选类型String!之间的区别

```sw
let A:String? = "可选类型"
let B:string! = A//需要感叹号（！）来获取值

let A! = "隐式解析可选类型"
let B:String = A//不需要感叹号
```

# 可选链展开
参考：[可选链展开](./Swift-22.md)
