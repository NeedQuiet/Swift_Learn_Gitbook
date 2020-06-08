# 函数定义
- 无参，无返

  ```sw
  func test(){
      print("test")
  }

  func test2() -> Void {
      print("test2")
  }
  ```

- 无参，有返

  ```sw
  func testInt() -> Int {
      return 100
  }
  ```

- 有参，无返

  ```sw
  // ... 代表可变参数，可以输入多个值
  func test4(name:String...){
      print(type(of: name))
  }
  test4(name: "a","b") // Array<String>
  ```

- 有参，有返

  ```sw
  //示例1：
  func test3(name:String) -> String{
      return name
  }

  //示例2：
  func test5(name:(n1:String,n2:Int)) -> (String,Int){ // 参数为元组，返回值为元组
      var value:(a:String,b:Int)
      value.a = name.n1 + " world"
      value.b = name.n2 + 10
      return value
  }
  var value = test5(name: ("hello",100))
  print(value) // ("hello world", 110)
  // 或者
  var value2:(c:String,d:Int) = test5(name: ("hello",100))
  print(value2.c,value2.d)// hello world 110
  ```

# 关于参数名称

同一个参数实际上是有2个名称的

//专业定义 outName：函数时机参数标签(实参),inName:形式参数名(形参)
//个人理解就是 外部调用名和内部使用名

```sw
func test(outName inName:String){
    print(inName)
}
test(outName: "testStr")

// 外部名称可以忽略
func test2(_ inName:String){
    print(inName)
}
test2("test2Str")
```

# assert断言
用来停止程序的
```sw
assert(false,"停止继续运行")
```

# inout关键字
inout关键字会将`值传递`改变为`指针/地址传递`
```sw
func test(param: inout Int){
    param = param * 2 // 使用inout才能直接对入参进行值操作
    print(param) // 20
}

var a = 10;

print("传递前a = " + String(a)) // 传递前a = 10

test(param: &a)

print("传递后a = " + String(a)) // 传递后a = 20
```

# 函数类型

- 定义

  ```sw
  var a:() -> Void
  var b:(Int,String) -> String
  let c:([Int]) -> (Int,String)
  ```

- 使用
  
  1. 常规调用
   
     ```sw
     // 函数test1
     func test1() -> Void{
     }

     // 定义函数a，并将函数test1赋给a
     var a:() -> Void = test1

     //调用
     a()
     ```

     或(有返回值)

     ```sw
     func test(param1:String,param2:Int) -> String {
     return param1 + String(param2)
     }
     var c:(String,Int) -> String = test
     print(c("hello",10))
     ```

  2. 匿名函数调用
   
    ```sw
    var b:()->Void = {()->Void in
    print("匿名函数")
    }
    b() 
    ```

    或者(带参数带返回值)

     ```sw
     var f:([Int]) -> String = { (array:[Int]) -> String in
         var temp:String = ""
         for item in array {
             temp = temp + String(item)
         }
         return temp
     }

     print(f([1,2,3])) // 123
     ```

# 函数作为参数

>函数类型作为函数的参数类型

- 例1：(将test函数作为参数传入test1)

```sw
func test() -> Void{
    print("test()函数")
}

func test1(param:() -> Void){
    param()
}

test1(param: test) 
```

- 例2：(匿名函数作为参数)

```sw
func test1(param:() -> Void){
    param()
}

test1(param: {()->Void in
    print("匿名函数")
})
```

- 例3：(带参，带返回值)
  
```sw
func sum(param:(Int,Int) -> Int ) -> Int{
    return param(1,2) // 实际上是调用了add
}

func add(a:Int,b:Int) -> Int{
    return a + b
}

let value = sum(param: add)
print("value = \(value)")
```

- 例4：(匿名函数方式实现例3)

```sw
func sum(param:(Int,Int) -> Int ) -> Int{
    return param(1,2) // 实际上是调用了add
}

var value = sum(param: {(a:Int,b:Int) -> Int in
    return a + b
})

print("value = \(value)")
```

# 函数作为返回值

>`禁止套娃`😁

```sw
func play1(value:Int) -> Int {
    return value * value
}

func play2(value:Int) -> Int {
    return value + value
}

func test(param:Bool) -> (Int) -> Int {
    return param ? play1 : play2
}

let a = test(param: true) // 此时a为play1

a(3) // 9
```

# 内嵌函数

和上面的套娃一样，更改成内嵌的方式书写

```sw
func test1(param:Bool) -> (Int) -> Int {
    
    func play1(value:Int) -> Int {
        return value * value
    }

    func play2(value:Int) -> Int {
        return value + value
    }
    
    return param ? play1 : play2
}

let b = test1(param: false) // 此时b为play2

b(3) // 6
```

# 匿名函数及简写

## 1.匿名函数类型

- 无参无返回值
```sw
var a:() -> Void = {() -> Void in
   print("a")
}
a()
```
- 可简写为:
```sw
var a:() -> Void = {
   print("a")
}
a()
```

- 根据类型推断，还可以简写为
```sw
var a = {
   print("a")
}
a()
```

## 2.匿名函数

1. 无参无返

   - 无参无返回值
   ```sw
   func test(param:() -> Void){
      param()
   }
   test(param: {() -> Void in
      print("写全了")
   })
   ```

   - 可简写为
   ```sw
   test(param: {print("test简写")})
   ```

   - 还可继续简写为
   ```sw
   test{print("test再次简写")}
   ```

2. 有参无返

   - 有参无返
   ```sw
   func test2(param:(Int)->Void){
      param(10)
   }
   test2(param: {(value:Int) -> Void in
      print(value)
   })
   ```

   - 可简写为
   ```sw
   test2(param: {(value:Int) in
      print(value)
   })
   ```

   - 可根据类型推断继续简写为
   ```sw
   test2(param: {(value) in
      print(value)
   })
   ```

   - 可再次简写为
   ```sw
   test2 { (value) in
      print(value)
   }
   ```

3. 有参有返

   - 有参有返
   ```sw
   func test3(param:(Int,Int) -> Int){
      print(param(10,20))
   }
   test3(param: {(item1:Int,item2:Int) -> Int in
      return item1 + item2
   })
   ```

   - 可简写为
   ```sw
   test3 { (item1, item2) -> Int in
      return item1 + item2
   }
   ```

   - 可继续简写为
   ```sw
   test3(param: {return $0 + $1})
   ```

   - 可最终简写为
   ```sw
   test3(param: {$0 + $1})
   ```
