

>Set和Array类似但是不同，Array是有序的集合，但是Set却是无序的集合(因为无序，所以内容不能重复)

# 基本操作

声明:
```sw
var a:Set = [1,2,3,4]

//指定类型
var b:Set<String> = ["hello","world"]
var c:Set<Int> = []

//长度
a.count
```

遍历、过滤等其他基本操作使用方式和[Array](./Swift-07.md)差不多，就不多叙述了

# 集合比较
```sw
var a:Set = [1,2,3,4]
var b:Set<Int> = [5,6,1]

// 将两个Set合并，返回新的Set（不会有重复的值）
var c = a.union(b) // {4, 3, 2, 5, 1, 6}

// 返回两个Set中相同的数据
var d = a.intersection(b) // {1}

// 返回两个Set中不同的数据
var e = a.symmetricDifference(b) // {4, 3, 2, 5, 6}

// 两个Set比较，返回a中跟b不同的数据（只返回）
var f = a.subtracting(b) // {4, 3, 2}
```