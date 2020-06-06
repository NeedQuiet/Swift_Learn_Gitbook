# 循环引用以及如何使用弱引用weak

- 下面的范例是一个循环引用，TestA和TestB相互引用的对方，这时即使将TestA置为空值也是无法释放掉的，因为依然在相互强引用

  ```sw
  class TestA{
      var name:String
      
      var ref:TestB? = nil
      
      init(name:String) {
          self.name = name
      }
      
      deinit {
          print("TestA被销毁")
      }
  }

  class TestB{
      var name:String
      
      var ref:TestA? = nil
      
      init(name:String) {
          self.name = name
      }
      
      deinit {
          print("TestB被销毁")
      }
  }

  var testA:TestA? = TestA(name: "TestA")
  var testB:TestB? = TestB(name: "TestB")
  testA!.ref = testB
  testB!.ref = testA

  testA = nil
  ```

- 这时可以用弱引用weak来解决：

  ```sw
  class TestA{
      var name:String
      
      weak var ref:TestB? = nil
      
      ...
  }

  class TestB{
      var name:String
      
      weak var ref:TestA? = nil
      
      ...
  }
  ```