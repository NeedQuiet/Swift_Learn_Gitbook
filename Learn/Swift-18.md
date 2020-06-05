# 基础写法
```sw
class TestClass{
    
}

protocol Protocol1{
    var value1: String{set get} // 读写
    func play1() -> String
    
}

protocol Protocol2{
    var value2: String{get} // 只读
    func play2() -> String
}

class Data:TestClass,Protocol1,Protocol2{
    
    var value1: String
    
    var value2: String{
        return "value2"
    }
    
    func play1() -> String {
        return self.value1
    }

    func play2() -> String {
        return self.value2
    }
    
    init(value1:String) {
        self.value1 = value1
    }
}

var data = Data(value1: "hello")
print(data.play1()) // hello
print(data.play2()) // value2
```