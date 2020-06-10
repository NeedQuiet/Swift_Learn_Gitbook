# 访问权限

swift中访问权限由大到小依次为：open，public，internal（默认），fileprivate，private。

1. open

    可以在任何地方访问，包括override和继承。

2. public

    可以在任何地方访问，但其他module中不可以被override和继承，而在本module内可以被override和继承。

3. internal（默认访问级别，internal修饰符可写可不写）

    新建文件时默认为internal，所修饰的属性或方法在整个模块内都可以访问。

4. fileprivate

    在当前文件内可以被访问。

5. private
  
    在当前类中能被访问，extension中不能访问。

# 重写: override

重写父类方法, 必须加上override关键字

```sw
class Man {
    func sleep(){
        print("父类睡觉")
    }
}

class SonMan: Man {
    var power:Int = 100
    // override关键字主要是为了明确表示重写父类方法，所以如果要重写父类方法, 必须加上override关键字
    override func sleep() {
        // sleep() 不能这样写, 会导致递归
        super.sleep() // 此处可以选择不调用
        print("子类睡觉")
    }
}
var sm = SonMan()
sm.sleep()
/**
 输出：
     父类睡觉
     子类睡觉
 */
```

# 禁止重写: final
final关键字可以在`class`、`func`和`var`前修饰。表示不允许对其修饰的内容进行继承或者重新操作。

```sw
class Parent {
   final func method1() {
       //权限验证（必须执行）
       //.....
        
       method2()
        
       //下面是日志记录（必须执行）
       //..........
   }
    
   func method2(){
       //父类的实现
       //......
   }
}

class Child : Parent {
   //只能重写父类的method2方法，不能重写method1方法
   override func method2() {
       //子类的实现
       //......
   }
}
```

# 扩展: extension

- 对类进行拓展：

  ```sw
  class A{
      
  }

  extension A{
      func printString(name:String) {
          print("拓展方法：" + name)
      }
  }

  let a = A()
  a.printString(name: "Test")

  // 输出： 拓展方法：Test
  ```

- 对String进行拓展

  ```sw
  extension String{
      func toString() -> String {
          return "长度 = " + String(self.count)
      }
  }

  var Str:String = "hello"
  print(Str.toString())
  //输出： 长度 = 5
  ```

# 泛型

简单理解就是用来代替任何类型

```sw
func toString<T>(param:T) -> T {
    return param
}

print(toString(param: "hello"))
print(toString(param: 10))
print(toString(param: [1,2,3]))
```

# 必要初始化器: required

参考：[必要初始化器: required](./Swift-20.md#必要初始化器required)