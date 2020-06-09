
>异常的try-catch机制有助于我们更快的定位出错原因所在,此处简单说明下try-catch机制的用法.

```sw
// 定义一个错误的枚举，并遵循错误的协议
enum TestError:String,Error{
    case error1 = "错误1"
    case error2 = "错误2"
}

// 用throw进行抛出异常
func play(param:Int) throws -> String {
    if param < 0 {
        throw TestError.error1
    }else if param >= 0 && param <= 10{
        throw TestError.error2
    }
    
    print("正常执行")
    return "hello world"
}

// 捕获异常
do {
    let value =  try play(param: 10)
    print(value)
} catch TestError.error1 { // 捕获错误
    print(TestError.error1.rawValue)
} catch TestError.error2 {
    print(TestError.error2.rawValue)
}
defer { // 最后的收尾工作，无论是否error都会执行
    print("defer")
}
```