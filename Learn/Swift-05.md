# switch case

- Swift里的switch case语言不像OC，可以不用写break：
```sw
let a:Int! = 2
switch a {
case 1,2,3:
    print("case 1~3")
case 4,5:
    print("case 4~5")
default:
    print("case 其他")
}
// 输出: case 1~3
```

- Fallthrough 穿透：
>在大多数语言中，switch 语句块中，case 要紧跟 break，否则 case 之后的语句会顺序运行，而在 Swift 语言中，默认是不会执行下去的，switch 也会终止。如果你想在 Swift 中让 case 之后的语句会按顺序继续运行，则需要使用 fallthrough 语句。

    ```sw
    let value = (10,20)
    switch value {
    case let(a,b) where a < b:
        print("case 1: \(a),\(b)")
        fallthrough
    case let(10,b):
        print("case 2: \(b)")
    default:
        print("case 其他")
    }
    /*
    输出：
        case 1: 10,20
        case 2: 20
    */
    ```

# for in循环
- 可以利用区间运算符
```sw
for index in 0...5 {
    print(index)
}
//输出： 0 1 2 3 4 5
```

- stride函数：可变步长类型值的序列
  1. stride(from:to:by)，开区间处理，最后一个值严格小于最大值；
  2. stride(from:through:by)，闭区间处理，最后一个值小于或等于最大值；
  3. .reversed(): 反向

  ```sw
  for index in stride(from: 0, to: 10, by: 2) {
      print(index) 
  } // 0 2 4 6 8

  for index in stride(from: 0, through: 10, by: 2) {
      print(index)
  } // 0 2 4 6 8 10

  for index in stride(from: 0, to: 10, by: 2).reversed(){
      print(index)
  } // 8 6 4 2 0
  ```

# while 循环
- while循环没什么好说的
- Swift中的 `do while` 叫 `repeat while`
