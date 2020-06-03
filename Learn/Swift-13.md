# 定义方式

- 基础方式
  
```sw
struct Test{
    var a = 10
}

var t1 = Test()
print(t1.a) // 10
var t2 = t1 // 这里其实是深拷贝
t2.a = 100

print(t1.a) // 10
print(t2.a) // 100
```

- 复杂方式

其实不建议定义这么复杂的，复杂的操作由类去操作就可以了

```sw
struct Student{
    var name = "unknow"
    var age = 0
    var score = 0.0
    var ispass = false
    
    static var schoolName = "家里蹲大学"
    
    //初始化器（构造方法）
    init(name:String,age:Int,score:Double) {
        self.name = name
        self.age = age
        self.score = score
        if self.score < 60 {
            self.ispass = false
        }else{
            self.ispass = true
        }
    }
    
    /*
        不太建议以下的方式，因为把 类 的活给抢了
     */
    
    func getName() -> String {
        return self.name
    }
    
    func getAge() -> Int {
        return self.age
    }
    
    func getScore() -> Double {
        return self.score
    }
    
    func getIspass() -> Bool {
        return self.ispass
    }
    
    // 想在结构体里修改属性值，需要增加 mutating 关键字
    mutating func setScore(score:Double) {
        self.score = score
        if self.score < 60 {
            self.ispass = false
        }else{
            self.ispass = true
        }
    }
}

// 创建Student实例
var a = Student(name: "A", age: 18, score: 59)
print("姓名：" + a.getName())          // 姓名：A
print("年龄：" + String(a.getAge()))   // 年龄：18
print("分数：" + String(a.getAge()))   // 分数：18
print("学校：" + Student.schoolName)   // 学校：家里蹲大学
Student.schoolName = "家外蹲小学"
print("学校：" + Student.schoolName)   // 学校：家外蹲小学
```