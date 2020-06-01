# 基本操作

- 判断长度
```sw
str.count
```

- 是否包含某个字符
```sw
str.contains("E")
```

- 是否已xx为开头或结尾
```sw
str.hasPrefix("AB")
str.hasSuffix("EF")
```



# 增

- 追加字符串
```sw
str.append("xx")
```

- 插入字符串
```sw
var str = "ABCDEF"
str.insert(contentsOf: "xx", at: str.index(str.startIndex, offsetBy: 2))
print(str) 
//输出： ABxxCDEF
```

# 删
- 根据index删除
```sw
var str = "ABCDEF"
str.remove(at: str.index(str.startIndex, offsetBy: 2))
print(str)
// 输出：ABDEF
```

- 范围删除
```sw
var str = "ABCDEF"
var a = str.index(str.startIndex, offsetBy: 2)
var b = str.index(str.startIndex, offsetBy: 4)
str.removeSubrange(a...b)
print(str)
// 输出： ABF
```


# 改

- 根据范围替换字符串
```sw
var str = "ABCDEF"
var a = str.index(str.startIndex, offsetBy: 2)
var b = str.index(str.startIndex, offsetBy: 4)
let range = a...b
str.replaceSubrange(range, with: "xxx")
print(str)
// 输出： ABxxxF
```

- 根据字符串替换
```sw
var str = "ABCDEF"
str = str.replacingOccurrences(of: "BC", with: "888")
print(str)
// 输出：A888DEF
```

# 查

- 取首位:
```sw
str[str.startIndex]
```

- 取最后一位（endIndex取得是最后一位的下一位）:
```sw
str[str.index(before: str.endIndex)]
```

- 从首尾开始，往后数2位:
```sw
var str = "ABCDEF"
print(str[str.index(str.startIndex, offsetBy: 2)])
// 输出：C
```

- 取区间 index 2~4：
```sw
var str = "ABCDEF"
var a = str.index(str.startIndex, offsetBy: 2)
var b = str.index(str.startIndex, offsetBy: 4)
print(str[a...b]) 
//输出：CDE
```

- 找到字符对应的Index：
```sw
var str = "ABCDEF"
var e = str.firstIndex(of: "E") ?? nil
```

- 截取前4位：
```sw
var str = "ABCDEF"
print(str.prefix(4))
//输出：ABCD
```

# 遍历字符串
- 基本遍历
```sw
for item in str
{
    print(item)
}
```

- 根据index遍历
```sw
for index in 0..<str.count-1
{
    print(str[str.index(str.startIndex, offsetBy: index)])
}
```

# 多行文本
文字会按照3引号内格式输出
```sw
let a = """
        asdad
asdasd
            asdasd
"""
```

# 特殊符号
用#将字符串包起来
```sw
let b = #""asda!@(*&#(*!&@#sd""#
```
