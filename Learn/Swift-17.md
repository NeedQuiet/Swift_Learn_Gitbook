# 访问权限

swift中访问权限由大到小依次为：open，public，internal（默认），fileprivate，private。

- open：可以在任何地方访问，包括override和继承。
- public：可以在任何地方访问，但其他module中不可以被override和继承，而在本module内可以被override和继承。
- internal：新建文件时默认为internal，所修饰的属性或方法在整个模块内都可以访问。
- fileprivate：在当前文件内可以被访问。
- private：在当前类中能被访问，extension中不能访问。

# 重写关键字: override

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