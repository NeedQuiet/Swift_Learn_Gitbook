# 延迟加载 Lazy

- 我们以下面代码为例，常规情况下我们都是这样书写代码的

  ```sw
  class Data{
      init() {
          print("Data init")
      }
      func play() {
          print("Data play")
      }
  }

  class Test{
      var data:Data = Data()
      init() {
          print("Test init")
      }
  }
  var test = Test()
  /**
   输出：
       Data init
       Test init
   */
  ```

- 很明显，是Data先初始化，然后Test才初始化；但是有的时候我们仅仅想让Data在我们需要的时候初始化，而不是每次初始化Test都会先去初始化Data，这时，我们就可以用`lazy`属性来改进代码，达到什么时候用，什么时候再去初始化的目的

  ```sw
  class Data{
      init() {
          print("Data init")
      }
      func play() {
          print("Data play")
      }
  }

  class Test{
      // 这里添加lazy关键字
      lazy var data:Data = Data()
      init() {
          print("Test init")
      }
  }
  var test = Test()

  print("我要初始化data了")

  test.data // 使用的时候才会初始化
  /**
   输出：
       Test init
       我要初始化data了
       Data init
   */
  ```
