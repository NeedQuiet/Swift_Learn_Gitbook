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

#   无主引用

- 首先我们看一下下面的例子，最后虽然 `testA = nil`，但是`TestA`和`TestB`的`deinit`都没有执行；

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
      
      var ref:TestA
      
      init(name:String,ref:TestA) {
          self.name = name
          self.ref = ref
      }
      
      deinit {
          print("TestB被销毁")
      }
  }

  var testA:TestA? = TestA(name: "TestA")

  testA!.ref = TestB(name: "TestB", ref: testA!)

  testA = nil
  ```

  - 这种情况如果我们想销毁TestA和TestB，那么常规的操作为：

  ```sw
  var testA:TestA? = TestA(name: "TestA")

  testA!.ref = TestB(name: "TestB", ref: testA!)
  // 1. 先将testA的ref置空(消除了TestA指向TestB的强引用，此时已经没有引用指向TestB，所以TestB被释放)
  testA!.ref = nil // TestB被销毁 (同时TestB中指向TestA的ref也会被销毁)
  // 2. 再讲testA置空(消除引用名testA对TestA对象的引用)
  testA = nil // TestA被销毁
  ```

  - 上面的方式是可以的，但是如果成员变量多了就不好处理了，所以我们可以引用 `无主引用unowned`

  ```sw
  class TestB{
      var name:String
      
      // 无主引用 unowned
      unowned var ref:TestA
      
      init(name:String,ref:TestA) {
          self.name = name
          self.ref = ref
      }
      
      deinit {
          print("TestB被销毁")
      }
  }
  ```

  我们只需将TestB的ref设为无主引用，这时如果销毁了TestA，那么TestB指向TestA的无主引用ref也会同时断开;<br>
  和弱引用不同，如果使用weak，那么TestB的ref就需要设定为可选类型

# 闭包造成的循环引用
  Test的data属性指向了一个闭包，闭包中的self引用指向了当前的实例，造成了闭包循环引用，无法释放

  ```sw

  class Test{
      var name:String
      
      // 需要加lazy关键字（因为此时可能还没有初始化，就去使用self了）
      lazy var data:() -> Void = {() -> Void in
          print(self.name)
      }
      
      
      init(name:String) {
          self.name = name
      }
      
      deinit {
          print("Test被销毁 - " + self.name)
      }
  }


  var t:Test? = Test(name: "hello")

  t!.data()

  t = nil
  ```

  所以我们只要将闭包的中的self强引用干掉，就可以正常释放Test对象了，在此我们引入一个方式：<br>
  `定义捕获列表`

  ```sw
  lazy var data:() -> Void = {[unowned self]() -> Void in
      print(self.name)
  }
  ```