# 可选链展开

据说是一种“优雅”的书写方式，可以防止空值调用的时候造成报错之类的

```sw
class Data{
    var name:String
    
    init(name:String) {
        self.name = name
    }
    
    func play() {
        print(self.name)
    }
}


class Test{
    var name:String
    var data:Data? = nil
    
    init(outname name:String,data:Data) {
        self.name = name
        self.data = data
    }
    
    deinit {
        print("Test实被销毁")
    }
}

var t:Test? = Test(outname: "hello", data: Data(name:"world"))
t?.data?.play()
```