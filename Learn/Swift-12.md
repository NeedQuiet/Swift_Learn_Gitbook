
# 定义方式

- 基本方式：
```sw
enum TestEnum{
    case A
    case B
    case C
}
print(TestEnum.A) // A
```
或者：

  ```sw
  enum TestEnum{
      case A,B,C
  }

  print(TestEnum.B) // B
  ```

- 设置枚举值：
```sw
enum TestEnum:Int{
    case A = 1
    case B = 2
    case C = 3
}
print(TestEnum.A) // A
print(TestEnum.A.rawValue) // 1
```

- 枚举相关值

  ```sw
  enum TestEnum{
      case name(String)
      case age(Int)
      case xy(Int,Int)
  }

  func test(param:TestEnum){
      switch param {
      case TestEnum.name("hello"):
          print("已匹配")
      default:
          print("未匹配")
      }
  }

  print(TestEnum.name("ABC")) // name("ABC")
  print(TestEnum.xy(100, 200)) // xy(100, 200)
  test(param: TestEnum.name("test")) // 未匹配
  ```

- 注：

  <font color=red>在switf中只有类之间才可以用==来比较，而像枚举,结构体这样的值类型是不可以的，如果想用==，那需要自己重写相等协议Equatable，至于怎么重写，百度一下就知道了</font>

  ```sw
  func test(param:TestEnum){
      if param == TestEnum.name("hello") { // 这样写会报错，不能用 == 对比枚举
          print("已匹配")
      }else{
          print("未匹配")
      }
  }
  ```

# 遍历枚举

需要给枚举定义`CaseIterable`属性，然后就可以通过`allCases`属性拿到所有属性

```sw
enum TestEnum:CaseIterable{
    case A
    case B
    case C
}

for item in TestEnum.allCases {
    print(item)
}
// 输出 A B C
```