
# 基本操作

- 定义方式

```sw
var a:Dictionary<String,String> = ["a":"A","b":"B"]
var b:[Int:String] = [1:"a",2:"b"]
var c = [1:"c"]
```

# 增

有则修改，无则增加

```sw
a.updateValue("swift", forKey: "ios")
```

# 删

```sw
a.removeValue(forKey: "b") // key不存在也不会报错
```

通过过滤删除
```sw
a.filter { (key,value) -> Bool in
    if key == "b" {
        return false
    }
    return true
}
```

# 改

```sw
a["a"] = "C"
或者
a.updateValue("swift", forKey: "ios")
```

# 查

- 一般查询：
```sw
print(a["asd"] ?? "unknow") // unknow
```

- 可选绑定查询：
```sw
if let value = a["a"] {
    print(value) // A
}
```

# 遍历

```sw
for (key,value) in a {
    print("key: \(key), value: \(value)")
}
```