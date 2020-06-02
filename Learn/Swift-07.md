# 基本操作

- 定义方式

```sw
var a = [1,2,3,4]
var b:[String] = ["hello","world"]
var c:Array<Double> = [1.4,1.6]
var d = [Int]() // 通过初始化器，定义可变的空数组
var d = Array(repeating: -1, count: 3) // 通过Array初始化器，生成一个，初始值为-1，长度为3的数组(-1,-1,-1)
```

- 根据index取值

```sw
a[0]
```

- 数组比较

```sw
array1 == array2 // 直接判断
```

- 遍历

```sw
for in // 区间、索引或者直接遍历
for item in array[0...] // 无限大的区间去遍历数组
```


# 增

直接用+ 或 append
```sw
a = a + [1,2]
或
a.append(3)
```

插入：
```sw
var array = [1,2,3,4]
array.insert(4, at: 2)
print(array)
```

# 删
根据index修改：
```sw
array.remove(at: index)
```

# 改
根据index修改：
```sw
var array = [1,2,3,4]
array[0] = 2
print(array)
// 输出：[2, 2, 3, 4]
```

替换：
```sw
var array = [1,2,3,4]
array.replaceSubrange((0...2), with: [3,2,1])
print(array)
```

# 查

是否存在：
```sw
array.contains(xx)
```

# 排序演示

倒叙：
```sw
var array = [1,2,3,4,5,6,7]
array.sort { (s1, s2) -> Bool in
    if s1 > s2 {
        return true
    }else{
        return false
    }
}
print(array)
// 输出：[7, 6, 5, 4, 3, 2, 1]
```

过滤(记得用新数组接收)：
```sw
var array = [1,2,3,4,5,6,7]
var new_array = array.filter { (item) -> Bool in
    if item != 3 {
        return true
    }else{
        return false
    }
}
print(new_array)
// 输出：[1, 2, 4, 5, 6, 7]
```

