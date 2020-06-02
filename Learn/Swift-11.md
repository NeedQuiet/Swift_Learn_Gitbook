# guard语句

# 基本用法

```sw
//可以理解为不满局，就拦截
func test(param:Int){
    guard param < 10 else {
        print("进入guard语句里")
        
        //'guard' body must not fall through, consider using a 'return' or 'throw' to exit the scope
        //'guard'主体必须是不能穿透的，请考虑使用“return”或“throw”退出作用域
        return
    }
    print("hello")
}

test(param: 5) // hello

// 等同于
func test2(param:Int){
    if param < 10 {
        print("hello 2")
    }else{
        return
    }
}
```

# 利用可选项绑定

```sw
func test(param:Int?){
    //Initializer for conditional binding must have Optional type, not 'Int'
    //参数必须是可选值
    guard let value = param else {
        print("进入guard语句里")
        return
    }
    
    // 注意这里可以直接获取value
    print(value)
}

test(param: 10)
```