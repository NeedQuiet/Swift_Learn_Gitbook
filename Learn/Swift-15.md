# 基本用法

>下标（subscript）在数组和字典中使用，但是你可以给任何类型（枚举，结构体，类）增加 下标subscript 的功能；<br>subscript的语法类似实例方法、计算属性，其本质就是方法；

```sw
struct Person {
    var age = 0
    var no  = 0
    subscript(index: Int) -> Int {
        set {
            if index == 0 {
                age = newValue
            } else {
                no = newValue
            }
        }
        get {
            if index == 0 {
                return age
            } else {
                return no
            }
        }
    }
}

var p = Person()
p[0] = 10
p[1] = 20

print(p.age)  // 10
print(p[0])   // 10

print(p.no)  // 20
print(p[1])  // 20
```

# 说明

- subscript 的返回值类型决定了：
  - get 方法的返回值类型；
  - set 方法中 newValue 的类型；
- subscript 可以接受多个参数，并且是任意类型；
- subscript 可以没有 `set` 方法，但必须要有 `get` 方法；

***

1. 如果只有 `get` 方法，可以省略 `get{}`，直接写get的内容
  ```sw
  struct Person {
      var age = 30

      subscript(index: Int) -> Int {
          if index == 0 {
              return age
          } else {
              return age * 2
          }
      }
  }

  var p = Person()
  print(p[0])  // 30
  print(p[1])  // 60
  ```

2. subscript 可以设置参数标签；
```sw
struct Person {
    var age = 30

    subscript(index i: Int) -> Int {
        if i == 0 {
            return age
        } else {
            return age * 2
        }
    }
}
var p = Person()
print(p[index:0])  // 30
print(p[index:1])  // 60
```

3. subscript 可以是类型方法；
```sw
struct Person {
    static subscript(index:Int) -> Int {
        if index == 0 {
            return 30
        } else {
            return 60
        }
    }
}
/*
    这里没有用 var p = Person() 创建实例 ！！！
*/
print(Person[0])  // 30
print(Person[1])  // 60
```

4. 类和结构体作为返回值
>作为只读(get)返回值时，结构体是不可修改的，因为结构体的内存不可变；

   ```sw
   class Point {
       var x = 0
       var y = 0
   }

   /* 这里是不能用结构体的
   strust Point {
       var x = 0
       var y = 0
   }
   */

   class PointM {
       var point = Point()
       subscript(index: Int) -> Point {
           get {
               return point
           }
       }
   }

   var pm = PointM()
   pm[0].x = 10
   pm[0].y = 20

   // 如果上面用的结构体，这里会报错(...subscript is get-only)
   print(pm[0].x)  // 10
   print(pm[0].y)  // 20
   ```

# 多个参数
```sw
class Matix {
    var data = [
       [1,0,0],
       [0,1,0],
       [0,0,1]
    ]
    subscript(row: Int , col: Int) -> Int {
        set {
            guard row >= 0 && row < 3 && col >= 0 && col < 3 else {
                return
            }
            data[row][col] = newValue
        }
        get {
            guard row >= 0 && row < 3 && col >= 0 && col < 3 else {
                return 0
            }
            return data[row][col]
        }
    }
}

var m = Matix()
m[1, 1] = 3
m[0, 1] = 4
```