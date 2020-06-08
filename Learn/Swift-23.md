
>一个无名函数（闭包）作为一个参数传给一个正常的函数

# 尾随闭包

其实前面的匿名函数中有简单介绍过：[10.函数->匿名函数及简写](./Swift-10.md#匿名函数及简写)

- 有参数 无返回值

  ```sw
  func play1(param1:String,param2:(String)->Void){
      param2(param1 + " - Swift") // 简写了return
  }

  play1(param1: "正常写法", param2:  {(data:String) -> Void in
      print(data)
  })

  play1(param1: "尾随闭包写法") { (data) in
      print(data)
  }
  ```

- 无参数 无返回值

  简写过程

  ```sw
  func play(param:()->Void){
      param()
  }

  play(param: {()->Void in
      print("play")
  })

  play(){()->Void in
      print("play")
  }

  play (){
      print("play")
  }

  play {
      print("play")
  }
  ```

- 无参数 有返回值

  ```sw
  func play(param:() -> String){
      print(param()) 
  }

  play(param: {() -> String in
      return "play"
  })

  play(){() -> String in
      return "play"
  }

  play (){
      "play"
  }

  play {
      "play"
  }
  ```