# 类的定义

- 实例变量：每创建一个实例，就会为实例变量分配一次内存，实例变量可以在内存中有多个拷贝，互不影响（灵活）
- 静态变量：在内存中只有一个拷贝（节省内存），可用类名直接访问（方便）

```sw
class Student{
    //实例变量
    private var name:String = ""
    
    // 静态变量
    public static var schoolName = "家里蹲大学"
    
    //便利构造器是在init前加一个关键子convenience，它为一些属性提供默认值
    convenience init() {
        self.init(name:"unkonw")
    }
    
    init(name:String) {
        self.name = name
    }
    
    func setName(newName:String) {
        self.name = newName
    }
    
    func getName() -> String {
        return self.name
    }
}

var student_A = Student()
print(student_A.getName()) // unkonw

var student_B = Student(name:"老王")
print(student_B.getName()) // 老王

student_B.setName(newName: "隔壁老王")
print(student_B.getName()) // 隔壁老王

print(Student.schoolName) // 家里蹲大学

Student.schoolName = "蹲不住大学"
print(Student.schoolName) // 蹲不住大学
```

# 类的传值

类的传值为`浅拷贝`

```sw
var student_A = Student(name:"老王")
let student_B = student_A // 和结构体不同，类即使用let定义，也可以修改值

print(student_A.getName()) // 老王
print(student_B.getName()) // 老王

student_B.setName(newName: "老王2")

print(student_A.getName()) // 老王2
print(student_B.getName()) // 老王2
```

# 类的继承
```sw
class Person{
    private var name: String
    
    init(name:String) {
        self.name = name
    }
    
    public func setName(name:String){
        self.name = name
    }
    
    public func getName() -> String {
        return self.name
    }
}

// Student 继承了 Preson类
class Student: Person {
    public var age: Int = 0
}

var per = Person(name: "Person")
print(per.getName()) // Person

var stu = Student(name: "Student")
print(stu.getName()) // Student
stu.setName(name: "New Student")
print(stu.getName()) // New Student
stu.age = 100
print(stu.age) // 100
```

# 类型转换(向上/下、可选)

以上面的例子为例，如果将stu的类型设定为Any，那么是无法调用`stu.getName()`的，因此要使用`as`操作符进行类型转换

```sw
var stu:Any = Student(name: "Student")

let s = stu as! Student // 向下类型转换

print(s.getName())
```

- as ：从派生类转换为基类，向上转型（upcasts）
- as! ：向下转型（Downcasting）时使用。由于是强制类型转换，如果转换失败会报 runtime 运行错误。
- as? ：as? 和 as! 操作符的转换规则完全一样。但 as? 如果转换不成功的时候便会返回一个 nil 对象。成功的话返回可选类型值。由于 as? 在转换失败的时候也不会出现错误，所以对于如果能确保100%会成功的转换则可使用 as!，否则使用 as?

# 类的相等判断
```sw
class A{
    
}

var a = A()
var b = A()
var c = a

print(a === b) // false 因为2个都是新创建的不同的对象
print(a === c) // true 直接赋值，浅拷贝，指向同一个地址
```