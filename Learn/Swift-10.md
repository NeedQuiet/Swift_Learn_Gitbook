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